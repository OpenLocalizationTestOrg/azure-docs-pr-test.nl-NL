---
title: aaaAutomated back-up voor SQL Server Virtual Machines (klassiek) | Microsoft Docs
description: 'Verklaart Hallo automatische back-up-functie voor SQL Server wordt uitgevoerd in Azure Virtual Machines die met Resource Manager. '
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
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="71fbe-103">Automatische back-up voor SQL Server op Azure Virtual Machines (klassiek)</span><span class="sxs-lookup"><span data-stu-id="71fbe-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71fbe-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="71fbe-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="71fbe-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="71fbe-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="71fbe-106">Automatische back-up configureert automatisch [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise.</span><span class="sxs-lookup"><span data-stu-id="71fbe-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="71fbe-107">Hiermee kunt u tooconfigure reguliere databaseback-ups die gebruikmaken van duurzame Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="71fbe-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="71fbe-108">Automatische back-up, is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71fbe-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="71fbe-109">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="71fbe-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="71fbe-110">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="71fbe-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="71fbe-111">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71fbe-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="71fbe-112">tooview hello Resource Manager-versie van dit artikel, Zie [automatische back-up voor SQL Server in Azure Resource Manager voor virtuele Machines](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="71fbe-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71fbe-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="71fbe-113">Prerequisites</span></span>
<span data-ttu-id="71fbe-114">toouse automatische back-up, kunt u overwegen Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="71fbe-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="71fbe-115">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="71fbe-115">**Operating System**:</span></span>

* <span data-ttu-id="71fbe-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="71fbe-116">Windows Server 2012</span></span>
* <span data-ttu-id="71fbe-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="71fbe-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="71fbe-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="71fbe-118">Windows Server 2016</span></span>

<span data-ttu-id="71fbe-119">**SQL Server-versie /-editie**:</span><span class="sxs-lookup"><span data-stu-id="71fbe-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="71fbe-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="71fbe-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="71fbe-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="71fbe-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="71fbe-122">SQL Server 2016 is nog niet ondersteund voor automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="71fbe-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="71fbe-123">**Databaseconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="71fbe-123">**Database configuration**:</span></span>

* <span data-ttu-id="71fbe-124">Doeldatabases moeten het volledige herstelmodel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71fbe-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="71fbe-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="71fbe-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="71fbe-126">[Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="71fbe-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="71fbe-127">**Uitbreiding van SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="71fbe-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="71fbe-128">[Hallo IaaS-uitbreiding voor SQL-Server installeren](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="71fbe-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="71fbe-129">Instellingen</span><span class="sxs-lookup"><span data-stu-id="71fbe-129">Settings</span></span>
<span data-ttu-id="71fbe-130">Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="71fbe-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="71fbe-131">Voor klassieke virtuele machines, moet u PowerShell tooconfigure deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="71fbe-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="71fbe-132">Instelling</span><span class="sxs-lookup"><span data-stu-id="71fbe-132">Setting</span></span> | <span data-ttu-id="71fbe-133">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="71fbe-133">Range (Default)</span></span> | <span data-ttu-id="71fbe-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="71fbe-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="71fbe-135">**Automatische back-up**</span><span class="sxs-lookup"><span data-stu-id="71fbe-135">**Automated Backup**</span></span> |<span data-ttu-id="71fbe-136">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="71fbe-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="71fbe-137">Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise of.</span><span class="sxs-lookup"><span data-stu-id="71fbe-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="71fbe-138">**Bewaarperiode**</span><span class="sxs-lookup"><span data-stu-id="71fbe-138">**Retention Period**</span></span> |<span data-ttu-id="71fbe-139">1 tot 30 dagen (30 dagen)</span><span class="sxs-lookup"><span data-stu-id="71fbe-139">1-30 days (30 days)</span></span> |<span data-ttu-id="71fbe-140">Hallo aantal dagen tooretain een back-up.</span><span class="sxs-lookup"><span data-stu-id="71fbe-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="71fbe-141">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="71fbe-141">**Storage Account**</span></span> |<span data-ttu-id="71fbe-142">Azure storage-account (Hallo storage-account voor Hallo virtuele machine opgegeven hebt gemaakt)</span><span class="sxs-lookup"><span data-stu-id="71fbe-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="71fbe-143">Een Azure storage-account toouse voor automatische back-up bestanden opslaan in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="71fbe-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="71fbe-144">Een container is gemaakt op deze locatie toostore alle back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="71fbe-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="71fbe-145">de back-upbestand Hallo naamgevingsconventie omvat Hallo datum, tijd en de machinenaam van de.</span><span class="sxs-lookup"><span data-stu-id="71fbe-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="71fbe-146">**Versleuteling**</span><span class="sxs-lookup"><span data-stu-id="71fbe-146">**Encryption**</span></span> |<span data-ttu-id="71fbe-147">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="71fbe-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="71fbe-148">Hiermee schakelt versleuteling of.</span><span class="sxs-lookup"><span data-stu-id="71fbe-148">Enables or disables encryption.</span></span> <span data-ttu-id="71fbe-149">Als versleuteling is ingeschakeld, Hallo certificaten Hallo back-up gebruikte toorestore bevinden zich in Hallo storage-account opgegeven in Hallo hetzelfde automaticbackup container gebruikt dezelfde naamgevingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="71fbe-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="71fbe-150">Als Hallo wachtwoord wordt gewijzigd, een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat Hallo blijft toorestore eerdere back-ups.</span><span class="sxs-lookup"><span data-stu-id="71fbe-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="71fbe-151">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="71fbe-151">**Password**</span></span> |<span data-ttu-id="71fbe-152">Wachtwoord tekst (geen)</span><span class="sxs-lookup"><span data-stu-id="71fbe-152">Password text (None)</span></span> |<span data-ttu-id="71fbe-153">Een wachtwoord voor versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="71fbe-153">A password for encryption keys.</span></span> <span data-ttu-id="71fbe-154">Dit is alleen vereist als versleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="71fbe-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="71fbe-155">In volgorde toorestore een versleutelde back-up, hebt u het juiste wachtwoord Hallo en verwante certificaat dat is gebruikt tijdens het Hallo Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71fbe-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="71fbe-156">**Back-upsysteem databases**</span><span class="sxs-lookup"><span data-stu-id="71fbe-156">**Backup system databases**</span></span> | <span data-ttu-id="71fbe-157">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="71fbe-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="71fbe-158">Volledige back-ups van Master, Model en MSDB duren</span><span class="sxs-lookup"><span data-stu-id="71fbe-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="71fbe-159">**Back-upschema configureren**</span><span class="sxs-lookup"><span data-stu-id="71fbe-159">**Configure backup schedule**</span></span> | <span data-ttu-id="71fbe-160">Handmatige/geautomatiseerde (geautomatiseerde)</span><span class="sxs-lookup"><span data-stu-id="71fbe-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="71fbe-161">Selecteer **automatisch** tooautomatically duren volledige en logboekback-ups op basis van het logboek groei.</span><span class="sxs-lookup"><span data-stu-id="71fbe-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="71fbe-162">Selecteer **handmatige** toospecify Hallo planning voor volledige en logboekback-ups.</span><span class="sxs-lookup"><span data-stu-id="71fbe-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="71fbe-163">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="71fbe-163">Configuration with PowerShell</span></span>
<span data-ttu-id="71fbe-164">In de Hallo PowerShell-voorbeeld te volgen, is automatische back-up geconfigureerd voor een bestaande SQL Server 2014 VM.</span><span class="sxs-lookup"><span data-stu-id="71fbe-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="71fbe-165">Hallo **nieuw AzureVMSqlServerAutoBackupConfig** opdracht Hallo automatische back-up instellingen toostore back-ups in hello Azure storage-account is opgegeven door de variabele Hallo $storageaccount configureert.</span><span class="sxs-lookup"><span data-stu-id="71fbe-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="71fbe-166">Deze back-ups voor 10 dagen bewaard.</span><span class="sxs-lookup"><span data-stu-id="71fbe-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="71fbe-167">Hallo **Set AzureVMSqlServerExtension** opdracht updates Hallo opgegeven virtuele machine van Azure met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="71fbe-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="71fbe-168">Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.</span><span class="sxs-lookup"><span data-stu-id="71fbe-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="71fbe-169">tooenable versleuteling, Hallo vorige toopass hello EnableEncryption scriptparameter samen met een wachtwoord (beveiligde tekenreeks) wijzigen voor Hallo CertificatePassword-parameter.</span><span class="sxs-lookup"><span data-stu-id="71fbe-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="71fbe-170">Hallo volgende script Hiermee Hallo automatische back-up-instellingen in het vorige voorbeeld Hallo en versleuteling wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="71fbe-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="71fbe-171">toodisable automatische back-up uitvoeren Hallo dezelfde zonder Hallo script **-inschakelen** parameter toohello **nieuw AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="71fbe-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="71fbe-172">Net als bij de installatie kan enkele minuten toodisable automatische back-up duren.</span><span class="sxs-lookup"><span data-stu-id="71fbe-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="71fbe-173">Verwijdert geen Hallo eerder geconfigureerde back-up beheerde instellingen uit te schakelen en Hallo SQL Server IaaS-Agent verwijderen.</span><span class="sxs-lookup"><span data-stu-id="71fbe-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="71fbe-174">U moet automatische back-up uitschakelen voordat u het uitschakelen of verwijderen van Hallo SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="71fbe-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="71fbe-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71fbe-175">Next steps</span></span>
<span data-ttu-id="71fbe-176">Automatische back-up configureert Managed Backup op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="71fbe-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="71fbe-177">Dus is het belangrijk te[Hallo-documentatie voor back-up beheerd lezen](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hallo gedrag en de gevolgen.</span><span class="sxs-lookup"><span data-stu-id="71fbe-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="71fbe-178">U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp Hallo: [back-up en herstel voor SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71fbe-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="71fbe-179">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="71fbe-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="71fbe-180">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71fbe-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

