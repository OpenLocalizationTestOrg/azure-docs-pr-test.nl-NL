---
title: Back-up langdurig bewaren - Azure SQL-database configureren | Microsoft Docs
description: Meer informatie over hoe toostore automatische back-ups in hello Azure Recovery Services-kluis en toorestore van hello die Azure Recovery Services-kluis
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: carlrab
ms.openlocfilehash: 603f4dd21cee4407d46f749655aba8f9ef3322c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a>En terugzetten van back-up op lange termijn bewaren van Azure SQL Database configureren

U kunt hello Azure Recovery Services-kluis toostore Azure SQL database back-ups configureren en vervolgens herstellen in een database met behulp van back-ups behouden bij het gebruik van de kluis Hallo hello Azure-portal of PowerShell.

## <a name="azure-portal"></a>Azure Portal

Hallo secties tonen u hoe toouse hello Azure portal tooconfigure hello Azure Recovery Services-kluis, back-ups weergeven in de kluis Hallo en herstel van Hallo kluis te volgen.

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a>Hallo kluis configureren, Hallo-server registreren en databases selecteren

U [configureren van een back-ups van Azure Recovery Services-kluis tooretain geautomatiseerde](sql-database-long-term-retention.md) gedurende een periode langer is dan de bewaarperiode Hallo voor uw servicetier. 

