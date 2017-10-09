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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="137ea-103">Sleutelkluis-sleutel en geheime voor versleutelde VM's met Azure back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="137ea-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="137ea-104">In dit artikel wordt gesproken over het gebruik van Azure VM Backup tooperform herstel van versleutelde Azure virtuele machines, als uw sleutel en geheime bestaan niet in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="137ea-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="137ea-105">Deze stappen kunnen ook worden gebruikt als u toomaintain een afzonderlijk exemplaar van de sleutel (coderingssleutel Key wilt) en geheim (sleutel BitLocker-versleuteling) voor Hallo VM hersteld.</span><span class="sxs-lookup"><span data-stu-id="137ea-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="137ea-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="137ea-106">Prerequisites</span></span>
* <span data-ttu-id="137ea-107">**Back-up van virtuele machines versleuteld** - gecodeerde virtuele machines in Azure back-ups zijn met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="137ea-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="137ea-108">Raadpleeg Hallo artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md) voor meer informatie over hoe toobackup Azure Virtual machines versleuteld.</span><span class="sxs-lookup"><span data-stu-id="137ea-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="137ea-109">**Azure Sleutelkluis configureren** : Zorg ervoor dat sleutelkluis toowhich sleutels en geheimen nodig toobe hersteld is al aanwezig.</span><span class="sxs-lookup"><span data-stu-id="137ea-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="137ea-110">Raadpleeg Hallo artikel [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md) voor meer informatie over het beheer van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="137ea-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="137ea-111">**Herstellen schijf** -Zorg ervoor dat u de hersteltaak voor het herstellen van schijven voor het gebruik van versleutelde VM hebt geactiveerd [PowerShell stappen](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="137ea-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="137ea-112">Dit is omdat deze taak genereert een JSON-bestand in uw opslagaccount met sleutels en geheimen voor Hallo versleuteld VM toobe hersteld.</span><span class="sxs-lookup"><span data-stu-id="137ea-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="137ea-113">Sleutel en geheime ophalen uit Azure Backup</span><span class="sxs-lookup"><span data-stu-id="137ea-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="137ea-114">Als de schijf is hersteld voor Hallo VM versleuteld, zorg ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="137ea-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="137ea-115">$details is gevuld met restore schijf taakdetails, zoals vermeld in [PowerShell stappen voor het terugzetten Hallo schijven sectie](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="137ea-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="137ea-116">VM moet worden gemaakt van herstelde schijven alleen **nadat de sleutel en geheime is herstelde tookey kluis**.</span><span class="sxs-lookup"><span data-stu-id="137ea-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="137ea-117">Query Hallo schijfeigenschappen voor Hallo taakdetails hersteld.</span><span class="sxs-lookup"><span data-stu-id="137ea-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="137ea-118">Hello Azure storage-context instellen en JSON-configuratiebestand met de sleutel en geheime details voor versleutelde virtuele machine herstellen.</span><span class="sxs-lookup"><span data-stu-id="137ea-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="137ea-119">Sleutel herstellen</span><span class="sxs-lookup"><span data-stu-id="137ea-119">Restore key</span></span>
<span data-ttu-id="137ea-120">Zodra Hallo JSON-bestand wordt gegenereerd in Hallo doelpad bovengenoemde, key blob-bestand genereren van Hallo JSON en toorestore sleutel cmdlet tooput Hallo sleutel (een KEK) terug in de sleutelkluis Hallo feed.</span><span class="sxs-lookup"><span data-stu-id="137ea-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="137ea-121">Geheim herstellen</span><span class="sxs-lookup"><span data-stu-id="137ea-121">Restore secret</span></span>
<span data-ttu-id="137ea-122">Gebruik Hallo JSON-bestand gegenereerd hierboven tooget geheime naam en waarde en tooset geheime cmdlet tooput Hallo geheim (BEK) terug in de sleutelkluis Hallo feed.</span><span class="sxs-lookup"><span data-stu-id="137ea-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="137ea-123">**Deze cmdlets gebruiken als uw VM is versleuteld met behulp van BEK en KEK-sleutel.**</span><span class="sxs-lookup"><span data-stu-id="137ea-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="137ea-124">Als uw virtuele machine wordt **versleuteld met BEK alleen**, geheime blob-bestand genereren van Hallo JSON en toorestore geheime cmdlet tooput Hallo geheim (BEK) terug in de sleutelkluis Hallo feed.</span><span class="sxs-lookup"><span data-stu-id="137ea-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="137ea-125">Waarde voor $secretname kan worden verkregen door te verwijzen toohello uitvoer van $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl en tekst na geheimen / uitvoer geheime URL is bijvoorbeeld https://keyvaultname.vault.azure.net/secrets/ B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 en de geheime naam is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="137ea-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="137ea-126">Waarde van Hallo tag DiskEncryptionKeyFileName is hetzelfde als de geheime naam.</span><span class="sxs-lookup"><span data-stu-id="137ea-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="137ea-127">Virtuele machine van de herstelde schijf maken</span><span class="sxs-lookup"><span data-stu-id="137ea-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="137ea-128">Als u reservekopie versleutelde VM die gebruikmaakt van Azure VM-back-up hebt gemaakt, bovengenoemde Hallo PowerShell-cmdlets help herstellen van sleutel en geheime back toohello sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="137ea-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="137ea-129">Raadpleeg nadat deze is teruggezet, Hallo artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate virtuele machines van de herstelde schijf, sleutel en geheime versleuteld.</span><span class="sxs-lookup"><span data-stu-id="137ea-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="137ea-130">Verouderde benadering</span><span class="sxs-lookup"><span data-stu-id="137ea-130">Legacy approach</span></span>
<span data-ttu-id="137ea-131">Hallo-benadering bovengenoemde zou werken voor alle Hallo-herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="137ea-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="137ea-132">Echter hello oudere benadering van sleutel en geheime informatie ophalen van herstelpunt, zou zijn geldig voor de herstelpunten die ouder zijn dan 11 juli 2017 voor virtuele machines die zijn versleuteld met BEK en KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="137ea-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="137ea-133">Zodra de hersteltaak voor de schijf is voltooid voor het gebruik van versleutelde VM [PowerShell stappen](backup-azure-vms-automation.md#restore-an-azure-vm), zorg ervoor dat $rp is gevuld met een geldige waarde.</span><span class="sxs-lookup"><span data-stu-id="137ea-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="137ea-134">Sleutel herstellen</span><span class="sxs-lookup"><span data-stu-id="137ea-134">Restore key</span></span>
<span data-ttu-id="137ea-135">Hallo volgende cmdlets tooget sleutel (een KEK) informatie uit herstelpunt gebruiken en voer deze toorestore sleutel cmdlet tooput weer in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="137ea-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="137ea-136">Geheim herstellen</span><span class="sxs-lookup"><span data-stu-id="137ea-136">Restore secret</span></span>
<span data-ttu-id="137ea-137">Hallo volgende cmdlets tooget geheim (BEK) informatie uit herstelpunt gebruiken en voer deze tooset geheime cmdlet tooput weer in de sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="137ea-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="137ea-138">Waarde voor $secretname kan worden verkregen door toohello uitvoer van $rp1 verwijst. KeyAndSecretDetails.SecretUrl en het gebruik van tekst na geheimen / uitvoer geheime URL is bijvoorbeeld https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 en geheime naam is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="137ea-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="137ea-139">Waarde van Hallo tag DiskEncryptionKeyFileName is hetzelfde als de geheime naam.</span><span class="sxs-lookup"><span data-stu-id="137ea-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="137ea-140">Waarde voor DiskEncryptionKeyEncryptionKeyURL kan worden verkregen van de sleutelkluis na Hallo sleutels weer terugzetten en het gebruik van [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="137ea-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="137ea-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="137ea-141">Next steps</span></span>
<span data-ttu-id="137ea-142">Na het terugzetten van de sleutel en geheime back tookey kluis verwijzen Hallo artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate virtuele machines van de herstelde schijf, sleutel en geheime versleuteld.</span><span class="sxs-lookup"><span data-stu-id="137ea-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
