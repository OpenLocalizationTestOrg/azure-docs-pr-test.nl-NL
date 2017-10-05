---
title: Beschikbaarheidssets voor Windows-machines in Azure | Microsoft Docs
description: Meer informatie over de sleutel ontwerpen en implementeren van de richtlijnen voor het implementeren van Beschikbaarheidssets in Azure-infrastructuurservices.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f9449f58-664b-4d5d-82f6-84c5d083047f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f94004fbd32dcc8a2394fcdfe2ac61519364f176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-availability-sets-guidelines-for-windows-vms"></a>Azure beschikbaarheidssets richtlijnen voor VM's van Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Dit artikel is gericht op het inzicht in de vereiste stappen van de planning voor beschikbaarheidssets om te controleren of uw toepassingen blijft toegankelijk tijdens gepland of ongepland gebeurtenissen.

## <a name="implementation-guidelines-for-availability-sets"></a>Richtlijnen voor de implementatie van beschikbaarheidsset instellen
Beslissingen te nemen:

* Hoeveel beschikbaarheidssets moet u voor de verschillende functies en lagen in de infrastructuur van uw toepassingen?

Taken:

* Definieer het aantal virtuele machines in elke toepassingslaag die u nodig hebt.
* Bepalen of u moet het aantal fouten aanpassen of domeinen moet worden gebruikt voor uw toepassing bijwerken.
* Definieer de vereiste beschikbaarheidssets met uw naamgevingsconventie en wat virtuele machines zich bevinden. Een virtuele machine kan alleen worden opgenomen in een beschikbaarheidsset.

## <a name="availability-sets"></a>Beschikbaarheidssets
In Azure, kunnen virtuele machines (VM's) worden geplaatst op een logische groepering aangeroepen van een beschikbaarheidsset. Wanneer u virtuele machines binnen een beschikbaarheidsset maakt, wordt in de Azure-platform de plaatsing van deze VMs verdeelt over de onderliggende infrastructuur. Moet er een gebeurtenis gepland onderhoud aan de Azure-platform of een onderliggende hardware-infrastructuur fault, het gebruik van beschikbaarheidssets zorgt ervoor dat er ten minste één virtuele machine actief blijft.

Als een best practice toepassingen moeten bevindt zich niet op een enkele virtuele machine. Een beschikbaarheidsset die een enkele virtuele machine bevat krijgen geen beveiliging bij gepland of ongepland gebeurtenissen binnen het Azure-platform. De [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines) twee of meer virtuele machines binnen een beschikbaarheidsset om toe te staan de verdeling van virtuele machines over de onderliggende infrastructuur vereist. Als u [Azure Premium-opslag](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), de Azure SLA van toepassing is op een enkele virtuele machine.

De onderliggende infrastructuur in Azure is onderverdeeld met meerdere hardware-clusters. Elk cluster hardware kan een bereik van VM-grootten ondersteunen. Een beschikbaarheidsset kan alleen worden gehost op een cluster met één hardware op elk punt in tijd. Het bereik van VM-grootten die kunnen optreden in een beschikbaarheidsset één is daarom beperkt tot het bereik van VM-grootten ondersteund door de hardware-cluster. Het cluster hardware voor de beschikbaarheidsset is geselecteerd als de eerste virtuele machine in de beschikbaarheidsset is geïmplementeerd of bij het starten van de eerste virtuele machine in een beschikbaarheidsset waar alle VM's momenteel in de status gestopt-de toewijzing ongedaan gemaakt zijn. De volgende PowerShell-opdracht kan worden gebruikt om te bepalen het bereik van VM-grootten beschikbaar voor een beschikbaarheidsset: ' Get-AzureRmVMSize - ResourceGroupName \<tekenreeks\> - AvailabilitySetName \<tekenreeks\>'

Elk cluster hardware is onderverdeeld meerdere domeinen van de update en domeinen met fouten. Deze domeinen zijn gedefinieerd door welke hosts delen een gemeenschappelijke Updatefase of share vergelijkbare fysieke infrastructuur zoals stroom en netwerken. Azure distribueert automatisch uw virtuele machines binnen een beschikbaarheidsset tussen domeinen te onderhouden, beschikbaarheid en fouttolerantie. Afhankelijk van de grootte van uw toepassing en het aantal virtuele machines binnen een beschikbaarheidsset, kunt u het aantal domeinen die u wilt gebruiken aanpassen. U kunt meer lezen over [beschikbaarheid en het gebruik van de update en fouttolerantie domeinen beheren](manage-availability.md).

Plan de toepassingslagen die u gebruikt bij het ontwerpen van de infrastructuur van uw toepassing. Groep virtuele machines die hetzelfde doel in voor de beschikbaarheid van dienen wordt ingesteld, zoals een beschikbaarheidsset voor de front-virtuele machines waarop IIS wordt uitgevoerd. Maak een afzonderlijke beschikbaarheidsset voor uw back-end-VM's met SQL Server. Het doel is om ervoor te zorgen dat elk onderdeel van uw toepassing wordt beveiligd door een beschikbaarheidsset en ten minste eenmaal exemplaar altijd actief blijft.

Load balancers kunnen worden gebruikt voor elke toepassingslaag samenwerking met een beschikbaarheidsset en ervoor zorgen dat verkeer kan altijd worden doorgestuurd naar een actief exemplaar. Uw virtuele machines mogelijk blijven in bedrijf tijdens geplande en ongeplande onderhoud gebeurtenissen zonder een load balancer, maar de eindgebruiker mogelijk niet oplossen als de primaire virtuele machine niet beschikbaar is.

Ontwerp uw toepassing voor hoge beschikbaarheid in de opslaglaag. De beste [gebruik beheerd de schijven voor virtuele machines in een Beschikbaarheidsset](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Als u niet-beheerde schijven en gebruikt we raden u [converteren van virtuele machines in de Beschikbaarheidsset beheerd schijven te gebruiken](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]
