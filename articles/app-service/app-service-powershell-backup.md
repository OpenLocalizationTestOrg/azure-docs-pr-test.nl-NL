---
title: aaaUse PowerShell tooback ups en het terugzetten van App Service-apps
description: Meer informatie over hoe toouse PowerShell tooback ups en het terugzetten van een app in Azure App Service
services: app-service
documentationcenter: 
author: NKing92
manager: erikre
editor: 
ms.assetid: 7ea8661e-aefb-4823-9626-6bff980cdebf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2016
ms.author: nicking
ms.openlocfilehash: 4042166f6c650841926f010056d6c80ab2de57e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a><span data-ttu-id="c2b4a-103">Gebruik PowerShell tooback up en herstellen van App Service-apps</span><span class="sxs-lookup"><span data-stu-id="c2b4a-103">Use PowerShell tooback up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2b4a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2b4a-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="c2b4a-105">REST API</span><span class="sxs-lookup"><span data-stu-id="c2b4a-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="c2b4a-106">Meer informatie over hoe toouse Azure PowerShell tooback ups en het terugzetten [App Service-apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="c2b4a-106">Learn how toouse Azure PowerShell tooback up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="c2b4a-107">Zie voor meer informatie over web-app back-ups, met inbegrip van de vereisten en beperkingen, [Back-up van een web-app in Azure App Service](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="c2b4a-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2b4a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c2b4a-108">Prerequisites</span></span>
<span data-ttu-id="c2b4a-109">toouse PowerShell toomanage uw app back-ups, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c2b4a-109">toouse PowerShell toomanage your app backups, you need hello following:</span></span>

