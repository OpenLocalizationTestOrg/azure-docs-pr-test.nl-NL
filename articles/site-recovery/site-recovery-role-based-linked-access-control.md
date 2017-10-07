---
title: aaaUsing toegangsbeheer op basis van rollen toomanage Azure Site Recovery | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooapply en het gebruik rollen gebaseerd toegangsbeheer (RBAC) toomanage uw Azure Site Recovery-implementaties
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: manayar
ms.openlocfilehash: 7b721090351e561b28317ccdcf0ff283e0b146ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-site-recovery-deployments"></a>Toegangsbeheer op basis van rollen toomanage Azure Site Recovery-implementaties kan gebruiken

Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over geavanceerd toegangsbeheer voor Azure. Met RBAC kunt u taken scheiden binnen uw team en verleen alleen toegang met specifieke machtigingen toousers als benodigde tooperform specifieke taken.

Azure Site Recovery biedt ingebouwde rollen 3 toocontrol Site Recovery-beheerbewerkingen. Meer informatie over [ingebouwde Azure RBAC-rollen](../active-directory/role-based-access-built-in-roles.md)

* [Site Recovery Inzender](../active-directory/role-based-access-built-in-roles.md#site-recovery-contributor) -deze rol heeft alle machtigingen vereist toomanage Azure Site Recovery-bewerkingen in een Recovery Services-kluis. Een gebruiker met deze rol echter niet maken of verwijderen van een Recovery Services-kluis of toegang rechten tooother gebruikers toewijzen. Deze rol is het meest geschikt voor disaster recovery beheerders die kunnen inschakelen en beheren van herstel na noodgevallen voor toepassingen of volledige organisaties Hallo geval zijn.
* [Site Recovery-Operator](../active-directory/role-based-access-built-in-roles.md#site-recovery-operator) -heeft machtigingen tooexecute manager Failover en Failback bewerkingen en deze functie. Een gebruiker met deze rol kan niet- of uitschakelen replicatie, maken of verwijderen van kluizen, registreren van nieuwe infrastructuur of toegang rechten tooother gebruikers toewijzen. Deze rol is het meest geschikt is voor een disaster recovery operator die failover virtuele machines kunt of toepassingen wanneer u hierom wordt gevraagd door toepassingseigenaars en IT-beheerders in een situatie met een bestaande of gesimuleerde na noodgevallen zoals een DR zoomen. Post resolutie van Hallo na noodgevallen, Hallo DR-operator opnieuw kunt beveiligen en failback Hallo virtuele machines.
* [Site Recovery-lezer](../active-directory/role-based-access-built-in-roles.md#site-recovery-reader) -deze rol heeft machtigingen tooview alle beheerbewerkingen van Site Recovery. Deze rol is het meest geschikt is voor een IT-bewaking leidinggevende die kunt bewaken Hallo huidige status van beveiliging en ondersteuningstickets verhogen, indien nodig.

Als u op zoek bent toodefine uw eigen rollen voor nog meer controle, Zie hoe te[aangepaste rollen maken](../active-directory/role-based-access-control-custom-roles.md) in Azure.

## <a name="permissions-required-tooenable-replication-for-new-virtual-machines"></a>Machtigingen vereist tooEnable replicatie voor de nieuwe virtuele Machines
Wanneer een nieuwe virtuele Machine gerepliceerde tooAzure met Azure Site Recovery is, van de gebruiker die is gekoppeld Hallo toegangsniveaus zijn gevalideerde tooensure die gebruiker Hallo Hallo vereist machtigingen toouse hello Azure-resources opgegeven tooSite herstel.

tooenable replicatie voor een nieuwe virtuele machine, een gebruiker moet hebben:
* Machtiging toocreate een virtuele machine in de geselecteerde resourcegroep Hallo
* Machtiging toocreate een virtuele machine in de geselecteerde virtuele netwerk Hallo
* Machtiging toowrite toohello geselecteerde opslagaccount

Een gebruiker moet Hallo machtigingen toocomplete replicatie van een nieuwe virtuele machine te volgen.

> [!IMPORTANT]
>Zorg ervoor dat de relevante machtigingen per Hallo-implementatiemodel zijn toegevoegd (Resource Manager / klassieke) gebruikt voor de implementatie van de resource.

| **Resourcetype** | **Implementatiemodel** | **Machtiging** |
| --- | --- | --- |
| Compute | Resource Manager | Microsoft.Compute/availabilitySets/read |
|  |  | Microsoft.Compute/virtualMachines/read |
|  |  | Microsoft.Compute/virtualMachines/write |
|  |  | Microsoft.Compute/virtualMachines/delete |
|  | Klassiek | Microsoft.ClassicCompute/domainNames/read |
|  |  | Microsoft.ClassicCompute/domainNames/write |
|  |  | Microsoft.ClassicCompute/domainNames/delete |
|  |  | Microsoft.ClassicCompute/virtualMachines/read |
|  |  | Microsoft.ClassicCompute/virtualMachines/write |
|  |  | Microsoft.ClassicCompute/virtualMachines/delete |
| Netwerk | Resource Manager | Microsoft.Network/networkInterfaces/read |
|  |  | Microsoft.Network/networkInterfaces/write |
|  |  | Microsoft.Network/networkInterfaces/delete |
|  |  | Microsoft.Network/networkInterfaces/join/action |
|  |  | Microsoft.Network/virtualNetworks/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/read |
|  |  | Microsoft.Network/virtualNetworks/subnets/join/action |
|  | Klassiek | Microsoft.ClassicNetwork/virtualNetworks/read |
|  |  | Microsoft.ClassicNetwork/virtualNetworks/join/action |
| Storage | Resource Manager | Microsoft.Storage/storageAccounts/read |
|  |  | Microsoft.Storage/storageAccounts/listkeys/action |
|  | Klassiek | Microsoft.ClassicStorage/storageAccounts/read |
|  |  | Microsoft.ClassicStorage/storageAccounts/listKeys/action |
| Resourcegroep | Resource Manager | Microsoft.Resources/deployments/* |
|  |  | Microsoft.Resources/subscriptions/resourceGroups/read |

Overweeg het gebruik van Hallo 'Virtual Machine Contributor' en 'Klassieke Virtual Machine Contributor' [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md) modellen respectievelijk voor de implementatie van Resource Manager en Classic.

## <a name="next-steps"></a>Volgende stappen
* [Toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-configure.md): aan de slag met RBAC in hello Azure-portal.
* Meer informatie over hoe toomanage met toegang tot:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure-CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [Probleemoplossing voor toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-troubleshooting.md): Profiteer van tips voor het oplossen van veelvoorkomende problemen.
