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
# <a name="configure-and-restore-from-azure-sql-database-long-term-backup-retention"></a><span data-ttu-id="c73c1-103">En terugzetten van back-up op lange termijn bewaren van Azure SQL Database configureren</span><span class="sxs-lookup"><span data-stu-id="c73c1-103">Configure and restore from Azure SQL Database long-term backup retention</span></span>

<span data-ttu-id="c73c1-104">U kunt hello Azure Recovery Services-kluis toostore Azure SQL database back-ups configureren en vervolgens herstellen in een database met behulp van back-ups behouden bij het gebruik van de kluis Hallo hello Azure-portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c73c1-104">You can configure hello Azure Recovery Services vault toostore Azure SQL database backups and then recover a database using backups retained in hello vault using hello Azure portal or PowerShell.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="c73c1-105">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c73c1-105">Azure portal</span></span>

<span data-ttu-id="c73c1-106">Hallo secties tonen u hoe toouse hello Azure portal tooconfigure hello Azure Recovery Services-kluis, back-ups weergeven in de kluis Hallo en herstel van Hallo kluis te volgen.</span><span class="sxs-lookup"><span data-stu-id="c73c1-106">hello following sections show you how toouse hello Azure portal tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="configure-hello-vault-register-hello-server-and-select-databases"></a><span data-ttu-id="c73c1-107">Hallo kluis configureren, Hallo-server registreren en databases selecteren</span><span class="sxs-lookup"><span data-stu-id="c73c1-107">Configure hello vault, register hello server, and select databases</span></span>

<span data-ttu-id="c73c1-108">U [configureren van een back-ups van Azure Recovery Services-kluis tooretain geautomatiseerde](sql-database-long-term-retention.md) gedurende een periode langer is dan de bewaarperiode Hallo voor uw servicetier.</span><span class="sxs-lookup"><span data-stu-id="c73c1-108">You [configure an Azure Recovery Services vault tooretain automated backups](sql-database-long-term-retention.md) for a period longer than hello retention period for your service tier.</span></span> 

1. <span data-ttu-id="c73c1-109">Open Hallo **SQL Server** pagina voor uw server.</span><span class="sxs-lookup"><span data-stu-id="c73c1-109">Open hello **SQL Server** page for your server.</span></span>

   ![pagina met SQL server](./media/sql-database-get-started-portal/sql-server-blade.png)

2. <span data-ttu-id="c73c1-111">Klik op **Langetermijnretentie**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-111">Click **Long-term backup retention**.</span></span>

   ![koppeling langetermijnretentie](./media/sql-database-get-started-backup-recovery/long-term-backup-retention-link.png)

3. <span data-ttu-id="c73c1-113">Op Hallo **lange bewaartermijn van de back-** pagina voor uw server, lees en accepteer Hallo preview-voorwaarden (tenzij u hebben gedaan - of deze functie niet langer in preview is).</span><span class="sxs-lookup"><span data-stu-id="c73c1-113">On hello **Long-term backup retention** page for your server, review and accept hello preview terms (unless you have already done so - or this feature is no longer in preview).</span></span>

   ![Hallo preview-voorwaarden accepteren](./media/sql-database-get-started-backup-recovery/accept-the-preview-terms.png)

