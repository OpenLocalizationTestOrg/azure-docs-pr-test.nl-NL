---
title: Sleutelkluis-sleutel en geheime herstellen voor versleutelde virtuele machines maken met Azure Backup | Microsoft Docs
description: Informatie over het herstellen van de Sleutelkluis-sleutel en geheime in Azure back-up met behulp van PowerShell
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
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="57a15-103">Sleutelkluis-sleutel en geheime voor versleutelde VM's met Azure back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="57a15-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="57a15-104">In dit artikel wordt gesproken over het gebruik van Azure VM-back-up voor herstel uitvoeren van versleutelde Azure virtuele machines, als uw sleutel en geheime bestaan niet in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="57a15-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="57a15-105">Deze stappen kunnen ook worden gebruikt als u wilt een afzonderlijk exemplaar van de sleutel (coderingssleutel Key) en geheim (sleutel BitLocker-versleuteling) voor de herstelde virtuele machine te onderhouden.</span><span class="sxs-lookup"><span data-stu-id="57a15-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57a15-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="57a15-106">Prerequisites</span></span>
* <span data-ttu-id="57a15-107">**Back-up van virtuele machines versleuteld** - gecodeerde virtuele machines in Azure back-ups zijn met Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="57a15-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="57a15-108">Raadpleeg het artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md) voor meer informatie over het back-up van versleutelde Azure VM's.</span><span class="sxs-lookup"><span data-stu-id="57a15-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="57a15-109">**Azure Sleutelkluis configureren** : Zorg ervoor dat sleutelkluis waaraan sleutels en geheimen moeten worden hersteld, is al aanwezig.</span><span class="sxs-lookup"><span data-stu-id="57a15-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="57a15-110">Raadpleeg het artikel [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md) voor meer informatie over het beheer van de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="57a15-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="57a15-111">**Herstellen schijf** -Zorg ervoor dat u de hersteltaak voor het herstellen van schijven voor het gebruik van versleutelde VM hebt geactiveerd [PowerShell stappen](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="57a15-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="57a15-112">Dit is omdat deze taak een JSON-bestand in uw opslagaccount met sleutels en geheimen voor de versleutelde virtuele machine genereert moet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="57a15-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="57a15-113">Sleutel en geheime ophalen uit Azure Backup</span><span class="sxs-lookup"><span data-stu-id="57a15-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="57a15-114">Als de schijf voor de versleutelde virtuele machine is hersteld, zorgt ervoor dat:</span><span class="sxs-lookup"><span data-stu-id="57a15-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="57a15-115">$details is gevuld met restore schijf taakdetails, zoals vermeld in [PowerShell stappen voor het terugzetten van de sectie schijven](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="57a15-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="57a15-116">VM moet worden gemaakt van herstelde schijven alleen **nadat sleutel en geheime sleutelkluis weer**.</span><span class="sxs-lookup"><span data-stu-id="57a15-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="57a15-117">De schijfeigenschappen van de herstelde voor de taakdetails opvragen.</span><span class="sxs-lookup"><span data-stu-id="57a15-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="57a15-118">De context van de Azure-opslag instellen en JSON-configuratiebestand met de sleutel en geheime details voor versleutelde virtuele machine herstellen.</span><span class="sxs-lookup"><span data-stu-id="57a15-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="57a15-119">Sleutel herstellen</span><span class="sxs-lookup"><span data-stu-id="57a15-119">Restore key</span></span>
<span data-ttu-id="57a15-120">Zodra het JSON-bestand wordt gegenereerd in het doelpad bovengenoemde, key blob-bestand van de JSON genereren en voer deze voor het herstellen van de belangrijkste cmdlet om de sleutel (KEK-sleutel) terug in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="57a15-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="57a15-121">Geheim herstellen</span><span class="sxs-lookup"><span data-stu-id="57a15-121">Restore secret</span></span>
<span data-ttu-id="57a15-122">Gebruik het JSON-bestand die hierboven worden gegenereerd voor het ophalen van de geheime naam en waarde en voer deze in te stellen geheime cmdlet om het geheim (BEK) terug in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="57a15-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="57a15-123">**Deze cmdlets gebruiken als uw VM is versleuteld met behulp van BEK en KEK-sleutel.**</span><span class="sxs-lookup"><span data-stu-id="57a15-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="57a15-124">Als uw virtuele machine wordt **versleuteld met BEK alleen**, geheime blob-bestand van de JSON genereren en voer deze voor het herstellen van de geheime cmdlet om het geheim (BEK) terug in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="57a15-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="57a15-125">Waarde voor $secretname kan worden verkregen door te verwijzen naar de uitvoer van $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl en tekst na geheimen / uitvoer geheime URL is bijvoorbeeld https://keyvaultname.vault.azure.net/secrets/ B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 en de geheime naam is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="57a15-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="57a15-126">Waarde van de tag DiskEncryptionKeyFileName is hetzelfde als de geheime naam.</span><span class="sxs-lookup"><span data-stu-id="57a15-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="57a15-127">Virtuele machine van de herstelde schijf maken</span><span class="sxs-lookup"><span data-stu-id="57a15-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="57a15-128">Als u reservekopie versleutelde VM die gebruikmaakt van Azure VM-back-up hebt gemaakt, bovengenoemde de PowerShell-cmdlets help dat u sleutel en geheime terug naar de sleutelkluis herstellen.</span><span class="sxs-lookup"><span data-stu-id="57a15-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="57a15-129">Nadat deze is teruggezet, Raadpleeg het artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) versleutelde virtuele machines van de herstelde schijf, sleutel en geheime maken.</span><span class="sxs-lookup"><span data-stu-id="57a15-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="57a15-130">Verouderde benadering</span><span class="sxs-lookup"><span data-stu-id="57a15-130">Legacy approach</span></span>
<span data-ttu-id="57a15-131">De hierboven genoemde benadering zou voor de herstelpunten werken.</span><span class="sxs-lookup"><span data-stu-id="57a15-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="57a15-132">De oudere benadering van sleutel en geheime informatie ophalen van herstelpunt, is ongeldig voor de herstelpunten die ouder zijn dan 11 juli 2017 voor virtuele machines die zijn versleuteld met BEK en KEK-sleutel.</span><span class="sxs-lookup"><span data-stu-id="57a15-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="57a15-133">Zodra de hersteltaak voor de schijf is voltooid voor het gebruik van versleutelde VM [PowerShell stappen](backup-azure-vms-automation.md#restore-an-azure-vm), zorg ervoor dat $rp is gevuld met een geldige waarde.</span><span class="sxs-lookup"><span data-stu-id="57a15-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="57a15-134">Sleutel herstellen</span><span class="sxs-lookup"><span data-stu-id="57a15-134">Restore key</span></span>
<span data-ttu-id="57a15-135">Gebruik de volgende cmdlets sleutelinformatie (KEK-sleutel) van herstelpunt verkrijgen en voer deze voor het herstellen van sleutel-cmdlet om te plaatsen in de sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="57a15-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="57a15-136">Geheim herstellen</span><span class="sxs-lookup"><span data-stu-id="57a15-136">Restore secret</span></span>
<span data-ttu-id="57a15-137">Gebruik de volgende cmdlets uit te halen geheime gegevens van (BEK) herstelpunt en voer deze om in te stellen geheime cmdlet terug in de sleutelkluis te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="57a15-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="57a15-138">Waarde voor $secretname kan worden verkregen door te verwijzen naar de uitvoer van $rp1. KeyAndSecretDetails.SecretUrl en het gebruik van tekst na geheimen / uitvoer geheime URL is bijvoorbeeld https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 en geheime naam is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="57a15-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="57a15-139">Waarde van de tag DiskEncryptionKeyFileName is hetzelfde als de geheime naam.</span><span class="sxs-lookup"><span data-stu-id="57a15-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="57a15-140">Waarde voor DiskEncryptionKeyEncryptionKeyURL kan worden verkregen van de sleutelkluis na het herstellen van de sleutels terug en het gebruik van [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="57a15-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="57a15-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="57a15-141">Next steps</span></span>
<span data-ttu-id="57a15-142">Na het herstellen van sleutel en geheime terug naar sleutelkluis, Raadpleeg het artikel [back-up en herstel van virtuele Azure-machines met behulp van PowerShell beheren](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) versleutelde virtuele machines van de herstelde schijf, sleutel en geheime maken.</span><span class="sxs-lookup"><span data-stu-id="57a15-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>
