---
title: aaaAutomated back-up voor SQL Server Virtual Machines (klassiek) | Microsoft Docs
description: 'Verklaart Hallo automatische back-up-functie voor SQL Server wordt uitgevoerd in Azure Virtual Machines die met Resource Manager. '
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a>Automatische back-up voor SQL Server op Azure Virtual Machines (klassiek)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Klassiek](../classic/sql-automated-backup.md)
> 
> 

Automatische back-up configureert automatisch [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise. Hiermee kunt u tooconfigure reguliere databaseback-ups die gebruikmaken van duurzame Azure blob-opslag. Automatische back-up, is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. tooview hello Resource Manager-versie van dit artikel, Zie [automatische back-up voor SQL Server in Azure Resource Manager voor virtuele Machines](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a>Vereisten
toouse automatische back-up, kunt u overwegen Hallo volgende vereisten:

**Besturingssysteem**:

* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

**SQL Server-versie /-editie**:

* SQL Server 2014 Standard
* SQL Server 2014 Enterprise

> [!NOTE]
> SQL Server 2016 is nog niet ondersteund voor automatische back-up.
> 
> 

**Databaseconfiguratie**:

* Doeldatabases moeten het volledige herstelmodel hello gebruiken.

**Azure PowerShell**:

* [Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).

**Uitbreiding van SQL Server IaaS**:

* [Hallo IaaS-uitbreiding voor SQL-Server installeren](../classic/sql-server-agent-extension.md).

## <a name="settings"></a>Instellingen
Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatische back-up. Voor klassieke virtuele machines, moet u PowerShell tooconfigure deze instellingen.

| Instelling | Bereik (standaard) | Beschrijving |
| --- | --- | --- |
| **Automatische back-up** |In-of uitschakelen (uitgeschakeld) |Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise of. |
| **Bewaarperiode** |1 tot 30 dagen (30 dagen) |Hallo aantal dagen tooretain een back-up. |
| **Storage-Account** |Azure storage-account (Hallo storage-account voor Hallo virtuele machine opgegeven hebt gemaakt) |Een Azure storage-account toouse voor automatische back-up bestanden opslaan in blob-opslag. Een container is gemaakt op deze locatie toostore alle back-upbestanden. de back-upbestand Hallo naamgevingsconventie omvat Hallo datum, tijd en de machinenaam van de. |
| **Versleuteling** |In-of uitschakelen (uitgeschakeld) |Hiermee schakelt versleuteling of. Als versleuteling is ingeschakeld, Hallo certificaten Hallo back-up gebruikte toorestore bevinden zich in Hallo storage-account opgegeven in Hallo hetzelfde automaticbackup container gebruikt dezelfde naamgevingsregel Hallo. Als Hallo wachtwoord wordt gewijzigd, een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat Hallo blijft toorestore eerdere back-ups. |
| **Wachtwoord** |Wachtwoord tekst (geen) |Een wachtwoord voor versleutelingssleutels. Dit is alleen vereist als versleuteling is ingeschakeld. In volgorde toorestore een versleutelde back-up, hebt u het juiste wachtwoord Hallo en verwante certificaat dat is gebruikt tijdens het Hallo Hallo back-up is gemaakt. | **Back-upsysteem databases** | In-of uitschakelen (uitgeschakeld) | Volledige back-ups van Master, Model en MSDB duren |
| **Back-upschema configureren** | Handmatige/geautomatiseerde (geautomatiseerde) | Selecteer **automatisch** tooautomatically duren volledige en logboekback-ups op basis van het logboek groei. Selecteer **handmatige** toospecify Hallo planning voor volledige en logboekback-ups. |

## <a name="configuration-with-powershell"></a>Configuratie met PowerShell
In de Hallo PowerShell-voorbeeld te volgen, is automatische back-up geconfigureerd voor een bestaande SQL Server 2014 VM. Hallo **nieuw AzureVMSqlServerAutoBackupConfig** opdracht Hallo automatische back-up instellingen toostore back-ups in hello Azure storage-account is opgegeven door de variabele Hallo $storageaccount configureert. Deze back-ups voor 10 dagen bewaard. Hallo **Set AzureVMSqlServerExtension** opdracht updates Hallo opgegeven virtuele machine van Azure met deze instellingen.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.

tooenable versleuteling, Hallo vorige toopass hello EnableEncryption scriptparameter samen met een wachtwoord (beveiligde tekenreeks) wijzigen voor Hallo CertificatePassword-parameter. Hallo volgende script Hiermee Hallo automatische back-up-instellingen in het vorige voorbeeld Hallo en versleuteling wordt toegevoegd.

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

toodisable automatische back-up uitvoeren Hallo dezelfde zonder Hallo script **-inschakelen** parameter toohello **nieuw AzureVMSqlServerAutoBackupConfig**. Net als bij de installatie kan enkele minuten toodisable automatische back-up duren.

> [!NOTE]
> Verwijdert geen Hallo eerder geconfigureerde back-up beheerde instellingen uit te schakelen en Hallo SQL Server IaaS-Agent verwijderen. U moet automatische back-up uitschakelen voordat u het uitschakelen of verwijderen van Hallo SQL Server IaaS-Agent.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Automatische back-up configureert Managed Backup op Azure Virtual machines. Dus is het belangrijk te[Hallo-documentatie voor back-up beheerd lezen](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hallo gedrag en de gevolgen.

U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp Hallo: [back-up en herstel voor SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

