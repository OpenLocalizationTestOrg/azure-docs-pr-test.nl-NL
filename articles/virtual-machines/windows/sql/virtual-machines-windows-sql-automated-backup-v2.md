---
title: aaaAutomated back-up v2 voor SQL Server 2016 Azure Virtual Machines | Microsoft Docs
description: Verklaart Hallo automatische back-up-functie voor SQL Server 2016 virtuele machines in Azure wordt uitgevoerd. Dit artikel is een specifieke tooVMs met Hallo Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>Automatische back-v2 voor SQL Server 2016 Azure Virtual Machines (Resource Manager)

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Automatische back-up v2 configureert automatisch [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2016 Standard, Enterprise of Developer-edities. Hiermee kunt u tooconfigure reguliere databaseback-ups die gebruikmaken van duurzame Azure blob-opslag. Automatische back-up v2, is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Vereisten
toouse v2 voor automatische back-up, controleert u Hallo volgende vereisten:

**Besturingssysteem**:

- Windows Server 2012 R2
- Windows Server 2016

**SQL Server-versie /-editie**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> Automatische back-up v2 werkt met SQL Server 2016. Als u SQL Server 2014 gebruikt, kunt u automatische back-up v1 tooback van uw databases. Zie voor meer informatie [automatische back-up-voor SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

**Databaseconfiguratie**:

- Doeldatabases moeten het volledige herstelmodel hello gebruiken. Zie voor meer informatie over Hallo impact van het volledige herstelmodel Hallo op back-ups [back-up onder Hallo volledig herstelmodel](https://technet.microsoft.com/library/ms190217.aspx).
- Systeemdatabases hoeft geen toouse volledig herstelmodel. Als u logboek back-ups toobe genomen voor het Model of MSDB vereist, moet u volledig herstelmodel gebruiken.
- Doeldatabases zich op Hallo standaard SQL Server-exemplaar. Hallo IaaS-uitbreiding voor SQL Server biedt geen ondersteuning voor benoemde exemplaren.

**Azure-implementatiemodel**:

- Resource Manager

> [!NOTE]
> Automatische back-up is afhankelijk van Hallo **uitbreiding voor SQL Server IaaS-Agent**. Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd. Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Instellingen
Hallo onderstaande Hallo worden opties beschreven die kunnen worden geconfigureerd voor automatische back-up v2. de werkelijke configuratiestappen Hallo variëren afhankelijk van of u hello Azure-portal of Azure Windows PowerShell-opdrachten gebruiken.

### <a name="basic-settings"></a>Basisinstellingen

| Instelling | Bereik (standaard) | Beschrijving |
| --- | --- | --- |
| **Automatische back-up** | In-of uitschakelen (uitgeschakeld) | Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2016 Standard of Enterprise of. |
| **Bewaarperiode** | 1 tot 30 dagen (30 dagen) | Hallo aantal dagen tooretain back-ups. |
| **Storage-Account** | Azure Storage-account | Een Azure storage-account toouse voor automatische back-up bestanden opslaan in blob-opslag. Een container is gemaakt op deze locatie toostore alle back-upbestanden. de back-upbestand Hallo naamgevingsconventie omvat Hallo datum, tijd en GUID van database. |
| **Versleuteling** |In-of uitschakelen (uitgeschakeld) | Hiermee schakelt versleuteling of. Als versleuteling is ingeschakeld, Hallo certificaten gebruikt toorestore Hallo back-up bevinden zich in de opgegeven Hallo storage-account in Hallo dezelfde **automaticbackup** container met behulp van dezelfde naamgevingsregel Hallo. Als Hallo wachtwoord wordt gewijzigd, een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat Hallo blijft toorestore eerdere back-ups. |
| **Wachtwoord** |Wachtwoord tekst | Een wachtwoord voor versleutelingssleutels. Dit is alleen vereist als versleuteling is ingeschakeld. In volgorde toorestore een versleutelde back-up, hebt u het juiste wachtwoord Hallo en verwante certificaat dat is gebruikt tijdens het Hallo Hallo back-up is gemaakt. |

### <a name="advanced-settings"></a>Geavanceerde instellingen

| Instelling | Bereik (standaard) | Beschrijving |
| --- | --- | --- |
| **Back-ups van de Database** | In-of uitschakelen (uitgeschakeld) | Wanneer dit is ingeschakeld, wordt ook back-up Hallo systeemdatabases deze functie: Master, MSDB en Model. Voor Hallo MSDB en Model databases, controleert u of ze in de modus voor volledig herstel als u wilt dat logboek back-ups toobe genomen. Logboekback-ups worden nooit genomen voor Master. En er is geen back-ups worden gemaakt voor TempDB. |
| **Back-upschema** | Handmatige/geautomatiseerde (geautomatiseerde) | Standaard wordt Hallo back-upschema automatisch bepaald op basis van Hallo logboek groei. Handmatige back-upschema kunt Hallo gebruiker toospecify Hallo-tijdvenster voor back-ups. In dit geval back-ups alleen ooit duurt plaats op Hallo opgegeven frequentie en tijdens het Hallo tijdvenster van een bepaalde dag. |
| **Volledige back-upfrequentie** | Dagelijks/wekelijks | De frequentie van volledige back-ups. In beide gevallen wordt de volledige back-ups tijdens de volgende geplande tijdstip venster Hallo gestart. Wanneer u wekelijks is ingeschakeld, kunnen back-ups van meerdere dagen totdat alle databases hebt met succes back-up gemaakt omvatten. |
| **Begintijd van volledige back-up** | 00:00 – 23:00 (01:00) | Begintijd van een bepaalde dag gedurende welke volledige back-ups kunnen worden uitgevoerd. |
| **Volledige back-up tijdvenster** | 1 – 23 uur (1 uur) | De duur van het tijdvenster Hallo van een bepaalde dag gedurende welke volledige back-ups kunnen worden uitgevoerd. |
| **Back-upfrequentie logboek** | 5 – 60 minuten (60 minuten) | De frequentie van logboekback-ups. |

## <a name="understanding-full-backup-frequency"></a>Volledige back-upfrequentie begrijpen
Het is belangrijk toounderstand Hallo verschil tussen de dagelijkse en wekelijkse volledige back-ups van. In deze poging doorlopen we twee voorbeeldscenario's.

### <a name="scenario-1-weekly-backups"></a>Scenario 1: Wekelijkse back-ups
U hebt een SQL Server-VM met een aantal zeer grote databases.

Op maandag, kunt u automatische back-up v2 Hello na instellingen inschakelen:

- Back-upschema: **handmatig**
- Volledige back-upfrequentie: **wekelijks**
- Volledige back-begintijd: **01:00 uur**
- Volledige back-up tijdvenster: **1 uur**

Dit betekent dat Hallo volgende beschikbare back-upvenster dinsdag op 1 uur 1 uur. Op dat moment wordt begint automatische back-up back-ups van uw databases een tegelijk. In dit scenario zijn uw databases groot genoeg is dat de volledige back-ups voor de eerste paar databases hello wordt voltooid. Echter na één uur zijn niet alle databases Hallo back-ups.

Als dit gebeurt, begint automatische back-up een back-up Hallo resterende databases Hallo volgende dag, woensdag om 01: 00 1 uur. Als niet alle databases die back-ups zijn in die tijd, wordt geprobeerd volgende dag op Hallo opnieuw Hallo dezelfde tijd. Dit wordt voortgezet totdat alle databases is back-ups zijn.

Zodra het dinsdag opnieuw bereikt, worden automatische back-up begint back-ups van alle databases weer.

Dit scenario ziet u dat automatische back-up alleen binnen het opgegeven tijdvenster Hallo werkt en elke database, worden back-up eenmaal per week. Dit betekent ook dat het mogelijk is voor back-ups toospan meerdere dagen in Hallo case waar het is niet mogelijk toocomplete alle back-ups in één dag.

### <a name="scenario-2-daily-backups"></a>Scenario 2: Dagelijkse back-ups
U hebt een SQL Server-VM met een aantal zeer grote databases.

Op maandag, kunt u automatische back-up v2 Hello na instellingen inschakelen:

- Back-upschema: handmatige
- Volledige back-upfrequentie: per dag
- Volledige back-begintijd: 22:00
- Volledige back-up tijdvenster: 6 uur

Dit betekent dat Hallo volgende beschikbare back-upvenster maandag om 10 uur gedurende 6 uur. Op dat moment wordt begint automatische back-up back-ups van uw databases een tegelijk.

Klik vervolgens op dinsdag bij 10 gedurende 6 uur, wordt volledige back-ups van alle databases opnieuw gestart.

> [!IMPORTANT]
> Bij het plannen van dagelijkse back-ups, wordt het aanbevolen dat u een breed tijd venster tooensure die alle databases kunnen een back-up binnen deze tijd plannen. Dit is vooral belangrijk in geval van Hallo waarin u een grote hoeveelheid gegevens tooback up hebben.

## <a name="configuration-in-hello-portal"></a>De configuratie in Hallo Portal

U kunt hello Azure portal tooconfigure automatische back-up v2 gebruiken tijdens het inrichten of voor een bestaande SQL Server 2016 virtuele machines.

### <a name="new-vms"></a>Nieuwe virtuele machines

Hello Azure portal tooconfigure automatische back-up v2 gebruiken bij het maken van een nieuwe virtuele Machine van SQL Server 2016 Hallo Resource Manager-implementatiemodel. 

In Hallo **SQL Server-instellingen** blade Selecteer **automatische back-up**. Hallo volgende Azure portal schermafbeelding ziet u Hallo **SQL automatische back-up** blade.

![Configuratie SQL automatische back-up in Azure-portal](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> Automatische back-up v2 is standaard uitgeschakeld.

Zie voor context is voltooid onderwerp Hallo op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Bestaande virtuele machines

Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines. Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.

![SQL automatische back-up voor de bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo automatische back-sectie.

![SQL automatische back-up voor de bestaande virtuele machines configureren](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.

Als u automatische back-up voor Hallo eerst inschakelt, configureert Azure Hallo SQL Server IaaS-Agent op de achtergrond Hallo. Gedurende deze tijd hello Azure-portal mogelijk niet weergegeven of automatische back-up is geconfigureerd. Wacht enkele minuten voor Hallo agent toobe is geïnstalleerd, geconfigureerd. Na deze hello Azure bevatten portal Hallo nieuwe instellingen.

## <a name="configuration-with-powershell"></a>Configuratie met PowerShell

U kunt PowerShell tooconfigure automatische back-up v2 gebruiken. Voordat u begint, moet u het volgende doen:

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
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Als u de uitvoer ziet dat **inschakelen** te is ingesteld,**False**, hebt u tooenable automatische back-up. Hallo goed nieuws is dat u inschakelen en configureren van automatische back-up in Hallo dezelfde manier. Zie de volgende sectie Hallo voor deze informatie.

> [!NOTE] 
> Als u instellingen Hallo onmiddellijk na een wijziging selectievakje, is het mogelijk dat u terug Hallo oude configuratiewaarden krijgt. Wacht een paar minuten en controleer de instellingen van Hallo opnieuw toomake ervoor dat uw wijzigingen zijn toegepast.

### <a name="configure-automated-backup-v2"></a>Automatische back-v2 configureren
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

Gebruik vervolgens Hallo **nieuw AzureRmVMSqlServerAutoBackupConfig** tooenable opdracht en Hallo automatische back-up v2 instellingen toostore back-ups in hello Azure storage-account configureren. In dit voorbeeld worden back-ups Hallo ingesteld toobe 10 dagen bewaard. Back-ups van de database zijn ingeschakeld. Volledige back-ups zijn gepland voor de per week met een tijdvenster op starten om 20:00 uur gedurende 2 uur. Logboekback-ups zijn gepland voor elke 30 minuten. tweede opdracht Hallo **Set AzureRmVMSqlServerExtension**, updates Hallo opgegeven virtuele machine van Azure met deze instellingen.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren. 

tooenable versleuteling, Hallo vorige script toopass Hallo wijzigen **EnableEncryption** parameter samen met een wachtwoord (beveiligde tekenreeks) voor Hallo **CertificatePassword** parameter. Hallo volgende script Hiermee Hallo automatische back-up-instellingen in het vorige voorbeeld Hallo en versleuteling wordt toegevoegd.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

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
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Volgende stappen
Automatische back-up v2 configureert Managed Backup op Azure Virtual machines. Dus is het belangrijk te[Hallo-documentatie voor back-up beheerd lezen](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hallo gedrag en de gevolgen.

U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp Hallo: [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).

Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).

Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).

