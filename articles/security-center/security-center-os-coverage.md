---
title: aaaSupported platforms in Azure Security Center | Microsoft Docs
description: Dit document bevat een lijst met Windows en Linux operatings-systemen worden ondersteund in Azure Security Center.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: f73e04970749271fc9d75836f4f468b0a4953f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="supported-platforms-in-azure-security-center"></a>Ondersteunde platforms in Azure Security Center
Status beveiligingsbewaking en aanbevelingen zijn beschikbaar voor virtuele machines (VM's) gemaakt met behulp van zowel klassieke Hallo als Resource Manager-implementatiemodel.

> [!NOTE]
> Meer informatie over Hallo [klassieke en Resource Manager-implementatiemodel](../azure-classic-rm.md) voor Azure-resources.
>
>

## <a name="supported-platforms-for-windows-vms"></a>Ondersteunde platforms voor VM's van Windows
Ondersteunde Windows-besturingssystemen:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

> [!NOTE]
>
* OS beveiligingslek beoordelingen zijn nog niet beschikbaar voor Windows Server 2016.
* Crash analysis detecties worden alleen ondersteund voor Windows Server 2012 en Windows Server 2012 R2.
>
>

## <a name="supported-platforms-for-linux-vms"></a>Ondersteunde platforms voor virtuele Linux-machines
Ondersteunde Linux-besturingssystemen:

* Ubuntu versies 12.04, 14.04, 16.04, 16.10
* Debian versies 7, 8
* CentOS 6 versies. \*, 7.*
* Red Hat Enterprise Linux (RHEL) versie 6. \*, 7.*
* SUSE Linux Enterprise Server 11 SP4 + versies (SLES), 12.*
* Versies Oracle Linux 6. \*, 7.*

> [!NOTE]
> Virtuele machine gedragsanalyse zijn nog niet beschikbaar voor Linux-besturingssystemen.
>
>

## <a name="vms-and-cloud-services"></a>Virtuele machines en Cloud-Services
Virtuele machines die worden uitgevoerd in een cloudservice worden ook ondersteund. Alleen cloud services-web- en werkrollen rollen die worden uitgevoerd in de productieomgeving sleuven worden bewaakt. toolearn meer informatie over de service in de cloud, Zie [Cloud Services-overzicht](../cloud-services/cloud-services-choose-me.md).

## <a name="next-steps"></a>Volgende stappen

- [Azure Security Center Planning- en Bedieningsgids](security-center-planning-and-operations-guide.md) : meer informatie hoe tooplan en Hallo ontwerpoverwegingen tooadopt Azure Security Center begrijpen
- [Beveiligingswaarschuwingen op typen in Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-alerts-type.md#virtual-machine-behavioral-analysis) : meer informatie over de virtuele machine gedragsanalyse en crashes dump geheugenanalyse in Security Center
- [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service
- [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) : Lees blogberichten over Azure-beveiliging en naleving
