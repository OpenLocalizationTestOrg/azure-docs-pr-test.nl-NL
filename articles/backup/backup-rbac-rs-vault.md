---
title: Back-ups met op rollen gebaseerd toegangsbeheer van Azure beheren | Microsoft Docs
description: Gebruik toobackup beheerbewerkingen voor toegangsbeheer op basis van rollen toomanage toegang in Recovery Services-kluis.
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 3bd46b97-4b29-47a5-b5ac-ac174dd36760
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/22/2017
ms.author: trinadhk;markgal
ms.openlocfilehash: 26d034d152f9b77fc6d5b2ffd5ef2648b1797f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-azure-backup-recovery-points"></a>Herstelpunten voor toegangsbeheer op basis van rollen toomanage Azure Backup gebruiken
Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over geavanceerd toegangsbeheer voor Azure. Met RBAC kunt u taken scheiden binnen uw team en alleen Hallo hoeveelheid toousers toegang verlenen die zij nodig hebben tooperform hun werk.

> [!IMPORTANT]
> Rollen die worden geleverd door Azure Backup zijn beperkt tooactions die kunnen worden uitgevoerd in Azure-portal of PowerShell-cmdlets voor Recovery Services-kluis. Acties die worden uitgevoerd in Azure backup Agent Client-gebruikersinterface of System center Data Protection Manager UI of de gebruikersinterface van Azure Backup-Server aanwezig zijn buiten de controle van deze rollen.

Azure Backup biedt ingebouwde rollen 3 toocontrol Backup-beheertaken uit te voeren. Meer informatie over [ingebouwde Azure RBAC-rollen](../active-directory/role-based-access-built-in-roles.md)

* [Back-up Inzender](../active-directory/role-based-access-built-in-roles.md#backup-contributor) -deze rol heeft alle machtigingen toocreate en back-up, behalve de Recovery Services-kluis maken en geeft toegang tot tooothers beheren. Denk aan deze rol als beheerder van back-management die elke back-management-bewerking kunt uitvoeren.
* [Back-up Operator](../active-directory/role-based-access-built-in-roles.md#backup-operator) -deze rol heeft machtigingen tooeverything Inzender behalve back-up en het beheer van back-upbeleid te verwijderen. Deze rol is gelijkwaardig toocontributor behalve mag destructieve zoals back-ups van stoppen met het verwijderen van gegevens bewerkingen of verwijder de registratie van lokale bronnen.
* [Back-up lezer](../active-directory/role-based-access-built-in-roles.md#backup-reader) -deze rol heeft machtigingen tooview alle back-beheertaken uit te voeren. Denk aan deze rol toobe bewaking van een persoon.

Als u op zoek bent toodefine uw eigen rollen voor nog meer controle, Zie hoe te[aangepaste rollen maken](../active-directory/role-based-access-control-custom-roles.md) in Azure RBAC.



## <a name="mapping-backup-built-in-roles-toobackup-management-actions"></a>Toewijzing van de ingebouwde rollen toobackup acties back-up
Hallo tabel vastgelegd Hallo acties voor back-up en bijbehorende minimale RBAC-rol vereist tooperform die voor deze bewerking.

| Bewerking voor het beheer | Minimale RBAC-rol vereist |
| --- | --- |
| Recovery Services-kluis maken | Inzender voor de resourcegroep van de kluis |
| Back-up van Azure Virtual machines inschakelen | Back-upoperator op de kluis, bijdrager van de virtuele machine op virtuele machines |
| Op aanvraag back-up van de virtuele machine | Back-upoperator |
| Virtuele machine herstellen | Back-upoperator, Resource groep Inzender waarin VM en Vnets tooget geïmplementeerd gaat |
| Schijven, afzonderlijke bestanden in de VM-back-up herstellen | Back-upoperator |
| Back-upbeleid voor virtuele machine van Azure back-up maken | Back-up Inzender |
| Back-upbeleid van virtuele machine van Azure back-up wijzigen | Back-up Inzender |
| Back-upbeleid van virtuele machine van Azure back-up verwijderen | Back-up Inzender |
| Back-up stoppen (met behoud van gegevens of gegevens verwijderen) in VM-back-up | Back-up Inzender |
| Lokale Windows Server/client-/ SCDPM of Azure Backup-Server registreren | Back-upoperator |
| Geregistreerde lokale Windows Server/client-/ SCDPM of Azure Backup-Server verwijderen | Back-up Inzender |

## <a name="next-steps"></a>Volgende stappen
* [Op rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md): aan de slag met RBAC in hello Azure-portal.
* Meer informatie over hoe toomanage met toegang tot:
  * [PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  * [Azure-CLI](../active-directory/role-based-access-control-manage-access-azure-cli.md)
  * [REST API](../active-directory/role-based-access-control-manage-access-rest.md)
* [Probleemoplossing voor toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-troubleshooting.md): Profiteer van tips voor het oplossen van veelvoorkomende problemen.
