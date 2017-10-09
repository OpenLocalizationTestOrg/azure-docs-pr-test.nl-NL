---
title: aaaAutomated back-up voor SQL Server 2014 Azure Virtual Machines | Microsoft Docs
description: Verklaart Hallo automatische back-up-functie voor SQL Server 2014 virtuele machines in Azure wordt uitgevoerd. Dit artikel is een specifieke tooVMs met Hallo Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>Automatische back-up voor virtuele Machines (Resource Manager) voor SQL Server 2014

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Automatische back-up configureert automatisch [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise. Hiermee kunt u tooconfigure reguliere databaseback-ups die gebruikmaken van duurzame Azure blob-opslag. Automatische back-up, is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Vereisten
toouse automatische back-up, kunt u overwegen Hallo volgende vereisten:

**Besturingssysteem**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**SQL Server-versie /-editie**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> Automatische back-up werkt met SQL Server 2014. Als u SQL Server 2016 gebruikt, kunt u automatische back-up v2 tooback van uw databases. Zie voor meer informatie [automatische back-up v2 voor SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).

**Databaseconfiguratie**:

- Doeldatabases moeten het volledige herstelmodel hello gebruiken. Zie voor meer informatie over Hallo impact van het volledige herstelmodel Hallo op back-ups [back-up onder Hallo volledig herstelmodel](https://technet.microsoft.com/library/ms190217.aspx).
- Doeldatabases zich op Hallo standaard SQL Server-exemplaar. Hallo IaaS-uitbreiding voor SQL Server biedt geen ondersteuning voor benoemde exemplaren.

**Azure-implementatiemodel**:

- Resource Manager

**Azure PowerShell**:

- [Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview) als u van plan tooconfigure automatische back-up met PowerShell bent.

> [!NOTE]
> Automatische back-up, is afhankelijk van Hallo uitbreiding voor SQL Server IaaS-Agent. Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd. Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Instellingen

Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatische back-up. de werkelijke configuratiestappen Hallo variëren afhankelijk van of u hello Azure-portal of Azure Windows PowerShell-opdrachten gebruiken.

| Instelling | Bereik (standaard) | Beschrijving |
| --- | --- | --- |
| **Automatische back-up** | In-of uitschakelen (uitgeschakeld) | Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise of. |
| **Bewaarperiode** | 1 tot 30 dagen (30 dagen) | Hallo aantal dagen tooretain een back-up. |
| **Storage-Account** | Azure Storage-account | Een Azure storage-account toouse voor automatische back-up bestanden opslaan in blob-opslag. Een container is gemaakt op deze locatie toostore alle back-upbestanden. de back-upbestand Hallo naamgevingsconventie omvat Hallo datum, tijd en de machinenaam van de. |
| **Versleuteling** | In-of uitschakelen (uitgeschakeld) | Hiermee schakelt versleuteling of. Als versleuteling is ingeschakeld, Hallo certificaten gebruikt toorestore Hallo back-up bevinden zich in de opgegeven Hallo storage-account in Hallo dezelfde `automaticbackup` container met behulp van dezelfde naamgevingsregel Hallo. Als Hallo wachtwoord wordt gewijzigd, een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat Hallo blijft toorestore eerdere back-ups. |
| **Wachtwoord** | Wachtwoord tekst | Een wachtwoord voor versleutelingssleutels. Dit is alleen vereist als versleuteling is ingeschakeld. In volgorde toorestore een versleutelde back-up, hebt u het juiste wachtwoord Hallo en verwante certificaat dat is gebruikt tijdens het Hallo Hallo back-up is gemaakt. |

## <a name="configuration-in-hello-portal"></a>De configuratie in Hallo Portal

U kunt hello Azure portal tooconfigure automatische back-up gebruiken tijdens het inrichten of voor een bestaande SQL Server 2014 virtuele machines.

### <a name="new-vms"></a>Nieuwe virtuele machines

Hello Azure portal tooconfigure automatische back-up gebruiken bij het maken van een nieuwe virtuele Machine van SQL Server 2014 in Hallo Resource Manager-implementatiemodel.

In Hallo **SQL Server-instellingen** blade Selecteer **automatische back-up**. Hallo volgende Azure portal schermafbeelding ziet u Hallo **SQL automatische back-up** blade.

![Configuratie SQL automatische back-up in Azure-portal](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Zie voor context is voltooid onderwerp Hallo op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Bestaande virtuele machines

Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines. Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.

![SQL automatische back-up voor de bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo automatische back-sectie.

![SQL automatische back-up voor de bestaande virtuele machines configureren](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.

Als u automatische back-up voor Hallo eerst inschakelt, configureert Azure Hallo SQL Server IaaS-Agent op de achtergrond Hallo. Gedurende deze tijd hello Azure-portal mogelijk niet weergegeven of automatische back-up is geconfigureerd. Wacht enkele minuten voor Hallo agent toobe is geïnstalleerd, geconfigureerd. Na deze hello Azure bevatten portal Hallo nieuwe instellingen.

> [!NOTE]
> U kunt ook automatische back-up-met een sjabloon configureren. Zie voor meer informatie [Azure quickstart-sjabloon voor automatische back-up](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).

## <a name="configuration-with-powershell"></a>Configuratie met PowerShell

U kunt PowerShell tooconfigure automatische back-up gebruiken. Voordat u begint, moet u het volgende doen:

- [Download en installeer Hallo nieuwste Azure PowerShell](http://aka.ms/webpi-azps).
- Open Windows PowerShell en deze koppelen aan uw account. U kunt dit doen door de stappen te volgen Hallo in Hallo [configureren van uw abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sectie Hallo onderwerp inrichten.

### <a name="install-hello-sql-iaas-extension"></a>Hallo SQL IaaS-uitbreiding installeren
Als u een virtuele machine van SQL Server uit hello Azure-portal hebt ingericht, Hallo uitbreiding van SQL Server IaaS al is geïnstalleerd. U kunt bepalen of het voor uw virtuele machine is geïnstalleerd door het aanroepen van **Get-AzureRmVM** opdracht en onderzoeken Hallo **extensies** eigenschap.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

Als Hallo uitbreiding van de SQL Server IaaS-Agent is geïnstalleerd, ziet u dat het weergegeven als 'SqlIaaSAgent' of 'SQLIaaSExtension'. **ProvisioningState** voor Hallo-uitbreiding moet ook 'Voltooid' weergegeven.

Als deze is niet geïnstalleerd of toobe ingericht mislukt, kunt u deze met de volgende opdracht Hallo installeren. Toevoeging toohello VM en de bron-groep, moet u ook opgeven Hallo regio (**$region**) waarin uw VM zich bevindt.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <a id="verifysettings"></a>Controleer of de huidige instellingen

Als u automatische back-up ingeschakeld tijdens het inrichten, kunt u PowerShell toocheck uw huidige configuratie. Voer Hallo **Get-AzureRmVMSqlServerExtension** opdracht en bekijk het Hallo **AutoBackupSettings** eigenschap:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

U moet uitvoer vergelijkbare toohello volgende krijgen:

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Als u de uitvoer ziet dat **inschakelen** te is ingesteld,**False**, hebt u tooenable automatische back-up. Hallo goed nieuws is dat u inschakelen en configureren van automatische back-up in Hallo dezelfde manier. Zie de volgende sectie Hallo voor deze informatie.

> [!NOTE] 
> Als u instellingen Hallo onmiddellijk na een wijziging selectievakje, is het mogelijk dat u terug Hallo oude configuratiewaarden krijgt. Wacht een paar minuten en controleer de instellingen van Hallo opnieuw toomake ervoor dat uw wijzigingen zijn toegepast.

### <a name="configure-automated-backup"></a>Automatische back-up configureren
U kunt PowerShell tooenable automatische back-up, evenals toomodify de configuratie en het gedrag op elk gewenst moment.

Eerst, selecteer of maak een opslagaccount voor Hallo back-upbestanden. Hallo volgende script selecteert een opslagaccount of gemaakt als deze niet bestaat.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> Automatische back-up biedt geen ondersteuning voor back-ups van opslag in premium-opslag, maar het kan duren voordat de back-ups van VM-schijven die met Premium-opslag gebruiken.

Gebruik vervolgens Hallo **nieuw AzureRmVMSqlServerAutoBackupConfig** tooenable opdracht en Hallo automatische back-up instellingen toostore back-ups in hello Azure storage-account configureren. In dit voorbeeld worden back-ups Hallo ingesteld toobe 10 dagen bewaard. tweede opdracht Hallo **Set AzureRmVMSqlServerExtension**, updates Hallo opgegeven virtuele machine van Azure met deze instellingen.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.

> [!NOTE]
> Er zijn andere instellingen voor **nieuw AzureRmVMSqlServerAutoBackupConfig** die van toepassing zijn alleen tooSQL Server 2016 en automatische back-up v2. Hallo instellingen na biedt geen ondersteuning voor SQL Server 2014: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, en **LogBackupFrequencyInMinutes**. Als u deze instellingen op een virtuele machine van SQL Server 2014 tooconfigure probeert, er is geen fout, maar komen Hallo-instellingen niet toegepast. Als u deze instellingen op een virtuele machine van SQL Server 2016 toouse wilt, Zie [automatische back-up v2 voor SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).

tooenable versleuteling, Hallo vorige script toopass Hallo wijzigen **EnableEncryption** parameter samen met een wachtwoord (beveiligde tekenreeks) voor Hallo **CertificatePassword** parameter. Hallo volgende script Hiermee Hallo automatische back-up-instellingen in het vorige voorbeeld Hallo en versleuteling wordt toegevoegd.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

uw instellingen worden toegepast, tooconfirm [Hallo automatische back-up-configuratie controleren](#verifysettings).

### <a name="disable-automated-backup"></a>Uitschakelen van automatische back-up

Automatische back-up, Voer Hallo dezelfde script zonder Hallo toodisable **-inschakelen** parameter toohello **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht. gebrek aan Hallo Hallo **-inschakelen** parameter signalen Hallo opdracht toodisable Hallo functie. Net als bij de installatie kan enkele minuten toodisable automatische back-up duren.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Voorbeeldscript

Hallo volgende script geeft een reeks variabelen tooenable aanpassen en het configureren van automatische back-up voor uw virtuele machine. In uw geval moet u wellicht toocustomize Hallo script op basis van uw vereisten. U zou bijvoorbeeld toomake wijzigingen hebben als u deze toodisable Hallo back-up van de systeemdatabases wilde of versleuteling inschakelen.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Volgende stappen

Automatische back-up configureert Managed Backup op Azure Virtual machines. Dus is het belangrijk te[Hallo-documentatie voor back-up beheerd lezen](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hallo gedrag en de gevolgen.

U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp Hallo: [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