4. <span data-ttu-id="c73c1-115">tooconfigure op lange termijn back-retentie, dat de database in Hallo raster selecteren en klik vervolgens op **configureren** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="c73c1-115">tooconfigure long-term backup retention, select that database in hello grid and then click **Configure** on hello toolbar.</span></span>

   ![database selecteren voor langetermijnretentie](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

5. <span data-ttu-id="c73c1-117">Op Hallo **configureren** pagina, klikt u op **vereiste instellingen configureren** onder **Recovery-kluis service**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-117">On hello **Configure** page, click **Configure required settings** under **Recovery service vault**.</span></span>

   ![koppeling kluis](./media/sql-database-get-started-backup-recovery/configure-vault-link.png)

6. <span data-ttu-id="c73c1-119">Op Hallo **Recovery services-kluis** pagina, selecteert u een bestaande kluis, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="c73c1-119">On hello **Recovery services vault** page, select an existing vault, if any.</span></span> <span data-ttu-id="c73c1-120">Als geen recovery services-kluis gevonden voor uw abonnement, klikt u op tooexit Hallo stroom en een recovery services-kluis maken.</span><span class="sxs-lookup"><span data-stu-id="c73c1-120">Otherwise, if no recovery services vault found for your subscription, click tooexit hello flow and create a recovery services vault.</span></span>

   ![koppeling van de kluis maken](./media/sql-database-get-started-backup-recovery/create-new-vault-link.png)

7. <span data-ttu-id="c73c1-122">Op Hallo **Recovery Services-kluizen** pagina, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-122">On hello **Recovery Services vaults** page, click **Add**.</span></span>

   ![kluis koppeling toevoegen](./media/sql-database-get-started-backup-recovery/add-new-vault-link.png)
   
8. <span data-ttu-id="c73c1-124">Op Hallo **Recovery Services-kluis** pagina, Geef een geldige naam voor Hallo Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="c73c1-124">On hello **Recovery Services vault** page, provide a valid name for hello Recovery Services vault.</span></span>

   ![naam nieuwe kluis](./media/sql-database-get-started-backup-recovery/new-vault-name.png)

9. <span data-ttu-id="c73c1-126">Selecteer uw abonnement en resourcegroep en selecteer vervolgens Hallo-locatie voor Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="c73c1-126">Select your subscription and resource group, and then select hello location for hello vault.</span></span> <span data-ttu-id="c73c1-127">Klik op **Maken** als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="c73c1-127">When done, click **Create**.</span></span>

   ![Kluis maken](./media/sql-database-get-started-backup-recovery/create-new-vault.png)

   > [!IMPORTANT]
   > <span data-ttu-id="c73c1-129">Hallo kluis moet zich bevinden in dezelfde regio bevinden als de logische Azure SQL-server Hallo Hallo en gebruik moet Hallo dezelfde resourcegroep als Hallo logische server.</span><span class="sxs-lookup"><span data-stu-id="c73c1-129">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>
   >

10. <span data-ttu-id="c73c1-130">Nadat de nieuwe kluis Hallo is gemaakt, uitvoeren Hallo nodige tooreturn toohello **Recovery services-kluis** pagina.</span><span class="sxs-lookup"><span data-stu-id="c73c1-130">After hello new vault is created, execute hello necessary steps tooreturn toohello **Recovery services vault** page.</span></span>

11. <span data-ttu-id="c73c1-131">Op Hallo **Recovery services-kluis** pagina, klikt u op Hallo kluis en klik op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-131">On hello **Recovery services vault** page, click hello vault and then click **Select**.</span></span>

   ![bestaande kluis selecteren](./media/sql-database-get-started-backup-recovery/select-existing-vault.png)

12. <span data-ttu-id="c73c1-133">Op Hallo **configureren** pagina, Geef een geldige naam voor een nieuw bewaarbeleid Hallo Hallo standaard bewaarbeleid desgewenst wijzigen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-133">On hello **Configure** page, provide a valid name for hello new retention policy, modify hello default retention policy as appropriate, and then click **OK**.</span></span>

   ![retentiebeleid definiëren](./media/sql-database-get-started-backup-recovery/define-retention-policy.png)

13. <span data-ttu-id="c73c1-135">Op Hallo **lange bewaartermijn van de back-** pagina voor uw database, klikt u op **opslaan** en klik vervolgens op **OK** tooapply Hallo op lange termijn bewaren van back-beleid tooall geselecteerd databases.</span><span class="sxs-lookup"><span data-stu-id="c73c1-135">On hello **Long-term backup retention** page for your database, click **Save** and then click **OK** tooapply hello long-term backup retention policy tooall selected databases.</span></span>

   ![retentiebeleid definiëren](./media/sql-database-get-started-backup-recovery/save-retention-policy.png)

14. <span data-ttu-id="c73c1-137">Klik op **opslaan** back-up langdurig bewaren van tooenable worden met dit nieuwe beleid toohello Azure Recovery Services-kluis maken die u hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c73c1-137">Click **Save** tooenable long-term backup retention using this new policy toohello Azure Recovery Services vault that you configured.</span></span>

   ![retentiebeleid definiëren](./media/sql-database-get-started-backup-recovery/enable-long-term-retention.png)

> [!IMPORTANT]
> <span data-ttu-id="c73c1-139">Na de configuratie weergegeven back-ups in Hallo kluis binnen de komende 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="c73c1-139">Once configured, backups show up in hello vault within next seven days.</span></span> <span data-ttu-id="c73c1-140">Deze zelfstudie niet doorgaat totdat back-ups in het Hallo-kluis weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c73c1-140">Do not continue this tutorial until backups show up in hello vault.</span></span>
>

### <a name="view-backups-in-long-term-retention-using-azure-portal"></a><span data-ttu-id="c73c1-141">Back-ups weergeven in lange bewaartermijn met Azure portal</span><span class="sxs-lookup"><span data-stu-id="c73c1-141">View backups in long-term retention using Azure portal</span></span>

<span data-ttu-id="c73c1-142">Informatie weergeven over uw databaseback-ups in [lange bewaartermijn van de back-](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c73c1-142">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

1. <span data-ttu-id="c73c1-143">In Azure-portal hello, opent u de Azure Recovery Services-kluis voor back-ups van uw database (Ga te**alle resources** en selecteren in lijst van resources voor uw abonnement Hallo) tooview Hallo hoeveelheid opslag van uw database back-ups in Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="c73c1-143">In hello Azure portal, open your Azure Recovery Services vault for your database backups (go too**All resources** and select it from hello list of resources for your subscription) tooview hello amount of storage used by your database backups in hello vault.</span></span>

   ![recovery services-kluis weergeven met back-ups](./media/sql-database-get-started-backup-recovery/view-recovery-services-vault-with-data.png)

2. <span data-ttu-id="c73c1-145">Open Hallo **SQL-database** pagina voor uw database.</span><span class="sxs-lookup"><span data-stu-id="c73c1-145">Open hello **SQL database** page for your database.</span></span>

   ![nieuwe db voorbeeldpagina](./media/sql-database-get-started-portal/new-sample-db-blade.png)

3. <span data-ttu-id="c73c1-147">Op de werkbalk Hallo **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-147">On hello toolbar, click **Restore**.</span></span>

   ![werkbalk herstellen](./media/sql-database-get-started-backup-recovery/restore-toolbar.png)

4. <span data-ttu-id="c73c1-149">Op de pagina Hallo terugzetten op **op lange termijn**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-149">On hello Restore page, click **Long-term**.</span></span>

5. <span data-ttu-id="c73c1-150">Back-ups van Azure-kluis, klik op **selecteert u een back-up** tooview Hallo beschikbaar databaseback-ups in lange bewaartermijn van de back-up.</span><span class="sxs-lookup"><span data-stu-id="c73c1-150">Under Azure vault backups, click **Select a backup** tooview hello available database backups in long-term backup retention.</span></span>

   ![back-ups in kluis](./media/sql-database-get-started-backup-recovery/view-backups-in-vault.png)

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention-using-hello-azure-portal"></a><span data-ttu-id="c73c1-152">Een database herstellen vanaf een back-up in lange back-up bewaartermijn met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="c73c1-152">Restore a database from a backup in long-term backup retention using hello Azure portal</span></span>

<span data-ttu-id="c73c1-153">U terugzetten Hallo database tooa nieuwe database vanuit een back-up in hello die Azure Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="c73c1-153">You restore hello database tooa new database from a backup in hello Azure Recovery Services vault.</span></span>

1. <span data-ttu-id="c73c1-154">Op Hallo **Azure kluis back-ups** pagina, klikt u op de back-toorestore hello en klik vervolgens op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="c73c1-154">On hello **Azure vault backups** page, click hello backup toorestore and then click **Select**.</span></span>

   ![back-up in kluis selecteren](./media/sql-database-get-started-backup-recovery/select-backup-in-vault.png)

2. <span data-ttu-id="c73c1-156">In Hallo **databasenaam** tekst hello naam voor de database hersteld Hallo Geef.</span><span class="sxs-lookup"><span data-stu-id="c73c1-156">In hello **Database name** text box, provide hello name for hello restored database.</span></span>

   ![nieuwe databasenaam](./media/sql-database-get-started-backup-recovery/new-database-name.png)

3. <span data-ttu-id="c73c1-158">Klik op **OK** toorestore uw database vanuit back-up van Hallo in Hallo kluis toohello nieuwe database.</span><span class="sxs-lookup"><span data-stu-id="c73c1-158">Click **OK** toorestore your database from hello backup in hello vault toohello new database.</span></span>

4. <span data-ttu-id="c73c1-159">Klik op Hallo melding pictogram tooview Hallo status van de hersteltaak Hallo op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="c73c1-159">On hello toolbar, click hello notification icon tooview hello status of hello restore job.</span></span>

   ![taakvoortgang herstellen vanuit kluis](./media/sql-database-get-started-backup-recovery/restore-job-progress-long-term.png)

5. <span data-ttu-id="c73c1-161">Hallo hersteltaak is voltooid, opent u Hallo **SQL-databases** pagina tooview Hallo zojuist hersteld database.</span><span class="sxs-lookup"><span data-stu-id="c73c1-161">When hello restore job is completed, open hello **SQL databases** page tooview hello newly restored database.</span></span>

   ![uit kluis herstelde database](./media/sql-database-get-started-backup-recovery/restored-database-from-vault.png)

> [!NOTE]
> <span data-ttu-id="c73c1-163">Hier kunt u verbinding maakt toohello hersteld database met behulp van SQL Server Management Studio tooperform nodig taken, zoals te[een stukje gegevens ophalen uit Hallo hersteld database toocopy in de bestaande database Hallo of toodelete Hallo bestaande database- en wijzig de naam van Hallo hersteld database toohello bestaande databasenaam](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="c73c1-163">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as too[extract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>
>

## <a name="powershell"></a><span data-ttu-id="c73c1-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c73c1-164">PowerShell</span></span>

<span data-ttu-id="c73c1-165">Hallo volgende secties ziet u hoe toouse PowerShell tooconfigure hello Azure Recovery Services-kluis back-ups weergeven in de kluis Hallo en herstel van Hallo kluis.</span><span class="sxs-lookup"><span data-stu-id="c73c1-165">hello following sections show you how toouse PowerShell tooconfigure hello Azure Recovery Services vault, view backups in hello vault, and restore from hello vault.</span></span>

### <a name="create-a-recovery-services-vault"></a><span data-ttu-id="c73c1-166">Een Recovery Services-kluis maken</span><span class="sxs-lookup"><span data-stu-id="c73c1-166">Create a recovery services vault</span></span>

<span data-ttu-id="c73c1-167">Gebruik Hallo [nieuw AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate een recovery services-kluis.</span><span class="sxs-lookup"><span data-stu-id="c73c1-167">Use hello [New-AzureRmRecoveryServicesVault](/powershell/module/azurerm.recoveryservices/new-azurermrecoveryservicesvault) toocreate a recovery services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c73c1-168">Hallo kluis moet zich bevinden in dezelfde regio bevinden als de logische Azure SQL-server Hallo Hallo en gebruik moet Hallo dezelfde resourcegroep als Hallo logische server.</span><span class="sxs-lookup"><span data-stu-id="c73c1-168">hello vault must be located in hello same region as hello Azure SQL logical server, and must use hello same resource group as hello logical server.</span></span>

```PowerShell
# Create a recovery services vault

#$resourceGroupName = "{resource-group-name}"
#$serverName = "{server-name}"
$serverLocation = (Get-AzureRmSqlServer -ServerName $serverName -ResourceGroupName $resourceGroupName).Location
$recoveryServiceVaultName = "{new-vault-name}"

$vault = New-AzureRmRecoveryServicesVault -Name $recoveryServiceVaultName -ResourceGroupName $ResourceGroupName -Location $serverLocation 
Set-AzureRmRecoveryServicesBackupProperties -BackupStorageRedundancy LocallyRedundant -Vault $vault
```

### <a name="set-your-server-toouse-hello-recovery-vault-for-its-long-term-retention-backups"></a><span data-ttu-id="c73c1-169">Instellen van uw server toouse Hallo recovery-kluis voor de lange termijn bewaren van back-ups</span><span class="sxs-lookup"><span data-stu-id="c73c1-169">Set your server toouse hello recovery vault for its long-term retention backups</span></span>

<span data-ttu-id="c73c1-170">Gebruik Hallo [Set AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate een eerder gemaakte recovery services-kluis met een specifieke Azure SQL-server.</span><span class="sxs-lookup"><span data-stu-id="c73c1-170">Use hello [Set-AzureRmSqlServerBackupLongTermRetentionVault](/powershell/module/azurerm.sql/set-azurermsqlserverbackuplongtermretentionvault) cmdlet tooassociate a previously created recovery services vault with a specific Azure SQL server.</span></span>

```PowerShell
# Set your server toouse hello vault toofor long-term backup retention 

Set-AzureRmSqlServerBackupLongTermRetentionVault -ResourceGroupName $resourceGroupName -ServerName $serverName -ResourceId $vault.Id
```

### <a name="create-a-retention-policy"></a><span data-ttu-id="c73c1-171">Retentiebeleid maken</span><span class="sxs-lookup"><span data-stu-id="c73c1-171">Create a retention policy</span></span>

<span data-ttu-id="c73c1-172">Een bewaarbeleid is waarin u tookeep hoe lang een databaseback-up instellen.</span><span class="sxs-lookup"><span data-stu-id="c73c1-172">A retention policy is where you set how long tookeep a database backup.</span></span> <span data-ttu-id="c73c1-173">Gebruik Hallo [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget Hallo standaard bewaren beleid toouse als Hallo-sjabloon voor het maken van beleid.</span><span class="sxs-lookup"><span data-stu-id="c73c1-173">Use hello [Get-AzureRmRecoveryServicesBackupRetentionPolicyObject](https://docs.microsoft.com/powershell/resourcemanager/azurerm.recoveryservices.backup/v2.3.0/get-azurermrecoveryservicesbackupretentionpolicyobject) cmdlet tooget hello default retention policy toouse as hello template for creating policies.</span></span> <span data-ttu-id="c73c1-174">In deze sjabloon is Hallo bewaarperiode ingesteld voor 2 jaar.</span><span class="sxs-lookup"><span data-stu-id="c73c1-174">In this template, hello retention period is set for 2 years.</span></span> <span data-ttu-id="c73c1-175">Voer vervolgens Hallo [nieuw AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally Hallo-beleid maken.</span><span class="sxs-lookup"><span data-stu-id="c73c1-175">Next, run hello [New-AzureRmRecoveryServicesBackupProtectionPolicy](/powershell/module/azurerm.recoveryservices.backup/new-azurermrecoveryservicesbackupprotectionpolicy) toofinally create hello policy.</span></span> 

> [!NOTE]
> <span data-ttu-id="c73c1-176">Sommige cmdlets vereisen Hallo kluis context voordat u in te stellen ([Set AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) zodat u deze cmdlet in enkele verwante codefragmenten zien.</span><span class="sxs-lookup"><span data-stu-id="c73c1-176">Some cmdlets require that you set hello vault context before running ([Set-AzureRmRecoveryServicesVaultContext](/powershell/module/azurerm.recoveryservices/set-azurermrecoveryservicesvaultcontext)) so you see this cmdlet in a few related snippets.</span></span> <span data-ttu-id="c73c1-177">U instellen Hallo context omdat Hallo beleid deel uit van Hallo kluis maakt.</span><span class="sxs-lookup"><span data-stu-id="c73c1-177">You set hello context because hello policy is part of hello vault.</span></span> <span data-ttu-id="c73c1-178">U kunt meerdere bewaarbeleid voor elke kluis maken en vervolgens toepassen Hallo gewenst beleid toospecific databases.</span><span class="sxs-lookup"><span data-stu-id="c73c1-178">You can create multiple retention policies for each vault and then apply hello desired policy toospecific databases.</span></span> 


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

### <a name="configure-a-database-toouse-hello-previously-defined-retention-policy"></a><span data-ttu-id="c73c1-179">Een bewaarbeleid database toouse Hallo eerder gedefinieerd configureren</span><span class="sxs-lookup"><span data-stu-id="c73c1-179">Configure a database toouse hello previously defined retention policy</span></span>

<span data-ttu-id="c73c1-180">Gebruik Hallo [Set AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply Hallo nieuwe beleid tooa specifieke database.</span><span class="sxs-lookup"><span data-stu-id="c73c1-180">Use hello [Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasebackuplongtermretentionpolicy) cmdlet tooapply hello new policy tooa specific database.</span></span>

```PowerShell
# Enable long-term retention for a specific SQL database
$policyState = "enabled"
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -State $policyState -ResourceId $policy.Id
```

### <a name="view-backup-info-and-backups-in-long-term-retention"></a><span data-ttu-id="c73c1-181">Back-upinformatie en back-ups met langetermijnretentie weergeven</span><span class="sxs-lookup"><span data-stu-id="c73c1-181">View backup info, and backups in long-term retention</span></span>

<span data-ttu-id="c73c1-182">Informatie weergeven over uw databaseback-ups in [lange bewaartermijn van de back-](sql-database-long-term-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c73c1-182">View information about your database backups in [long-term backup retention](sql-database-long-term-retention.md).</span></span> 

<span data-ttu-id="c73c1-183">Gebruik Hallo cmdlets tooview back-upgegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="c73c1-183">Use hello following cmdlets tooview backup information:</span></span>

- [<span data-ttu-id="c73c1-184">Get-AzureRmRecoveryServicesBackupContainer</span><span class="sxs-lookup"><span data-stu-id="c73c1-184">Get-AzureRmRecoveryServicesBackupContainer</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupcontainer)
- [<span data-ttu-id="c73c1-185">Get-AzureRmRecoveryServicesBackupItem</span><span class="sxs-lookup"><span data-stu-id="c73c1-185">Get-AzureRmRecoveryServicesBackupItem</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackupitem)
- [<span data-ttu-id="c73c1-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="c73c1-186">Get-AzureRmRecoveryServicesBackupRecoveryPoint</span></span>](/powershell/module/azurerm.recoveryservices.backup/get-azurermrecoveryservicesbackuprecoverypoint)

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

### <a name="restore-a-database-from-a-backup-in-long-term-backup-retention"></a><span data-ttu-id="c73c1-187">Een database herstellen vanuit een back-up met langetermijnretentie</span><span class="sxs-lookup"><span data-stu-id="c73c1-187">Restore a database from a backup in long-term backup retention</span></span>

<span data-ttu-id="c73c1-188">Hallo terugzetten vanaf een lange bewaartermijn van de back-up gebruikt [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c73c1-188">Restoring from long-term backup retention uses hello [Restore-AzureRmSqlDatabase](/powershell/module/azurerm.sql/restore-azurermsqldatabase) cmdlet.</span></span>

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
> <span data-ttu-id="c73c1-189">Hier kunt u verbinding kunt maken met toohello hersteld database met behulp van SQL Server Management Studio tooperform nodig taken, zoals tooextract een bits van gegevens van Hallo database toocopy teruggezet naar de bestaande database Hallo of toodelete Hallo bestaande database en wijzig de naam Hallo herstelde database toohello bestaande databasenaam.</span><span class="sxs-lookup"><span data-stu-id="c73c1-189">From here, you can connect toohello restored database using SQL Server Management Studio tooperform needed tasks, such as tooextract a bit of data from hello restored database toocopy into hello existing database or toodelete hello existing database and rename hello restored database toohello existing database name.</span></span> <span data-ttu-id="c73c1-190">Zie [punt in tijd terugzetten](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="c73c1-190">See [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c73c1-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c73c1-191">Next steps</span></span>

- <span data-ttu-id="c73c1-192">toolearn over service gegenereerde automatische back-ups, Zie [automatische back-ups](sql-database-automated-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c73c1-192">toolearn about service-generated automatic backups, see [automatic backups](sql-database-automated-backups.md)</span></span>
- <span data-ttu-id="c73c1-193">toolearn over het bewaren van back-up op lange termijn, Zie [lange bewaartermijn van de back-up](sql-database-long-term-retention.md)</span><span class="sxs-lookup"><span data-stu-id="c73c1-193">toolearn about long-term backup retention, see [long-term backup retention](sql-database-long-term-retention.md)</span></span>
- <span data-ttu-id="c73c1-194">toolearn over het terugzetten van back-ups, Zie [back-up terugzetten](sql-database-recovery-using-backups.md)</span><span class="sxs-lookup"><span data-stu-id="c73c1-194">toolearn about restoring from backups, see [restore from backup](sql-database-recovery-using-backups.md)</span></span>