* <span data-ttu-id="c2b4a-110">**Een SAS-URL** waarmee lees- en schrijftoegang tooan Azure Storage-container.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-110">**A SAS URL** that allows read and write access tooan Azure Storage container.</span></span> <span data-ttu-id="c2b4a-111">Zie [Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor een uitleg van SAS-URL's.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-111">See [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="c2b4a-112">Zie [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) voor voorbeelden van het beheer van Azure Storage met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="c2b4a-113">**Een databaseverbindingsreeks** als u wilt dat tooback up van een database samen met uw web-app.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-113">**A database connection string** if you want tooback up a database along with your web app.</span></span>

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a><span data-ttu-id="c2b4a-114">Hoe toogenerate een toouse SAS-URL met Hallo web-app back-up cmdlets</span><span class="sxs-lookup"><span data-stu-id="c2b4a-114">How toogenerate a SAS URL toouse with hello web app backup cmdlets</span></span>
<span data-ttu-id="c2b4a-115">Een SAS-URL kan worden gegenereerd met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="c2b4a-116">Hier volgt een voorbeeld van hoe toogenerate die kan worden gebruikt met Hallo cmdlets in dit artikel besproken.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-116">Here is an example of how toogenerate one that can be used with hello cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="c2b4a-117">Installeer Azure PowerShell 1.3.2 of hoger</span><span class="sxs-lookup"><span data-stu-id="c2b4a-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="c2b4a-118">Zie [Azure PowerShell gebruiken met Azure Resource Manager](/powershell/azure/overview) voor instructies over het installeren en gebruiken van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="c2b4a-119">Maak een back-up</span><span class="sxs-lookup"><span data-stu-id="c2b4a-119">Create a backup</span></span>
<span data-ttu-id="c2b4a-120">Hallo nieuw AzureRmWebAppBackup cmdlet toocreate een back-up van een web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-120">Use hello New-AzureRmWebAppBackup cmdlet toocreate a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="c2b4a-121">Hiermee maakt u een back-up met een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="c2b4a-122">Als u tooprovide een naam voor uw back-up wilt, gebruikt u Hallo naam_back-up is een optionele parameter.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-122">If you would like tooprovide a name for your backup, use hello BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="c2b4a-123">tooinclude een database in Hallo back-up maakt eerst een database van een back-instelling met de Hallo nieuw AzureRmWebAppDatabaseBackupSetting cmdlet en opgeven dat instellen in Hallo Databases parameter van Hallo nieuw AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-123">tooinclude a database in hello backup, first create a database backup setting using hello New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in hello Databases parameter of hello New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c2b4a-124">Hallo Databases-parameter accepteert een matrix van database-instellingen, zodat u tooback van meer dan één database.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-124">hello Databases parameter accepts an array of database settings, allowing you tooback up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="c2b4a-125">Back-ups ophalen</span><span class="sxs-lookup"><span data-stu-id="c2b4a-125">Get backups</span></span>
<span data-ttu-id="c2b4a-126">Hallo Get AzureRmWebAppBackupList cmdlet retourneert een matrix van alle back-ups voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-126">hello Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="c2b4a-127">U moet Hallo-naam van het Hallo-web-app en de resourcegroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-127">You must supply hello name of hello web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="c2b4a-128">een specifieke back-up tooget Hallo Get AzureRmWebAppBackup cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-128">tooget a specific backup, use hello Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="c2b4a-129">U kunt ook een web-app-object in een Hallo back-management-cmdlets voor het gemak overbrengen.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-129">You can also pipe a web app object into any of hello backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="c2b4a-130">Automatische back-ups plannen</span><span class="sxs-lookup"><span data-stu-id="c2b4a-130">Schedule automatic backups</span></span>
<span data-ttu-id="c2b4a-131">U kunt back-ups toohappen automatisch plannen op een opgegeven interval.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-131">You can schedule backups toohappen automatically at a specified interval.</span></span> <span data-ttu-id="c2b4a-132">een back-upschema tooconfigure Hallo bewerken AzureRmWebAppBackupConfiguration cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-132">tooconfigure a backup schedule, use hello Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="c2b4a-133">Deze cmdlet bevat verschillende parameters:</span><span class="sxs-lookup"><span data-stu-id="c2b4a-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="c2b4a-134">**Naam** - hello naam van het Hallo-web-app.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-134">**Name** - hello name of hello web app.</span></span>
* <span data-ttu-id="c2b4a-135">**ResourceGroupName** - hello naam van het Hallo resource groep met Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-135">**ResourceGroupName** - hello name of hello resource group containing hello web app.</span></span>
* <span data-ttu-id="c2b4a-136">**Sleuf** : optioneel.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-136">**Slot** - Optional.</span></span> <span data-ttu-id="c2b4a-137">Hallo-naam van de web-appsite Hallo.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-137">hello name of hello web app slot.</span></span>
* <span data-ttu-id="c2b4a-138">**StorageAccountUrl** -Hallo SAS-URL voor hello Azure Storage-container toostore Hallo back-ups gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-138">**StorageAccountUrl** - hello SAS URL for hello Azure Storage container used toostore hello backups.</span></span>
* <span data-ttu-id="c2b4a-139">**FrequencyInterval** -numerieke waarde voor hoe vaak hello back-ups moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-139">**FrequencyInterval** - Numeric value for how often hello backups should be made.</span></span> <span data-ttu-id="c2b4a-140">Moet een positief geheel getal zijn.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-140">Must be a positive integer.</span></span>
* <span data-ttu-id="c2b4a-141">**FrequencyUnit** -tijdseenheid voor hoe vaak hello back-ups moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-141">**FrequencyUnit** - Unit of time for how often hello backups should be made.</span></span> <span data-ttu-id="c2b4a-142">Opties zijn uur en dag.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="c2b4a-143">**RetentionPeriodInDays** : hoeveel dagen Hallo automatische back-ups moeten worden opgeslagen voordat ze automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-143">**RetentionPeriodInDays** - How many days hello automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="c2b4a-144">**StartTime** : optioneel.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-144">**StartTime** - Optional.</span></span> <span data-ttu-id="c2b4a-145">Hallo-tijd waarop de Hallo automatische back-ups moeten beginnen.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-145">hello time when hello automatic backups should begin.</span></span> <span data-ttu-id="c2b4a-146">Back-ups worden onmiddellijk starten als deze leeg is.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="c2b4a-147">Moet een datetime-waarde.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-147">Must be a DateTime.</span></span>
* <span data-ttu-id="c2b4a-148">**Databases** : optioneel.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-148">**Databases** - Optional.</span></span> <span data-ttu-id="c2b4a-149">Een matrix met DatabaseBackupSettings voor Hallo databases toobackup.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-149">An array of DatabaseBackupSettings for hello databases toobackup.</span></span>
* <span data-ttu-id="c2b4a-150">**KeepAtLeastOneBackup** : optioneel parameter overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="c2b4a-151">Geef dit als één back-up moet altijd worden bewaard in Hallo storage-account, ongeacht hoe oud is.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-151">Supply this if one backup should always be kept in hello storage account, regardless of how old it is.</span></span>

<span data-ttu-id="c2b4a-152">Hieronder volgt een voorbeeld van hoe toouse deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-152">Following is an example of how toouse this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="c2b4a-153">tooget hello huidige back-upschema, gebruik de cmdlet Get-AzureRmWebAppBackupConfiguration Hallo.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-153">tooget hello current backup schedule, use hello Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="c2b4a-154">Dit is handig voor het wijzigen van een planning die al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="c2b4a-155">Een web-app vanaf een back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="c2b4a-155">Restore a web app from a backup</span></span>
<span data-ttu-id="c2b4a-156">een web-app uit een back-up, gebruik de cmdlet voor Hallo terugzetten AzureRmWebAppBackup toorestore.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-156">toorestore a web app from a backup, use hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c2b4a-157">de eenvoudigste manier toouse Hallo deze cmdlet is toopipe in een back-object is opgehaald uit de cmdlet Get-AzureRmWebAppBackup Hallo of de cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-157">hello easiest way toouse this cmdlet is toopipe in a backup object retrieved from hello Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="c2b4a-158">Zodra u een back-object hebt, kunt u het doorsluizen naar Hallo terugzetten AzureRmWebAppBackup cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-158">Once you have a backup object, you can pipe it into hello Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c2b4a-159">Hallo overschrijven switch parameter tooindicate die u van plan toooverwrite Hallo inhoud van uw web-app met inhoud van back-up Hallo Hallo bent opgeven.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-159">Specify hello Overwrite switch parameter tooindicate that you intend toooverwrite hello contents of your web app with hello contents of hello backup.</span></span> <span data-ttu-id="c2b4a-160">Als Hallo back-up databases bevat, worden deze databases ook hersteld.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-160">If hello backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="c2b4a-161">Hier volgt een voorbeeld van hoe toouse terugzetten AzureRmWebAppBackup Hallo door te geven van alle Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-161">Following is an example of how toouse hello Restore-AzureRmWebAppBackup by specifying all hello parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="c2b4a-162">Verwijderen van een back-up</span><span class="sxs-lookup"><span data-stu-id="c2b4a-162">Delete a backup</span></span>
<span data-ttu-id="c2b4a-163">een back-up, toodelete Hallo verwijderen AzureRmWebAppBackup cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-163">toodelete a backup, use hello Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="c2b4a-164">Hiermee verwijdert u Hallo back-up van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-164">This removes hello backup from your storage account.</span></span> <span data-ttu-id="c2b4a-165">Geef de naam van uw app, de resourcegroep en ID Hallo Hallo back-up gewenste toodelete.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-165">Specify your app name, its resource group, and hello ID of hello backup you want toodelete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="c2b4a-166">U kunt ook een back-upobject overbrengen naar Hallo verwijderen AzureRmWebAppBackup cmdlet toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="c2b4a-166">You can also pipe a backup object into hello Remove-AzureRmWebAppBackup cmdlet toodelete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
