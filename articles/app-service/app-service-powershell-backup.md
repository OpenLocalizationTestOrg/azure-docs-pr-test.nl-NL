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
# <a name="use-powershell-to-back-up-and-restore-app-service-apps"></a>PowerShell gebruiken voor back-up en herstellen van App Service-apps
> [!div class="op_single_selector"]
> * [PowerShell](app-service-powershell-backup.md)
> * [REST API](../app-service-web/websites-csm-backup.md)
> 
> 

Informatie over het gebruik van Azure PowerShell back-up en herstellen van [App Service-apps](https://azure.microsoft.com/services/app-service/web/). Zie voor meer informatie over web-app back-ups, met inbegrip van de vereisten en beperkingen, [Back-up van een web-app in Azure App Service](../app-service-web/web-sites-backup.md).

## <a name="prerequisites"></a>Vereisten
Als PowerShell wilt gebruiken voor het beheren van uw app back-ups, moet u het volgende:

* **Een SAS-URL** waarmee lees- en schrijftoegang tot een Azure Storage-container. Zie [inzicht in het SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor een uitleg van SAS-URL's. Zie [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) voor voorbeelden van het beheer van Azure Storage met behulp van PowerShell.
* **Een databaseverbindingsreeks** als u wilt back-up van een database samen met uw web-app.

### <a name="how-to-generate-a-sas-url-to-use-with-the-web-app-backup-cmdlets"></a>Het genereren van een SAS-URL voor gebruik met de back-cmdlets voor web-app
Een SAS-URL kan worden gegenereerd met PowerShell. Hier volgt een voorbeeld van het genereren van een die kunnen worden gebruikt met de cmdlets die in dit artikel wordt besproken.

        $storageAccountName = "<your storage account's name>"
        $storageAccountRg = "<your storage account's resource group>"

        # This returns an array of keys for your storage account. Be sure to select the appropriate key. Here we select the first key as a default.
        $storageAccountKey = Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccountRg -Name $storageAccountName
        $context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey[0].Value

        $blobContainerName = "<name of blob container for app backups>"
        $sasUrl = New-AzureStorageContainerSASToken -Name $blobContainerName -Permission rwdl -Context $context -ExpiryTime (Get-Date).AddMonths(1) -FullUri

## <a name="install-azure-powershell-132-or-greater"></a>Installeer Azure PowerShell 1.3.2 of hoger
Zie [Azure PowerShell gebruiken met Azure Resource Manager](/powershell/azure/overview) voor instructies over het installeren en gebruiken van Azure PowerShell.

## <a name="create-a-backup"></a>Maak een back-up
Gebruik de cmdlet New-AzureRmWebAppBackup voor het maken van een back-up van een web-app.

        $sasUrl = "<your SAS URL>"
        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl

Hiermee maakt u een back-up met een automatisch gegenereerde naam. Als u een naam opgeven voor de back-up wilt, gebruikt u de optionele parameter naam_back-up.

        $backup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -StorageAccountUrl $sasUrl -BackupName MyBackup

Als u wilt opnemen een database in de back-up, maakt eerst een database back-instelling met de cmdlet New-AzureRmWebAppDatabaseBackupSetting en die instelling in de parameter Databases van de cmdlet New-AzureRmWebAppBackup opgeven. De Databases-parameter accepteert een matrix van database-instellingen, zodat u kunt back-up van meer dan één database.

        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbBackup = New-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupName MyBackup -StorageAccountUrl $sasUrl -Databases $dbSetting1,$dbSetting2

## <a name="get-backups"></a>Back-ups ophalen
De cmdlet Get-AzureRmWebAppBackupList retourneert een matrix van alle back-ups voor een web-app. U moet de naam van de web-app en de resourcegroep opgeven.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $backups = Get-AzureRmWebAppBackupList -Name $appName -ResourceGroupName $resourceGroupName

Als u een specifieke back-up, gebruikt u de cmdlet Get-AzureRmWebAppBackup.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102

U kunt ook een web-app-object in een van de back-up-cmdlets voor het gemak overbrengen.

        $app = Get-AzureRmWebApp -Name ContosoApp -ResourceGroupName Default-Web-WestUS
        $backupList = $app | Get-AzureRmWebAppBackupList
        $backup = $app | Get-AzureRmWebAppBackup -BackupId 10102

## <a name="schedule-automatic-backups"></a>Automatische back-ups plannen
U kunt back-ups automatisch gebeurt met een opgegeven interval plannen. Gebruik de cmdlet bewerken AzureRmWebAppBackupConfiguration voor het configureren van een back-upschema. Deze cmdlet bevat verschillende parameters:

* **Naam** -de naam van de web-app.
* **ResourceGroupName** -de naam van de resourcegroep met de web-app.
* **Sleuf** : optioneel. De naam van de web-appsite.
* **StorageAccountUrl** -de SAS-URL voor de Azure Storage-container die is gebruikt voor het opslaan van de back-ups.
* **FrequencyInterval** -numerieke waarde voor hoe vaak de back-ups moeten worden gemaakt. Moet een positief geheel getal zijn.
* **FrequencyUnit** -tijdseenheid voor hoe vaak de back-ups moeten worden gemaakt. Opties zijn uur en dag.
* **RetentionPeriodInDays** : hoeveel dagen de automatische back-ups moeten worden opgeslagen voordat ze automatisch worden verwijderd.
* **StartTime** : optioneel. De tijd waarop de automatische back-ups moeten beginnen. Back-ups worden onmiddellijk starten als deze leeg is. Moet een datetime-waarde.
* **Databases** : optioneel. Een matrix met DatabaseBackupSettings voor de databases naar de back-up.
* **KeepAtLeastOneBackup** : optioneel parameter overgeschakeld. Geef dit als één back-up moet altijd worden bewaard in de storage-account, ongeacht hoe oud is.

Hieronder volgt een voorbeeld van het gebruik van deze cmdlet.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Edit-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName -Slot $slotName `
          -StorageAccountUrl "<your SAS URL>" -FrequencyInterval 6 -FrequencyUnit Hour -Databases $dbSetting1,$dbSetting2 `
          -KeepAtLeastOneBackup -StartTime (Get-Date).AddHours(1)

Als u de huidige back-upschema, gebruikt u de cmdlet Get-AzureRmWebAppBackupConfiguration. Dit is handig voor het wijzigen van een planning die al is geconfigureerd.

        $configuration = Get-AzureRmWebAppBackupConfiguration -Name $appName -ResourceGroupName $resourceGroupName

        # Modify the configuration slightly
        $configuration.FrequencyInterval = 2
        $configuration.FrequencyUnit = "Day"

        # Apply the new configuration by piping it into the Edit-AzureRmWebAppBackupConfiguration cmdlet
        $configuration | Edit-AzureRmWebAppBackupConfiguration

## <a name="restore-a-web-app-from-a-backup"></a>Een web-app vanaf een back-up herstellen
Als u een web-app herstellen vanaf een back-up, herstel AzureRmWebAppBackup cmdlet te gebruiken. De eenvoudigste manier om het gebruik van deze cmdlet is pipe in een back-object is opgehaald van de cmdlet Get-AzureRmWebAppBackup of de cmdlet Get-AzureRmWebAppBackupList.

Zodra u een back-object hebt, kunt u het doorsluizen naar de cmdlet terugzetten AzureRmWebAppBackup. Geef de parameter overschrijven om aan te geven die u van plan bent om te overschrijven van de inhoud van uw web-app met de inhoud van de back-up. Als de back-up databases bevat, worden deze databases ook hersteld.

        $backup | Restore-AzureRmWebAppBackup -Overwrite

Hieronder volgt een voorbeeld van het gebruik van de Restore-AzureRmWebAppBackup door te geven van alle parameters.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        $slotName = "StagingSlot"
        $blobName = "ContosoBackup.zip"
        $dbSetting1 = New-AzureRmWebAppDatabaseBackupSetting -Name DB1 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        $dbSetting2 = New-AzureRmWebAppDatabaseBackupSetting -Name DB2 -DatabaseType SqlAzure -ConnectionString "<connection_string>"
        Restore-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -Slot $slotName -StorageAccountUrl "<your SAS URL>" -BlobName $blobName -Databases $dbSetting1,$dbSetting2 -Overwrite

## <a name="delete-a-backup"></a>Verwijderen van een back-up
Als u wilt verwijderen van een back-up, gebruikt u de cmdlet Remove-AzureRmWebAppBackup. Hiermee verwijdert u de back-up van uw opslagaccount. Geef de appnaam van uw, de resourcegroep en de ID van de back-up die u wilt verwijderen.

        $resourceGroupName = "Default-Web-WestUS"
        $appName = "ContosoApp"
        Remove-AzureRmWebAppBackup -ResourceGroupName $resourceGroupName -Name $appName -BackupId 10102

U kunt ook een back-upobject doorsluizen naar de cmdlet Remove-AzureRmWebAppBackup te verwijderen.

        $backup = Get-AzureRmWebAppBackup -Name $appName -ResourceGroupName $resourceGroupName -BackupId 10102
        $backup | Remove-AzureRmWebAppBackup -Overwrite
