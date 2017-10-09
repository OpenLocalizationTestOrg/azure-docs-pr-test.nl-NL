---
title: aaaRestore Sleutelkluis sleutel en geheim voor virtuele machines met Azure Backup versleuteld | Microsoft Docs
description: Meer informatie over hoe toorestore Key Vault sleutel en geheime in Azure back-up met behulp van PowerShell
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Sleutelkluis-sleutel en geheime voor versleutelde VM's met Azure back-up herstellen
In dit artikel wordt gesproken over het gebruik van Azure VM Backup tooperform herstel van versleutelde Azure virtuele machines, als uw sleutel en geheime bestaan niet in de sleutelkluis Hallo. Deze stappen kunnen ook worden gebruikt als u toomaintain een afzonderlijk exemplaar van de sleutel (coderingssleutel Key wilt) en geheim (sleutel BitLocker-versleuteling) voor Hallo VM hersteld.

## <a name="prerequisites"></a>Vereisten
* **Back-up van virtuele machines versleuteld** - gecodeerde virtuele machines in Azure back-ups zijn met Azure Backup. Raadpleeg Hallo artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md) voor meer informatie over hoe toobackup Azure Virtual machines versleuteld.
* **Azure Sleutelkluis configureren** : Zorg ervoor dat sleutelkluis toowhich sleutels en geheimen nodig toobe hersteld is al aanwezig. Raadpleeg Hallo artikel [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md) voor meer informatie over het beheer van de sleutelkluis.
* **Herstellen schijf** -Zorg ervoor dat u de hersteltaak voor het herstellen van schijven voor het gebruik van versleutelde VM hebt geactiveerd [PowerShell stappen](backup-azure-vms-automation.md#restore-an-azure-vm). Dit is omdat deze taak genereert een JSON-bestand in uw opslagaccount met sleutels en geheimen voor Hallo versleuteld VM toobe hersteld.

## <a name="get-key-and-secret-from-azure-backup"></a>Sleutel en geheime ophalen uit Azure Backup

> [!NOTE]
> Als de schijf is hersteld voor Hallo VM versleuteld, zorg ervoor dat:
> 1. $details is gevuld met restore schijf taakdetails, zoals vermeld in [PowerShell stappen voor het terugzetten Hallo schijven sectie](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. VM moet worden gemaakt van herstelde schijven alleen **nadat de sleutel en geheime is herstelde tookey kluis**.
>
>

Query Hallo schijfeigenschappen voor Hallo taakdetails hersteld.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Hello Azure storage-context instellen en JSON-configuratiebestand met de sleutel en geheime details voor versleutelde virtuele machine herstellen.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Sleutel herstellen
Zodra Hallo JSON-bestand wordt gegenereerd in Hallo doelpad bovengenoemde, key blob-bestand genereren van Hallo JSON en toorestore sleutel cmdlet tooput Hallo sleutel (een KEK) terug in de sleutelkluis Hallo feed.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Geheim herstellen
Gebruik Hallo JSON-bestand gegenereerd hierboven tooget geheime naam en waarde en tooset geheime cmdlet tooput Hallo geheim (BEK) terug in de sleutelkluis Hallo feed. **Deze cmdlets gebruiken als uw VM is versleuteld met behulp van BEK en KEK-sleutel.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Als uw virtuele machine wordt **versleuteld met BEK alleen**, geheime blob-bestand genereren van Hallo JSON en toorestore geheime cmdlet tooput Hallo geheim (BEK) terug in de sleutelkluis Hallo feed.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Waarde voor $secretname kan worden verkregen door te verwijzen toohello uitvoer van $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl en tekst na geheimen / uitvoer geheime URL is bijvoorbeeld https://keyvaultname.vault.azure.net/secrets/ B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 en de geheime naam is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Waarde van Hallo tag DiskEncryptionKeyFileName is hetzelfde als de geheime naam.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Virtuele machine van de herstelde schijf maken
Als u reservekopie versleutelde VM die gebruikmaakt van Azure VM-back-up hebt gemaakt, bovengenoemde Hallo PowerShell-cmdlets help herstellen van sleutel en geheime back toohello sleutelkluis. Raadpleeg nadat deze is teruggezet, Hallo artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate virtuele machines van de herstelde schijf, sleutel en geheime versleuteld.

## <a name="legacy-approach"></a>Verouderde benadering
Hallo-benadering bovengenoemde zou werken voor alle Hallo-herstelpunten. Echter hello oudere benadering van sleutel en geheime informatie ophalen van herstelpunt, zou zijn geldig voor de herstelpunten die ouder zijn dan 11 juli 2017 voor virtuele machines die zijn versleuteld met BEK en KEK-sleutel. Zodra de hersteltaak voor de schijf is voltooid voor het gebruik van versleutelde VM [PowerShell stappen](backup-azure-vms-automation.md#restore-an-azure-vm), zorg ervoor dat $rp is gevuld met een geldige waarde.

### <a name="restore-key"></a>Sleutel herstellen
Hallo volgende cmdlets tooget sleutel (een KEK) informatie uit herstelpunt gebruiken en voer deze toorestore sleutel cmdlet tooput weer in de sleutelkluis Hallo.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Geheim herstellen
Hallo volgende cmdlets tooget geheim (BEK) informatie uit herstelpunt gebruiken en voer deze tooset geheime cmdlet tooput weer in de sleutelkluis Hallo.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Waarde voor $secretname kan worden verkregen door toohello uitvoer van $rp1 verwijst. KeyAndSecretDetails.SecretUrl en het gebruik van tekst na geheimen / uitvoer geheime URL is bijvoorbeeld https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 en geheime naam is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Waarde van Hallo tag DiskEncryptionKeyFileName is hetzelfde als de geheime naam.
> 3. Waarde voor DiskEncryptionKeyEncryptionKeyURL kan worden verkregen van de sleutelkluis na Hallo sleutels weer terugzetten en het gebruik van [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet
>
>

## <a name="next-steps"></a>Volgende stappen
Na het terugzetten van de sleutel en geheime back tookey kluis verwijzen Hallo artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate virtuele machines van de herstelde schijf, sleutel en geheime versleuteld.
