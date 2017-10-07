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
# <a name="use-powershell-tooback-up-and-restore-app-service-apps"></a>Gebruik PowerShell tooback up en herstellen van App Service-apps
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

Meer informatie over hoe toouse Azure PowerShell tooback ups en het terugzetten [App Service-apps](https://azure.microsoft.com/services/app-service/web/). Zie voor meer informatie over web-app back-ups, met inbegrip van de vereisten en beperkingen, [Back-up van een web-app in Azure App Service](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Vereisten
toouse PowerShell toomanage uw app back-ups, moet u hello te volgen:

* **Een SAS-URL** waarmee lees- en schrijftoegang tooan Azure Storage-container. Zie [Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor een uitleg van SAS-URL's. Zie [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) voor voorbeelden van het beheer van Azure Storage met behulp van PowerShell.
* **Een databaseverbindingsreeks** als u wilt dat tooback up van een database samen met uw web-app.

### <a name="how-toogenerate-a-sas-url-toouse-with-hello-web-app-backup-cmdlets"></a>Hoe toogenerate een toouse SAS-URL met Hallo web-app back-up cmdlets
Een SAS-URL kan worden gegenereerd met PowerShell. Hier volgt een voorbeeld van hoe toogenerate die kan worden gebruikt met Hallo cmdlets in dit artikel besproken.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure tooselect hello appropriate key. Here we select hello first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Installeer Azure PowerShell 1.3.2 of hoger
Zie [Azure PowerShell gebruiken met Azure Resource Manager](/powershell/azure/overview) voor instructies over het installeren en gebruiken van Azure PowerShell.

## <a name="create-a-backup"></a>Maak een back-up
Hallo nieuw AzureRmWebAppBackup cmdlet toocreate een back-up van een web-app gebruiken.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Hiermee maakt u een back-up met een automatisch gegenereerde naam. Als u tooprovide een naam voor uw back-up wilt, gebruikt u Hallo naam_back-up is een optionele parameter.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

tooinclude een database in Hallo back-up maakt eerst een database van een back-instelling met de Hallo nieuw AzureRmWebAppDatabaseBackupSetting cmdlet en opgeven dat instellen in Hallo Databases parameter van Hallo nieuw AzureRmWebAppBackup cmdlet. Hallo Databases-parameter accepteert een matrix van database-instellingen, zodat u tooback van meer dan één database.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Back-ups ophalen
Hallo Get AzureRmWebAppBackupList cmdlet retourneert een matrix van alle back-ups voor een web-app. U moet Hallo-naam van het Hallo-web-app en de resourcegroep opgeven.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

een specifieke back-up tooget Hallo Get AzureRmWebAppBackup cmdlet gebruiken.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

U kunt ook een web-app-object in een Hallo back-management-cmdlets voor het gemak overbrengen.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Automatische back-ups plannen
U kunt back-ups toohappen automatisch plannen op een opgegeven interval. een back-upschema tooconfigure Hallo bewerken AzureRmWebAppBackupConfiguration cmdlet gebruiken. Deze cmdlet bevat verschillende parameters:

* **Naam** - hello naam van het Hallo-web-app.
* **ResourceGroupName** - hello naam van het Hallo resource groep met Hallo web-app.
* **Sleuf** : optioneel. Hallo-naam van de web-appsite Hallo.
* **StorageAccountUrl** -Hallo SAS-URL voor hello Azure Storage-container toostore Hallo back-ups gebruikt.
* **FrequencyInterval** -numerieke waarde voor hoe vaak hello back-ups moeten worden gemaakt. Moet een positief geheel getal zijn.
* **FrequencyUnit** -tijdseenheid voor hoe vaak hello back-ups moeten worden gemaakt. Opties zijn uur en dag.
* **RetentionPeriodInDays** : hoeveel dagen Hallo automatische back-ups moeten worden opgeslagen voordat ze automatisch worden verwijderd.
* **StartTime** : optioneel. Hallo-tijd waarop de Hallo automatische back-ups moeten beginnen. Back-ups worden onmiddellijk starten als deze leeg is. Moet een datetime-waarde.
* **Databases** : optioneel. Een matrix met DatabaseBackupSettings voor Hallo databases toobackup.
* **KeepAtLeastOneBackup** : optioneel parameter overgeschakeld. Geef dit als één back-up moet altijd worden bewaard in Hallo storage-account, ongeacht hoe oud is.

Hieronder volgt een voorbeeld van hoe toouse deze cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

tooget hello huidige back-upschema, gebruik de cmdlet Get-AzureRmWebAppBackupConfiguration Hallo. Dit is handig voor het wijzigen van een planning die al is geconfigureerd.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify hello configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply hello new configuration by piping it into hello Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Een web-app vanaf een back-up herstellen
een web-app uit een back-up, gebruik de cmdlet voor Hallo terugzetten AzureRmWebAppBackup toorestore. de eenvoudigste manier toouse Hallo deze cmdlet is toopipe in een back-object is opgehaald uit de cmdlet Get-AzureRmWebAppBackup Hallo of de cmdlet Get-AzureRmWebAppBackupList.

Zodra u een back-object hebt, kunt u het doorsluizen naar Hallo terugzetten AzureRmWebAppBackup cmdlet. Hallo overschrijven switch parameter tooindicate die u van plan toooverwrite Hallo inhoud van uw web-app met inhoud van back-up Hallo Hallo bent opgeven. Als Hallo back-up databases bevat, worden deze databases ook hersteld.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Hier volgt een voorbeeld van hoe toouse terugzetten AzureRmWebAppBackup Hallo door te geven van alle Hallo-parameters.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Verwijderen van een back-up
een back-up, toodelete Hallo verwijderen AzureRmWebAppBackup cmdlet gebruiken. Hiermee verwijdert u Hallo back-up van uw opslagaccount. Geef de naam van uw app, de resourcegroep en ID Hallo Hallo back-up gewenste toodelete.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

U kunt ook een back-upobject overbrengen naar Hallo verwijderen AzureRmWebAppBackup cmdlet toodelete deze.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