1. Open Hallo **SQL Server** pagina voor uw server.

   ![pagina met SQL server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. Klik op **Langetermijnretentie**.

   ![koppeling langetermijnretentie](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. Op Hallo **lange bewaartermijn van de back-** pagina voor uw server, lees en accepteer Hallo preview-voorwaarden (tenzij u hebben gedaan - of deze functie niet langer in preview is).

   ![Hallo preview-voorwaarden accepteren](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. tooconfigure op lange termijn back-retentie, dat de database in Hallo raster selecteren en klik vervolgens op **configureren** op Hallo-werkbalk.

   ![database selecteren voor langetermijnretentie](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. Op Hallo **configureren** pagina, klikt u op **vereiste instellingen configureren** onder **Recovery-kluis service**.

   ![koppeling kluis](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. Op Hallo **Recovery services-kluis** pagina, selecteert u een bestaande kluis, indien van toepassing. Als geen recovery services-kluis gevonden voor uw abonnement, klikt u op tooexit Hallo stroom en een recovery services-kluis maken.

   ![koppeling van de kluis maken](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. Op Hallo **Recovery Services-kluizen** pagina, klikt u op **toevoegen**.

   ![kluis koppeling toevoegen](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. Op Hallo **Recovery Services-kluis** pagina, Geef een geldige naam voor Hallo Recovery Services-kluis.

   ![naam nieuwe kluis](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. Selecteer uw abonnement en resourcegroep en selecteer vervolgens Hallo-locatie voor Hallo kluis. Klik op **Maken** als u klaar bent.

   ![Kluis maken](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > Hallo kluis moet zich bevinden in dezelfde regio bevinden als de logische Azure SQL-server Hallo Hallo en gebruik moet Hallo dezelfde resourcegroep als Hallo logische server.
   >

10. Nadat de nieuwe kluis Hallo is gemaakt, uitvoeren Hallo nodige tooreturn toohello **Recovery services-kluis** pagina.

11. Op Hallo **Recovery services-kluis** pagina, klikt u op Hallo kluis en klik op **Selecteer**.

   ![bestaande kluis selecteren](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. Op Hallo **configureren** pagina, Geef een geldige naam voor een nieuw bewaarbeleid Hallo Hallo standaard bewaarbeleid desgewenst wijzigen en klik vervolgens op **OK**.

   ![retentiebeleid definiëren](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. Op Hallo **lange bewaartermijn van de back-** pagina voor uw database, klikt u op **opslaan** en klik vervolgens op **OK** tooapply Hallo op lange termijn bewaren van back-beleid tooall geselecteerd databases.

   ![retentiebeleid definiëren](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. Klik op **opslaan** back-up langdurig bewaren van tooenable worden met dit nieuwe beleid toohello Azure Recovery Services-kluis maken die u hebt geconfigureerd.

   ![retentiebeleid definiëren](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> Na de configuratie weergegeven back-ups in Hallo kluis binnen de komende 7 dagen. Deze zelfstudie niet doorgaat totdat back-ups in het Hallo-kluis weergegeven.
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a>Back-ups weergeven in lange bewaartermijn met Azure portal

Informatie weergeven over uw databaseback-ups in [lange bewaartermijn van de back-](sql-database-long-term-retention.md). 

1. In Azure-portal hello, opent u de Azure Recovery Services-kluis voor back-ups van uw database (Ga te**alle resources** en selecteren in lijst van resources voor uw abonnement Hallo) tooview Hallo hoeveelheid opslag van uw database back-ups in Hallo kluis.

   ![recovery services-kluis weergeven met back-ups](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. Open Hallo **SQL-database** pagina voor uw database.

   ![nieuwe db voorbeeldpagina](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. Op de werkbalk Hallo **herstellen**.

   ![werkbalk herstellen](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. Op de pagina Hallo terugzetten op **op lange termijn**.

5. Back-ups van Azure-kluis, klik op **selecteert u een back-up** tooview Hallo beschikbaar databaseback-ups in lange bewaartermijn van de back-up.

   ![back-ups in kluis](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a>Een database herstellen vanaf een back-up in lange back-up bewaartermijn met hello Azure-portal

U terugzetten Hallo database tooa nieuwe database vanuit een back-up in hello die Azure Recovery Services-kluis.

1. Op Hallo **Azure kluis back-ups** pagina, klikt u op de back-toorestore hello en klik vervolgens op **Selecteer**.

   ![back-up in kluis selecteren](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. In Hallo **databasenaam** tekst hello naam voor de database hersteld Hallo Geef.

   ![nieuwe databasenaam](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. Klik op **OK** toorestore uw database vanuit back-up van Hallo in Hallo kluis toohello nieuwe database.

4. Klik op Hallo melding pictogram tooview Hallo status van de hersteltaak Hallo op Hallo-werkbalk.

   ![taakvoortgang herstellen vanuit kluis](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. Hallo hersteltaak is voltooid, opent u Hallo **SQL-databases** pagina tooview Hallo zojuist hersteld database.

   ![uit kluis herstelde database](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> Hier kunt u verbinding maakt toohello hersteld database met behulp van SQL Server Management Studio tooperform nodig taken, zoals te[een stukje gegevens ophalen uit Hallo hersteld database toocopy in de bestaande database Hallo of toodelete Hallo bestaande database- en wijzig de naam van Hallo hersteld database toohello bestaande databasenaam](sql-database-recovery-using-backups.md#point-in-time-restore).
>

## <a name="powershell"></a>PowerShell

Hallo volgende secties ziet u hoe toouse PowerShell tooconfigure hello Azure Recovery Services-kluis back-ups weergeven in de kluis Hallo en herstel van Hallo kluis.

### <a name="create-a-recovery-services-vault"></a>Een Recovery Services-kluis maken

Gebruik Hallo [nieuw AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate een recovery services-kluis.

> [!IMPORTANT]
> Hallo kluis moet zich bevinden in dezelfde regio bevinden als de logische Azure SQL-server Hallo Hallo en gebruik moet Hallo dezelfde resourcegroep als Hallo logische server.

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a>Instellen van uw server toouse Hallo recovery-kluis voor de lange termijn bewaren van back-ups

Gebruik Hallo [Set AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate een eerder gemaakte recovery services-kluis met een specifieke Azure SQL-server.

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a>Retentiebeleid maken

Een bewaarbeleid is waarin u tookeep hoe lang een databaseback-up instellen. Gebruik Hallo [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget Hallo standaard bewaren beleid toouse als Hallo-sjabloon voor het maken van beleid. In deze sjabloon is Hallo bewaarperiode ingesteld voor 2 jaar. Voer vervolgens Hallo [nieuw AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Hallo-beleid maken. 

> [!NOTE]
> Sommige cmdlets vereisen Hallo kluis context voordat u in te stellen ([Set AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) zodat u deze cmdlet in enkele verwante codefragmenten zien. U instellen Hallo context omdat Hallo beleid deel uit van Hallo kluis maakt. U kunt meerdere bewaarbeleid voor elke kluis maken en vervolgens toepassen Hallo gewenst beleid toospecific databases. 


```PowerShell
# Retrieve hello default retention policy for hello AzureSQLDatabase workload type
$retentionPolicy = Get-AzureRmRecoveryServicesBackupRetentionPolicyObject -WorkloadType AzureSQLDatabase

# Set hello retention value tootwo years (you can set tooany time between 1 week and 10 years)
$retentionPolicy.RetentionDurationType = "Years"
$retentionPolicy.RetentionCount = 2
$retentionPolicyName = "my2YearRetentionPolicy"

# Set hello vault context toohello vault you are creating hello policy for
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# Create hello new policy
$policy = New-AzureRmRecoveryServicesBackupProtectionPolicy -name $retentionPolicyName -WorkloadType AzureSQLDatabase -retentionPolicy $retentionPolicy
$policy
```

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a>Een bewaarbeleid database toouse Hallo eerder gedefinieerd configureren

Gebruik Hallo [Set AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply Hallo nieuwe beleid tooa specifieke database.

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a>Back-upinformatie en back-ups met langetermijnretentie weergeven

Informatie weergeven over uw databaseback-ups in [lange bewaartermijn van de back-](sql-database-long-term-retention.md). 

Gebruik Hallo cmdlets tooview back-upgegevens te volgen:

- [Get-AzureRmRecoveryServicesBackupContainer](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [Get-AzureRmRecoveryServicesBackupItem](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [Get-AzureRmRecoveryServicesBackupRecoveryPoint](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

```PowerShell
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$databaseNeedingRestore = $databaseName

# Set hello vault context toohello vault we want toorestore from
#$vault = Get-AzureRmRecoveryServicesVault -ResourceGroupName $resourceGroupName
Set-AzureRmRecoveryServicesVaultContext -Vault $vault

# hello following commands find hello container associated with hello server 'myserver' under resource group 'myresourcegroup'
$container = Get-AzureRmRecoveryServicesBackupContainer -ContainerType AzureSQL -FriendlyName $vault.Name

# Get hello long-term retention metadata associated with a specific database
$item = Get-AzureRmRecoveryServicesBackupItem -Container $container -WorkloadType AzureSQLDatabase -Name $databaseNeedingRestore

# Get all available backups for hello previously indicated database
# Optionally, set hello -StartDate and -EndDate parameters tooreturn backups within a specific time period
$availableBackups = Get-AzureRmRecoveryServicesBackupRecoveryPoint -Item $item
$availableBackups
```

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a>Een database herstellen vanuit een back-up met langetermijnretentie

Hallo terugzetten vanaf een lange bewaartermijn van de back-up gebruikt [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.

```PowerShell
# Restore hello most recent backup: $availableBackups[0]
#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$restoredDatabaseName = "{new-database-name}"
$edition = "Basic"
$performanceLevel = "Basic"

$restoredDb = Restore-AzureRmSqlDatabase -FromLongTermRetentionBackup -ResourceId $availableBackups[0].Id -ResourceGroupName $resourceGroupName `
 -ServerName $serverName -TargetDatabaseName $restoredDatabaseName -Edition $edition -ServiceObjectiveName $performanceLevel
$restoredDb
```


> [!NOTE]
> Hier kunt u verbinding kunt maken met toohello hersteld database met behulp van SQL Server Management Studio tooperform nodig taken, zoals tooextract een bits van gegevens van Hallo database toocopy teruggezet naar de bestaande database Hallo of toodelete Hallo bestaande database en wijzig de naam Hallo herstelde database toohello bestaande databasenaam. Zie [punt in tijd terugzetten](sql-database-recovery-using-backups.md#point-in-time-restore).

## <a name="next-steps"></a>Volgende stappen

- toolearn over service gegenereerde automatische back-ups, Zie [automatische back-ups](sql-database-automated-backups.md)
- toolearn over het bewaren van back-up op lange termijn, Zie [lange bewaartermijn van de back-up](sql-database-long-term-retention.md)
- toolearn over het terugzetten van back-ups, Zie [back-up terugzetten](sql-database-recovery-using-backups.md)
