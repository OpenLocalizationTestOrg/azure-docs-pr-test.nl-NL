---
title: PowerShell gebruiken voor back-up en herstellen van App Service-apps
description: Informatie over het gebruik van PowerShell back-up en herstellen van een app in Azure App Service
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
ms.openlocfilehash: 34a7e1d025c301ca056753d964bb3c5f4f1a62d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a><span data-ttu-id="7ce8a-103">PowerShell gebruiken voor back-up en herstellen van App Service-apps</span><span class="sxs-lookup"><span data-stu-id="7ce8a-103">Use PowerShell to back up and restore App Service apps</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ce8a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ce8a-104">PowerShell</span></span>](app-service-powershell-backup.md)
> * [<span data-ttu-id="7ce8a-105">REST API</span><span class="sxs-lookup"><span data-stu-id="7ce8a-105">REST API</span></span>](../app-service-web/websites-csm-backup.md)
> 
> 

<span data-ttu-id="7ce8a-106">Informatie over het gebruik van Azure PowerShell back-up en herstellen van [App Service-apps](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="7ce8a-106">Learn how to use Azure PowerShell to back up and restore [App Service apps](https://azure.microsoft.com/services/app-service/web/).</span></span> <span data-ttu-id="7ce8a-107">Zie voor meer informatie over web-app back-ups, met inbegrip van de vereisten en beperkingen, [Back-up van een web-app in Azure App Service](../app-service-web/web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="7ce8a-107">For more information about web app backups, including requirements and restrictions, see [Back up a web app in Azure App Service](../app-service-web/web-sites-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ce8a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ce8a-108">Prerequisites</span></span>
<span data-ttu-id="7ce8a-109">Als PowerShell wilt gebruiken voor het beheren van uw app back-ups, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="7ce8a-109">To use PowerShell to manage your app backups, you need the following:</span></span>

* <span data-ttu-id="7ce8a-110">**Een SAS-URL** waarmee lees- en schrijftoegang tot een Azure Storage-container.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-110">**A SAS URL** that allows read and write access to an Azure Storage container.</span></span> <span data-ttu-id="7ce8a-111">Zie [inzicht in het SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor een uitleg van SAS-URL's.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-111">See [Understanding the SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) for an explanation of SAS URLs.</span></span> <span data-ttu-id="7ce8a-112">Zie [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) voor voorbeelden van het beheer van Azure Storage met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-112">See [Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) for examples of managing Azure Storage using PowerShell.</span></span>
* <span data-ttu-id="7ce8a-113">**Een databaseverbindingsreeks** als u wilt back-up van een database samen met uw web-app.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-113">**A database connection string** if you want to back up a database along with your web app.</span></span>

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a><span data-ttu-id="7ce8a-114">Het genereren van een SAS-URL voor gebruik met de back-cmdlets voor web-app</span><span class="sxs-lookup"><span data-stu-id="7ce8a-114">How to generate a SAS URL to use with the web app backup cmdlets</span></span>
<span data-ttu-id="7ce8a-115">Een SAS-URL kan worden gegenereerd met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-115">A SAS URL can be generated with PowerShell.</span></span> <span data-ttu-id="7ce8a-116">Hier volgt een voorbeeld van het genereren van een die kunnen worden gebruikt met de cmdlets die in dit artikel wordt besproken.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-116">Here is an example of how to generate one that can be used with the cmdlets discussed in this article.</span></span>

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a><span data-ttu-id="7ce8a-117">Installeer Azure PowerShell 1.3.2 of hoger</span><span class="sxs-lookup"><span data-stu-id="7ce8a-117">Install Azure PowerShell 1.3.2 or greater</span></span>
<span data-ttu-id="7ce8a-118">Zie [Azure PowerShell gebruiken met Azure Resource Manager](/powershell/azure/overview) voor instructies over het installeren en gebruiken van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-118">See [Using Azure PowerShell with Azure Resource Manager](/powershell/azure/overview) for instructions on installing and using Azure PowerShell.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="7ce8a-119">Maak een back-up</span><span class="sxs-lookup"><span data-stu-id="7ce8a-119">Create a backup</span></span>
<span data-ttu-id="7ce8a-120">Gebruik de cmdlet New-AzureRmWebAppBackup voor het maken van een back-up van een web-app.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-120">Use the New-AzureRmWebAppBackup cmdlet to create a backup of a web app.</span></span>

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

<span data-ttu-id="7ce8a-121">Hiermee maakt u een back-up met een automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-121">This creates a backup with an automatically generated name.</span></span> <span data-ttu-id="7ce8a-122">Als u een naam opgeven voor de back-up wilt, gebruikt u de optionele parameter naam_back-up.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-122">If you would like to provide a name for your backup, use the BackupName optional parameter.</span></span>

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

<span data-ttu-id="7ce8a-123">Als u wilt opnemen een database in de back-up, maakt eerst een database back-instelling met de cmdlet New-AzureRmWebAppDatabaseBackupSetting en die instelling in de parameter Databases van de cmdlet New-AzureRmWebAppBackup opgeven.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-123">To include a database in the backup, first create a database backup setting using the New-AzureRmWebAppDatabaseBackupSetting cmdlet, then supply that setting in the Databases parameter of the New-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7ce8a-124">De Databases-parameter accepteert een matrix van database-instellingen, zodat u kunt back-up van meer dan één database.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-124">The Databases parameter accepts an array of database settings, allowing you to back up more than one database.</span></span>

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a><span data-ttu-id="7ce8a-125">Back-ups ophalen</span><span class="sxs-lookup"><span data-stu-id="7ce8a-125">Get backups</span></span>
<span data-ttu-id="7ce8a-126">De cmdlet Get-AzureRmWebAppBackupList retourneert een matrix van alle back-ups voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-126">The Get-AzureRmWebAppBackupList cmdlet returns an array of all backups for a web app.</span></span> <span data-ttu-id="7ce8a-127">U moet de naam van de web-app en de resourcegroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-127">You must supply the name of the web app and its resource group.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

<span data-ttu-id="7ce8a-128">Als u een specifieke back-up, gebruikt u de cmdlet Get-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-128">To get a specific backup, use the Get-AzureRmWebAppBackup cmdlet.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

<span data-ttu-id="7ce8a-129">U kunt ook een web-app-object in een van de back-up-cmdlets voor het gemak overbrengen.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-129">You can also pipe a web app object into any of the backup management cmdlets for convenience.</span></span>

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a><span data-ttu-id="7ce8a-130">Automatische back-ups plannen</span><span class="sxs-lookup"><span data-stu-id="7ce8a-130">Schedule automatic backups</span></span>
<span data-ttu-id="7ce8a-131">U kunt back-ups automatisch gebeurt met een opgegeven interval plannen.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-131">You can schedule backups to happen automatically at a specified interval.</span></span> <span data-ttu-id="7ce8a-132">Gebruik de cmdlet bewerken AzureRmWebAppBackupConfiguration voor het configureren van een back-upschema.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-132">To configure a backup schedule, use the Edit-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="7ce8a-133">Deze cmdlet bevat verschillende parameters:</span><span class="sxs-lookup"><span data-stu-id="7ce8a-133">This cmdlet takes several parameters:</span></span>

* <span data-ttu-id="7ce8a-134">**Naam** -de naam van de web-app.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-134">**Name** - The name of the web app.</span></span>
* <span data-ttu-id="7ce8a-135">**ResourceGroupName** -de naam van de resourcegroep met de web-app.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-135">**ResourceGroupName** - The name of the resource group containing the web app.</span></span>
* <span data-ttu-id="7ce8a-136">**Sleuf** : optioneel.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-136">**Slot** - Optional.</span></span> <span data-ttu-id="7ce8a-137">De naam van de web-appsite.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-137">The name of the web app slot.</span></span>
* <span data-ttu-id="7ce8a-138">**StorageAccountUrl** -de SAS-URL voor de Azure Storage-container die is gebruikt voor het opslaan van de back-ups.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-138">**StorageAccountUrl** - The SAS URL for the Azure Storage container used to store the backups.</span></span>
* <span data-ttu-id="7ce8a-139">**FrequencyInterval** -numerieke waarde voor hoe vaak de back-ups moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-139">**FrequencyInterval** - Numeric value for how often the backups should be made.</span></span> <span data-ttu-id="7ce8a-140">Moet een positief geheel getal zijn.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-140">Must be a positive integer.</span></span>
* <span data-ttu-id="7ce8a-141">**FrequencyUnit** -tijdseenheid voor hoe vaak de back-ups moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-141">**FrequencyUnit** - Unit of time for how often the backups should be made.</span></span> <span data-ttu-id="7ce8a-142">Opties zijn uur en dag.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-142">Options are Hour and Day.</span></span>
* <span data-ttu-id="7ce8a-143">**RetentionPeriodInDays** : hoeveel dagen de automatische back-ups moeten worden opgeslagen voordat ze automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-143">**RetentionPeriodInDays** - How many days the automatic backups should be saved before being automatically deleted.</span></span>
* <span data-ttu-id="7ce8a-144">**StartTime** : optioneel.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-144">**StartTime** - Optional.</span></span> <span data-ttu-id="7ce8a-145">De tijd waarop de automatische back-ups moeten beginnen.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-145">The time when the automatic backups should begin.</span></span> <span data-ttu-id="7ce8a-146">Back-ups worden onmiddellijk starten als deze leeg is.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-146">Backups begin immediately if this is null.</span></span> <span data-ttu-id="7ce8a-147">Moet een datetime-waarde.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-147">Must be a DateTime.</span></span>
* <span data-ttu-id="7ce8a-148">**Databases** : optioneel.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-148">**Databases** - Optional.</span></span> <span data-ttu-id="7ce8a-149">Een matrix met DatabaseBackupSettings voor de databases naar de back-up.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-149">An array of DatabaseBackupSettings for the databases to backup.</span></span>
* <span data-ttu-id="7ce8a-150">**KeepAtLeastOneBackup** : optioneel parameter overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-150">**KeepAtLeastOneBackup** - Optional switched parameter.</span></span> <span data-ttu-id="7ce8a-151">Geef dit als één back-up moet altijd worden bewaard in de storage-account, ongeacht hoe oud is.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-151">Supply this if one backup should always be kept in the storage account, regardless of how old it is.</span></span>

<span data-ttu-id="7ce8a-152">Hieronder volgt een voorbeeld van het gebruik van deze cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-152">Following is an example of how to use this cmdlet.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

<span data-ttu-id="7ce8a-153">Als u de huidige back-upschema, gebruikt u de cmdlet Get-AzureRmWebAppBackupConfiguration.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-153">To get the current backup schedule, use the Get-AzureRmWebAppBackupConfiguration cmdlet.</span></span> <span data-ttu-id="7ce8a-154">Dit is handig voor het wijzigen van een planning die al is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-154">This can be useful for modifying a schedule that has already been configured.</span></span>

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a><span data-ttu-id="7ce8a-155">Een web-app vanaf een back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="7ce8a-155">Restore a web app from a backup</span></span>
<span data-ttu-id="7ce8a-156">Als u een web-app herstellen vanaf een back-up, herstel AzureRmWebAppBackup cmdlet te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-156">To restore a web app from a backup, use the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7ce8a-157">De eenvoudigste manier om het gebruik van deze cmdlet is pipe in een back-object is opgehaald van de cmdlet Get-AzureRmWebAppBackup of de cmdlet Get-AzureRmWebAppBackupList.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-157">The easiest way to use this cmdlet is to pipe in a backup object retrieved from the Get-AzureRmWebAppBackup cmdlet or Get-AzureRmWebAppBackupList cmdlet.</span></span>

<span data-ttu-id="7ce8a-158">Zodra u een back-object hebt, kunt u het doorsluizen naar de cmdlet terugzetten AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-158">Once you have a backup object, you can pipe it into the Restore-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7ce8a-159">Geef de parameter overschrijven om aan te geven die u van plan bent om te overschrijven van de inhoud van uw web-app met de inhoud van de back-up.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-159">Specify the Overwrite switch parameter to indicate that you intend to overwrite the contents of your web app with the contents of the backup.</span></span> <span data-ttu-id="7ce8a-160">Als de back-up databases bevat, worden deze databases ook hersteld.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-160">If the backup contains databases, those databases are restored as well.</span></span>

        $backup | Restore-AzureRmWebAppBackup -Overwrite

<span data-ttu-id="7ce8a-161">Hieronder volgt een voorbeeld van het gebruik van de Restore-AzureRmWebAppBackup door te geven van alle parameters.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-161">Following is an example of how to use the Restore-AzureRmWebAppBackup by specifying all the parameters.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a><span data-ttu-id="7ce8a-162">Verwijderen van een back-up</span><span class="sxs-lookup"><span data-stu-id="7ce8a-162">Delete a backup</span></span>
<span data-ttu-id="7ce8a-163">Als u wilt verwijderen van een back-up, gebruikt u de cmdlet Remove-AzureRmWebAppBackup.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-163">To delete a backup, use the Remove-AzureRmWebAppBackup cmdlet.</span></span> <span data-ttu-id="7ce8a-164">Hiermee verwijdert u de back-up van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-164">This removes the backup from your storage account.</span></span> <span data-ttu-id="7ce8a-165">Geef de appnaam van uw, de resourcegroep en de ID van de back-up die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-165">Specify your app name, its resource group, and the ID of the backup you want to delete.</span></span>

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

<span data-ttu-id="7ce8a-166">U kunt ook een back-upobject doorsluizen naar de cmdlet Remove-AzureRmWebAppBackup te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7ce8a-166">You can also pipe a backup object into the Remove-AzureRmWebAppBackup cmdlet to delete it.</span></span>

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
