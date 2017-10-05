---
title: Automatische back-up voor SQL Server virtuele Machines (klassiek) | Microsoft Docs
description: 'Verklaart de functie voor automatische back-up voor SQL Server wordt uitgevoerd in Azure Virtual Machines die met Resource Manager. '
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: f7664291c2f45c422d52f682d08dbb67ab32b099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="ea016-103">Automatische back-up voor SQL Server op Azure Virtual Machines (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ea016-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ea016-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ea016-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="ea016-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="ea016-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="ea016-106">Automatische back-up configureert automatisch [Managed Backup naar Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ea016-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="ea016-107">Hiermee kunt u voor het configureren van regelmatige back-ups die gebruikmaken van duurzame Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ea016-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="ea016-108">Automatische back-up is afhankelijk van de [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea016-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ea016-109">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ea016-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ea016-110">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ea016-110">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ea016-111">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ea016-111">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ea016-112">De Resource Manager-versie van dit artikel vindt u [automatische back-up voor SQL Server in Azure Resource Manager voor virtuele Machines](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ea016-112">To view the Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea016-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ea016-113">Prerequisites</span></span>
<span data-ttu-id="ea016-114">Houd rekening met de volgende vereisten voor het gebruik van automatische back-up:</span><span class="sxs-lookup"><span data-stu-id="ea016-114">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="ea016-115">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="ea016-115">**Operating System**:</span></span>

* <span data-ttu-id="ea016-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ea016-116">Windows Server 2012</span></span>
* <span data-ttu-id="ea016-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ea016-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ea016-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ea016-118">Windows Server 2016</span></span>

<span data-ttu-id="ea016-119">**SQL Server-versie /-editie**:</span><span class="sxs-lookup"><span data-stu-id="ea016-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="ea016-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="ea016-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="ea016-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="ea016-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="ea016-122">SQL Server 2016 is nog niet ondersteund voor automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="ea016-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="ea016-123">**Databaseconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="ea016-123">**Database configuration**:</span></span>

* <span data-ttu-id="ea016-124">Doeldatabases moeten het volledige herstelmodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ea016-124">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="ea016-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="ea016-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="ea016-126">[Installeer de nieuwste Azure PowerShell-opdrachten](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ea016-126">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="ea016-127">**Uitbreiding van SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="ea016-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="ea016-128">[Installeer de SQL Server IaaS-extensie](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ea016-128">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="ea016-129">Instellingen</span><span class="sxs-lookup"><span data-stu-id="ea016-129">Settings</span></span>
<span data-ttu-id="ea016-130">De volgende tabel beschrijft de opties die kunnen worden geconfigureerd voor automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="ea016-130">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="ea016-131">Voor klassieke virtuele machines, moet u PowerShell gebruiken om deze instellingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="ea016-131">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="ea016-132">Instelling</span><span class="sxs-lookup"><span data-stu-id="ea016-132">Setting</span></span> | <span data-ttu-id="ea016-133">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="ea016-133">Range (Default)</span></span> | <span data-ttu-id="ea016-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ea016-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ea016-135">**Automatische back-up**</span><span class="sxs-lookup"><span data-stu-id="ea016-135">**Automated Backup**</span></span> |<span data-ttu-id="ea016-136">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="ea016-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="ea016-137">Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise of.</span><span class="sxs-lookup"><span data-stu-id="ea016-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="ea016-138">**Bewaarperiode**</span><span class="sxs-lookup"><span data-stu-id="ea016-138">**Retention Period**</span></span> |<span data-ttu-id="ea016-139">1 tot 30 dagen (30 dagen)</span><span class="sxs-lookup"><span data-stu-id="ea016-139">1-30 days (30 days)</span></span> |<span data-ttu-id="ea016-140">Het aantal dagen wilt bewaren van een back-up.</span><span class="sxs-lookup"><span data-stu-id="ea016-140">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="ea016-141">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="ea016-141">**Storage Account**</span></span> |<span data-ttu-id="ea016-142">Azure storage-account (de storage-account voor de opgegeven virtuele machine gemaakt)</span><span class="sxs-lookup"><span data-stu-id="ea016-142">Azure storage account (the storage account created for the specified VM)</span></span> |<span data-ttu-id="ea016-143">Een Azure storage-account moet worden gebruikt voor het opslaan van automatische back-up-bestanden in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ea016-143">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="ea016-144">Een container is gemaakt op deze locatie voor het opslaan van alle back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="ea016-144">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="ea016-145">De naamconventie voor back-upbestand bevat de datum, tijd en de machinenaam van de.</span><span class="sxs-lookup"><span data-stu-id="ea016-145">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="ea016-146">**Versleuteling**</span><span class="sxs-lookup"><span data-stu-id="ea016-146">**Encryption**</span></span> |<span data-ttu-id="ea016-147">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="ea016-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="ea016-148">Hiermee schakelt versleuteling of.</span><span class="sxs-lookup"><span data-stu-id="ea016-148">Enables or disables encryption.</span></span> <span data-ttu-id="ea016-149">Bij versleuteling is ingeschakeld, worden de certificaten voor de back-up herstellen in het opgegeven opslagaccount in dezelfde automaticbackup container met de dezelfde naamgevingsregel gevonden.</span><span class="sxs-lookup"><span data-stu-id="ea016-149">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span></span> <span data-ttu-id="ea016-150">Als het wachtwoord wordt gewijzigd, wordt een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat blijft voor het herstellen van eerdere back-ups.</span><span class="sxs-lookup"><span data-stu-id="ea016-150">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="ea016-151">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="ea016-151">**Password**</span></span> |<span data-ttu-id="ea016-152">Wachtwoord tekst (geen)</span><span class="sxs-lookup"><span data-stu-id="ea016-152">Password text (None)</span></span> |<span data-ttu-id="ea016-153">Een wachtwoord voor versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="ea016-153">A password for encryption keys.</span></span> <span data-ttu-id="ea016-154">Dit is alleen vereist als versleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ea016-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="ea016-155">Om een versleutelde back-up herstellen, moet u het juiste wachtwoord en het bijbehorende certificaat dat is gebruikt op het moment dat de back-up is gehaald hebben.</span><span class="sxs-lookup"><span data-stu-id="ea016-155">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> | <span data-ttu-id="ea016-156">**Back-upsysteem databases**</span><span class="sxs-lookup"><span data-stu-id="ea016-156">**Backup system databases**</span></span> | <span data-ttu-id="ea016-157">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="ea016-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="ea016-158">Volledige back-ups van Master, Model en MSDB duren</span><span class="sxs-lookup"><span data-stu-id="ea016-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="ea016-159">**Back-upschema configureren**</span><span class="sxs-lookup"><span data-stu-id="ea016-159">**Configure backup schedule**</span></span> | <span data-ttu-id="ea016-160">Handmatige/geautomatiseerde (geautomatiseerde)</span><span class="sxs-lookup"><span data-stu-id="ea016-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="ea016-161">Selecteer **automatisch** automatisch volledige en logboekback-ups op basis van het logboek groei.</span><span class="sxs-lookup"><span data-stu-id="ea016-161">Select **Automated** to automatically take full and log backups based on log growth.</span></span> <span data-ttu-id="ea016-162">Selecteer **handmatige** om op te geven van de planning voor volledige en logboekback-ups.</span><span class="sxs-lookup"><span data-stu-id="ea016-162">Select **Manual** to specify the schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="ea016-163">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="ea016-163">Configuration with PowerShell</span></span>
<span data-ttu-id="ea016-164">In het volgende PowerShell-voorbeeld is automatische back-up geconfigureerd voor een bestaande SQL Server 2014 VM.</span><span class="sxs-lookup"><span data-stu-id="ea016-164">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="ea016-165">De **nieuw AzureVMSqlServerAutoBackupConfig** opdracht configureert u de instellingen voor automatische back-up voor het opslaan van back-ups in de Azure storage-account dat is opgegeven door de variabele $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="ea016-165">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span></span> <span data-ttu-id="ea016-166">Deze back-ups voor 10 dagen bewaard.</span><span class="sxs-lookup"><span data-stu-id="ea016-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="ea016-167">De **Set AzureVMSqlServerExtension** opdracht opgegeven Azure virtuele machine wordt bijgewerkt met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="ea016-167">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="ea016-168">Dit kan enige tijd duren om te installeren en configureren van de SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="ea016-168">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="ea016-169">Het inschakelen van versleuteling het vorige script wijzigen voor de parameter EnableEncryption samen met een wachtwoord (beveiligde tekenreeks) voor de parameter CertificatePassword doorgeven.</span><span class="sxs-lookup"><span data-stu-id="ea016-169">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span></span> <span data-ttu-id="ea016-170">Het volgende script kunt de instellingen voor automatische back-up in het vorige voorbeeld en versleuteling wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ea016-170">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="ea016-171">Schakel automatische back-ups uitvoeren hetzelfde script zonder de **-inschakelen** -parameter voor de **nieuw AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="ea016-171">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="ea016-172">Net als bij de installatie, kan het enkele minuten uitschakelen van automatische back-up duren.</span><span class="sxs-lookup"><span data-stu-id="ea016-172">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="ea016-173">Uitschakelen en verwijderen van de SQL Server IaaS-Agent wordt niet verwijderd van de eerder geconfigureerde instellingen voor Managed Backup.</span><span class="sxs-lookup"><span data-stu-id="ea016-173">Disabling and uninstalling the SQL Server IaaS Agent does not remove the previously configured Managed Backup settings.</span></span> <span data-ttu-id="ea016-174">U moet automatische back-up uitschakelen voordat u het uitschakelen of verwijderen van de SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="ea016-174">You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ea016-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea016-175">Next steps</span></span>
<span data-ttu-id="ea016-176">Automatische back-up configureert Managed Backup op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ea016-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="ea016-177">Daarom is het belangrijk dat [Raadpleeg de documentatie voor Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) om te begrijpen van het gedrag en de gevolgen.</span><span class="sxs-lookup"><span data-stu-id="ea016-177">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="ea016-178">U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp: [back-up en herstel voor SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea016-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="ea016-179">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ea016-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="ea016-180">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ea016-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

