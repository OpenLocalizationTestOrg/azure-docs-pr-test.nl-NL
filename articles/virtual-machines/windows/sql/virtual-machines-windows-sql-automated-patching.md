---
title: aaaAutomated patchen voor SQL Server-VM's (Resource Manager) | Microsoft Docs
description: Verklaart Hallo automatisch patchen functie voor SQL Server Virtual Machines worden uitgevoerd in Azure Resource Manager gebruiken.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a>Automated Patching voor SQL Server in virtuele machines van Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-automated-patching.md)
> * [Klassiek](../classic/sql-automated-patching.md)
> 
> 

Geautomatiseerde Patching stelt u een onderhoudsvenster voor een virtuele Machine van Azure met SQL Server. Automatische Updates kunnen alleen worden geïnstalleerd tijdens deze periode. Voor SQL Server zorgt deze rescriction systeemupdates en eventuele bijbehorende opnieuw is opgestart op Hallo best mogelijke tijdstip voor Hallo-database optreden. Geautomatiseerde Patching is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

tooview hello klassieke versie van dit artikel, Zie [automatisch patchen voor SQL Server in Azure virtuele Machines klassieke](../classic/sql-automated-patching.md).

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

* [Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview) als u van plan tooconfigure bent automatisch patchen met PowerShell.

> [!NOTE]
> Geautomatiseerde Patching is afhankelijk van Hallo uitbreiding voor SQL Server IaaS-Agent. Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd. Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).
> 
> 

## <a name="settings"></a>Instellingen
Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatisch patchen. de werkelijke configuratiestappen Hallo variëren afhankelijk van of u hello Azure-portal of Azure Windows PowerShell-opdrachten gebruiken.

| Instelling | Mogelijke waarden | Beschrijving |
| --- | --- | --- |
| **Automatisch patch toepassen** |In-of uitschakelen (uitgeschakeld) |Hiermee schakelt automatisch patchen voor een virtuele machine van Azure of. |
| **Onderhoudsplanning** |Dagelijks, maandag, dinsdag, woensdag, donderdag, vrijdag, zaterdag, zondag |Hallo-schema voor het downloaden en installeren van Windows, SQL Server en de Microsoft-updates voor uw virtuele machine. |
| **Beginuur van het onderhoud** |0-24 |Hallo lokale start tijd tooupdate Hallo virtuele machine. |
| **Duur van het venster Onderhoud** |30-180 |het aantal minuten Hallo toegestaan toocomplete Hallo downloaden en installeren van updates. |
| **Patch categorie** |Belangrijk |Hallo categorie van updates toodownload downloaden en installeren. |

## <a name="configuration-in-hello-portal"></a>De configuratie in Hallo Portal
U kunt hello Azure portal tooconfigure automatisch patchen tijdens het inrichten of voor een bestaande virtuele machines.

### <a name="new-vms"></a>Nieuwe virtuele machines
Gebruik hello Azure portal tooconfigure automatisch patchen wanneer u een nieuwe virtuele Machine van SQL Server in Hallo Resource Manager-implementatiemodel maakt.

In Hallo **SQL Server-instellingen** blade Selecteer **automatisch patchen**. Hallo volgende Azure portal schermafbeelding ziet u Hallo **SQL automatisch patchen** blade.

![SQL automatisch patchen in Azure-portal](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

Zie voor context is voltooid onderwerp Hallo op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Bestaande virtuele machines
Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines. Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.

![Automatisch patchen van SQL voor bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo automatische toepassing van patches sectie.

![Configureer SQL automatisch patchen voor bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.

Als u automatisch patchen voor Hallo eerst inschakelen wilt, configureert Azure Hallo SQL Server IaaS-Agent op de achtergrond Hallo. Gedurende deze tijd hello Azure-portal mogelijk niet weergegeven dat automatisch patchen is geconfigureerd. Wacht enkele minuten voor Hallo agent toobe is geïnstalleerd, geconfigureerd. Nadat de die hello Azure aangegeven portal Hallo nieuwe instellingen.

> [!NOTE]
> U kunt ook configureren met behulp van een sjabloon automatisch patchen. Zie voor meer informatie [Azure quickstart-sjabloon voor het automatisch patchen](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).
> 
> 

## <a name="configuration-with-powershell"></a>Configuratie met PowerShell
Na het inrichten van uw SQL VM Gebruik PowerShell tooconfigure automatisch patchen.

In de Hallo voorbeeld te volgen, PowerShell gebruikte tooconfigure is automatisch patchen op een bestaande SQL Server-VM. Hallo **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** opdracht configureert u een nieuw onderhoudsvenster voor automatische updates.

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

Op basis van dit voorbeeld, hello volgende tabel staan Hallo praktisch effect op Hallo doel-virtuele machine van Azure:

| Parameter | Effect |
| --- | --- |
| **DayOfWeek** |Patches elke donderdag geïnstalleerd. |
| **MaintenanceWindowStartingHour** |Begin updates om 11:00 uur. |
| **MaintenanceWindowsDuration** |Patches moeten worden geïnstalleerd binnen 120 minuten. Op basis van de begintijd hello, moeten ze volledig 13:00 uur. |
| **PatchCategory** |Hallo alleen mogelijk instellen voor deze parameter is **belangrijk**. |

Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.

toodisable automatisch patchen uitvoeren Hallo dezelfde zonder Hallo script **-inschakelen** parameter toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**. gebrek aan Hallo Hallo **-inschakelen** parameter signalen Hallo opdracht toodisable Hallo functie.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

