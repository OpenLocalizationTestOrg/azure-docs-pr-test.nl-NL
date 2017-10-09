---
title: aaaProtecting uw netwerk in Azure Security Center | Microsoft Docs
description: Dit document gaat in Azure Security Center aanbevelingen die u helpen beveiligen van uw Azure-netwerk en blijven in overeenstemming met het beveiligingsbeleid.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a>Beveiligen van uw netwerk in Azure Security Center
Azure Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources. Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, maakt deze aanbevelingen die u helpt bij Hallo Hallo nodig-besturingselementen configureren.  Aanbevelingen tooAzure brontypen die van toepassing: virtuele machines (VM's), netwerken, SQL en toepassingen.

In dit artikel biedt de aanbevelingen die van toepassing zijn tooyour netwerk.  Netwerkcentrum aanbevelingen om de volgende generatie firewalls, Netwerkbeveiligingsgroepen en regels voor binnenkomend verkeer op configureren.  Gebruik Hallo onderstaande tabel als een verwijzing toohelp erkent u Hallo beschikbaar netwerk aanbevelingen en elke eigenschap als u deze toe te passen.

## <a name="available-network-recommendations"></a>Aanbevelingen voor de beschikbare netwerken
| Aanbeveling | Beschrijving |
| --- | --- |
| [Een firewall van de volgende generatie toevoegen](security-center-add-next-generation-firewall.md) |Raadt aan dat u, een volgende generatie Firewall (NGFW) van een Microsoft-partner tooincrease uw beveiligingsinstellingen toevoegt. |
| [Verkeer alleen via NGFW sturen](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Raadt aan dat u configureert (NSG) netwerkbeveiligingsgroepen die binnenkomend verkeer tooyour VM via uw NGFW afdwingen. |
| [Netwerkbeveiligingsgroepen op subnetten of virtuele machines inschakelen](security-center-enable-network-security-groups.md) |Raadt het nsg's op subnetten of VM's in te schakelen. |
| [Toegang tot en met een Internetgericht eindpunt beperken](security-center-restrict-access-through-internet-facing-endpoints.md) |Raadt aan dat u regels voor binnenkomend verkeer voor het nsg's configureren. |

## <a name="see-also"></a>Zie ook
toolearn meer informatie over de aanbevelingen die van toepassing zijn tooother Azure brontypen, Zie de volgende Hallo:

* [Beveiligen van uw virtuele machines in Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Beveiligen van uw toepassingen in Azure Security Center](security-center-application-recommendations.md)
* [Beveiligen van uw Azure SQL-service in Azure Security Center](security-center-sql-service-recommendations.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
