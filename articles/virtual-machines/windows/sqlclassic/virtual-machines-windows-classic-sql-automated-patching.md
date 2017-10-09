---
title: aaaAutomated patchen voor SQL Server-VM's (klassiek) | Microsoft Docs
description: Automatisch patchen Hallo-functie voor SQL Server virtuele Machines die worden uitgevoerd in Azure met behulp van de klassieke implementatiemodus Hallo uitgelegd.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a>Automatisch patchen voor SQL Server op Azure Virtual Machines (klassiek)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [Klassiek](../classic/sql-automated-patching.md)
> 
> 

Geautomatiseerde Patching stelt u een onderhoudsvenster voor een virtuele Machine van Azure met SQL Server. Automatische Updates kunnen alleen worden geïnstalleerd tijdens deze periode. Voor SQL Server manier op deze systeemupdates en eventuele bijbehorende opnieuw is opgestart op Hallo best mogelijke tijdstip voor Hallo-database optreden. Geautomatiseerde Patching is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. tooview hello Resource Manager-versie van dit artikel, Zie [automatisch patchen voor SQL Server in Azure Resource Manager voor virtuele Machines](../sql/virtual-machines-windows-sql-automated-patching.md).

## <a name="prerequisites"></a>Vereisten
toouse automatisch patchen, overweeg Hallo volgende vereisten:

**Besturingssysteem**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server-versie**:

* SQL Server 2012
* SQL Server 2014
* SQL Server 2016

**Azure PowerShell**:

* [Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).

**Uitbreiding van SQL Server IaaS**:

* [Hallo IaaS-uitbreiding voor SQL-Server installeren](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Instellingen
Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatisch patchen. Voor klassieke virtuele machines, moet u PowerShell tooconfigure deze instellingen.

| Instelling | Mogelijke waarden | Beschrijving |
| --- | --- | --- |
| **Automatisch patch toepassen** |In-of uitschakelen (uitgeschakeld) |Hiermee schakelt automatisch patchen voor een virtuele machine van Azure of. |
| **Onderhoudsplanning** |Dagelijks, maandag, dinsdag, woensdag, donderdag, vrijdag, zaterdag, zondag |Hallo-schema voor het downloaden en installeren van Windows, SQL Server en de Microsoft-updates voor uw virtuele machine. |
| **Beginuur van het onderhoud** |0-24 |Hallo lokale start tijd tooupdate Hallo virtuele machine. |
| **Duur van het venster Onderhoud** |30-180 |het aantal minuten Hallo toegestaan toocomplete Hallo downloaden en installeren van updates. |
| **Patch categorie** |Belangrijk |Hallo categorie van updates toodownload downloaden en installeren. |

## <a name="configuration-with-powershell"></a>Configuratie met PowerShell
In de Hallo voorbeeld te volgen, PowerShell gebruikte tooconfigure is automatisch patchen op een bestaande SQL Server-VM. Hallo **nieuw AzureVMSqlServerAutoPatchingConfig** opdracht configureert u een nieuw onderhoudsvenster voor automatische updates.

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

Op basis van dit voorbeeld, hello volgende tabel staan Hallo praktisch effect op Hallo doel-virtuele machine van Azure:

| Parameter | Effect |
| --- | --- |
| **DayOfWeek** |Patches elke donderdag geïnstalleerd. |
| **MaintenanceWindowStartingHour** |Begin updates om 11:00 uur. |
| **MaintenanceWindowsDuration** |Patches moeten worden geïnstalleerd binnen 120 minuten. Op basis van de begintijd hello, moeten ze volledig 13:00 uur. |
| **PatchCategory** |Hallo is alleen mogelijke instelling voor deze parameter 'Belangrijk'. |

Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.

toodisable automatisch patchen uitvoeren Hallo dezelfde zonder script Hallo - Enable parameter toohello nieuw AzureVMSqlServerAutoPatchingConfig. Als met de installatie, het enkele minuten toodisable duurt automatisch patchen.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

