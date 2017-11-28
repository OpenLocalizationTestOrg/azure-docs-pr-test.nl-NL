---
title: Automatische back-up voor SQL Server 2014 Azure Virtual Machines | Microsoft Docs
description: Verklaart de functie voor automatische back-up voor SQL Server 2014 virtuele machines in Azure wordt uitgevoerd. In dit artikel is specifiek voor virtuele machines met behulp van de Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="02dda-104">Automatische back-up voor virtuele Machines (Resource Manager) voor SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="02dda-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="02dda-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="02dda-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="02dda-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="02dda-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="02dda-107">Automatische back-up configureert automatisch [Managed Backup naar Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise.</span><span class="sxs-lookup"><span data-stu-id="02dda-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="02dda-108">Hiermee kunt u voor het configureren van regelmatige back-ups die gebruikmaken van duurzame Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="02dda-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="02dda-109">Automatische back-up is afhankelijk van de [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="02dda-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="02dda-110">Prerequisites</span></span>
<span data-ttu-id="02dda-111">Houd rekening met de volgende vereisten voor het gebruik van automatische back-up:</span><span class="sxs-lookup"><span data-stu-id="02dda-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="02dda-112">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="02dda-112">**Operating System**:</span></span>

- <span data-ttu-id="02dda-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="02dda-113">Windows Server 2012</span></span>
- <span data-ttu-id="02dda-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="02dda-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="02dda-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="02dda-115">Windows Server 2016</span></span>

<span data-ttu-id="02dda-116">**SQL Server-versie /-editie**:</span><span class="sxs-lookup"><span data-stu-id="02dda-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="02dda-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="02dda-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="02dda-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="02dda-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02dda-119">Automatische back-up werkt met SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="02dda-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="02dda-120">Als u SQL Server 2016 gebruikt, kunt u automatische back-up v2 back-up van uw databases.</span><span class="sxs-lookup"><span data-stu-id="02dda-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="02dda-121">Zie voor meer informatie [automatische back-up v2 voor SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="02dda-122">**Databaseconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="02dda-122">**Database configuration**:</span></span>

- <span data-ttu-id="02dda-123">Doeldatabases moeten het volledige herstelmodel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02dda-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="02dda-124">Zie voor meer informatie over de impact van het volledige herstelmodel op back-ups, [back-up onder het volledige herstelmodel](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="02dda-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="02dda-125">Doeldatabases moeten zich op het standaardexemplaar van SQL Server.</span><span class="sxs-lookup"><span data-stu-id="02dda-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="02dda-126">Benoemde exemplaren wordt niet ondersteund door de SQL Server IaaS-extensie.</span><span class="sxs-lookup"><span data-stu-id="02dda-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="02dda-127">**Azure-implementatiemodel**:</span><span class="sxs-lookup"><span data-stu-id="02dda-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="02dda-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="02dda-128">Resource Manager</span></span>

<span data-ttu-id="02dda-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="02dda-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="02dda-130">[Installeer de nieuwste Azure PowerShell-opdrachten](/powershell/azure/overview) als u van plan bent voor het configureren van automatische back-up met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02dda-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="02dda-131">Automatische back-up is afhankelijk van de SQL Server IaaS-Agent-extensie.</span><span class="sxs-lookup"><span data-stu-id="02dda-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="02dda-132">Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="02dda-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="02dda-133">Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="02dda-134">Instellingen</span><span class="sxs-lookup"><span data-stu-id="02dda-134">Settings</span></span>

<span data-ttu-id="02dda-135">De volgende tabel beschrijft de opties die kunnen worden geconfigureerd voor automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="02dda-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="02dda-136">De werkelijke configuratiestappen variëren afhankelijk van of u de Azure portal of Azure Windows PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02dda-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="02dda-137">Instelling</span><span class="sxs-lookup"><span data-stu-id="02dda-137">Setting</span></span> | <span data-ttu-id="02dda-138">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="02dda-138">Range (Default)</span></span> | <span data-ttu-id="02dda-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="02dda-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="02dda-140">**Automatische back-up**</span><span class="sxs-lookup"><span data-stu-id="02dda-140">**Automated Backup**</span></span> | <span data-ttu-id="02dda-141">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="02dda-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="02dda-142">Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise of.</span><span class="sxs-lookup"><span data-stu-id="02dda-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="02dda-143">**Bewaarperiode**</span><span class="sxs-lookup"><span data-stu-id="02dda-143">**Retention Period**</span></span> | <span data-ttu-id="02dda-144">1 tot 30 dagen (30 dagen)</span><span class="sxs-lookup"><span data-stu-id="02dda-144">1-30 days (30 days)</span></span> | <span data-ttu-id="02dda-145">Het aantal dagen wilt bewaren van een back-up.</span><span class="sxs-lookup"><span data-stu-id="02dda-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="02dda-146">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="02dda-146">**Storage Account**</span></span> | <span data-ttu-id="02dda-147">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="02dda-147">Azure storage account</span></span> | <span data-ttu-id="02dda-148">Een Azure storage-account moet worden gebruikt voor het opslaan van automatische back-up-bestanden in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="02dda-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="02dda-149">Een container is gemaakt op deze locatie voor het opslaan van alle back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="02dda-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="02dda-150">De naamconventie voor back-upbestand bevat de datum, tijd en de machinenaam van de.</span><span class="sxs-lookup"><span data-stu-id="02dda-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="02dda-151">**Versleuteling**</span><span class="sxs-lookup"><span data-stu-id="02dda-151">**Encryption**</span></span> | <span data-ttu-id="02dda-152">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="02dda-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="02dda-153">Hiermee schakelt versleuteling of.</span><span class="sxs-lookup"><span data-stu-id="02dda-153">Enables or disables encryption.</span></span> <span data-ttu-id="02dda-154">Als versleuteling is ingeschakeld, de certificaten voor de back-up terugzetten bevinden zich in het opgegeven opslagaccount in dezelfde `automaticbackup` container met behulp van de dezelfde naamgevingsregel.</span><span class="sxs-lookup"><span data-stu-id="02dda-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="02dda-155">Als het wachtwoord wordt gewijzigd, wordt een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat blijft voor het herstellen van eerdere back-ups.</span><span class="sxs-lookup"><span data-stu-id="02dda-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="02dda-156">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="02dda-156">**Password**</span></span> | <span data-ttu-id="02dda-157">Wachtwoord tekst</span><span class="sxs-lookup"><span data-stu-id="02dda-157">Password text</span></span> | <span data-ttu-id="02dda-158">Een wachtwoord voor versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="02dda-158">A password for encryption keys.</span></span> <span data-ttu-id="02dda-159">Dit is alleen vereist als versleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="02dda-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="02dda-160">Om een versleutelde back-up herstellen, moet u het juiste wachtwoord en het bijbehorende certificaat dat is gebruikt op het moment dat de back-up is gehaald hebben.</span><span class="sxs-lookup"><span data-stu-id="02dda-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="02dda-161">De configuratie in de Portal</span><span class="sxs-lookup"><span data-stu-id="02dda-161">Configuration in the Portal</span></span>

<span data-ttu-id="02dda-162">U kunt de Azure portal gebruiken voor het configureren van automatische back-up tijdens het inrichten of voor een bestaande SQL Server 2014 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="02dda-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="02dda-163">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="02dda-163">New VMs</span></span>

<span data-ttu-id="02dda-164">De Azure portal gebruiken voor automatische back-up configureren wanneer u een nieuwe virtuele Machine van SQL Server 2014 in het Resource Manager-implementatiemodel maakt.</span><span class="sxs-lookup"><span data-stu-id="02dda-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="02dda-165">In de **SQL Server-instellingen** blade Selecteer **automatische back-up**.</span><span class="sxs-lookup"><span data-stu-id="02dda-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="02dda-166">De volgende schermopname van Azure portal bevat de **SQL automatische back-up** blade.</span><span class="sxs-lookup"><span data-stu-id="02dda-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Configuratie SQL automatische back-up in Azure-portal](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="02dda-168">Zie voor context is het volledig onderwerp op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="02dda-169">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="02dda-169">Existing VMs</span></span>

<span data-ttu-id="02dda-170">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="02dda-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="02dda-171">Selecteer vervolgens de **SQL Server-configuratiebestand** sectie van de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="02dda-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="02dda-173">In de **SQL Server-configuratiebestand** blade, klikt u op de **bewerken** knop in de automatische back-sectie.</span><span class="sxs-lookup"><span data-stu-id="02dda-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines configureren](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="02dda-175">Wanneer u klaar bent, klikt u op de **OK** knop aan de onderkant van de **SQL Server-configuratiebestand** blade uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="02dda-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="02dda-176">Als u automatische back-up voor het eerst inschakelt, configureert Azure de SQL Server IaaS-Agent op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="02dda-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="02dda-177">Gedurende deze tijd de Azure-portal mogelijk niet weergegeven of automatische back-up is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="02dda-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="02dda-178">Wacht enkele minuten voor de agent moet worden geïnstalleerd of geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="02dda-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="02dda-179">Daarna wordt de Azure-portal overeenkomen met de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="02dda-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="02dda-180">U kunt ook automatische back-up-met een sjabloon configureren.</span><span class="sxs-lookup"><span data-stu-id="02dda-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="02dda-181">Zie voor meer informatie [Azure quickstart-sjabloon voor automatische back-up](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="02dda-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="02dda-182">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="02dda-182">Configuration with PowerShell</span></span>

<span data-ttu-id="02dda-183">U kunt PowerShell gebruiken voor het configureren van automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="02dda-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="02dda-184">Voordat u begint, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="02dda-184">Before you begin, you must:</span></span>

- <span data-ttu-id="02dda-185">[Download en installeer de nieuwste Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="02dda-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="02dda-186">Open Windows PowerShell en deze koppelen aan uw account.</span><span class="sxs-lookup"><span data-stu-id="02dda-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="02dda-187">U kunt dit doen door de stappen in de [configureren van uw abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sectie van de inrichting onderwerp.</span><span class="sxs-lookup"><span data-stu-id="02dda-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="02dda-188">De uitbreiding voor de SQL-IaaS installeren</span><span class="sxs-lookup"><span data-stu-id="02dda-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="02dda-189">Als u een virtuele machine van SQL Server vanuit de Azure-portal hebt ingericht, de SQL Server IaaS-extensie al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="02dda-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="02dda-190">U kunt bepalen of het voor uw virtuele machine is geïnstalleerd door het aanroepen van **Get-AzureRmVM** opdracht en onderzoek de **extensies** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="02dda-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="02dda-191">Als de uitbreiding van de SQL Server IaaS-Agent is geïnstalleerd, ziet u dat het weergegeven als 'SqlIaaSAgent' of 'SQLIaaSExtension'.</span><span class="sxs-lookup"><span data-stu-id="02dda-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="02dda-192">**ProvisioningState** voor de extensie 'Geslaagd' moet ook worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="02dda-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="02dda-193">Als dit is niet geïnstalleerd of niet ingericht, kunt u deze kunt installeren met de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="02dda-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="02dda-194">Naast de groep van de naam en de bron voor virtuele machine, moet u ook de regio opgeven (**$region**) waarin uw VM zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="02dda-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="02dda-195"><a id="verifysettings"></a>Controleer of de huidige instellingen</span><span class="sxs-lookup"><span data-stu-id="02dda-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="02dda-196">Als u automatische back-up ingeschakeld tijdens het inrichten, kunt u PowerShell gebruiken om te controleren van uw huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="02dda-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="02dda-197">Voer de **Get-AzureRmVMSqlServerExtension** opdracht en bekijk de **AutoBackupSettings** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="02dda-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="02dda-198">Deze krijgt u uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="02dda-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="02dda-199">Als u de uitvoer ziet dat **inschakelen** is ingesteld op **False**, hebt u automatische back-up inschakelen.</span><span class="sxs-lookup"><span data-stu-id="02dda-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="02dda-200">Goed nieuws is dat u inschakelen en configureren van automatische back-up op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="02dda-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="02dda-201">Zie de volgende sectie voor deze informatie.</span><span class="sxs-lookup"><span data-stu-id="02dda-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="02dda-202">Als u de instellingen onmiddellijk na een wijziging selectievakje, is het mogelijk dat u weer de oude configuratiewaarden krijgt.</span><span class="sxs-lookup"><span data-stu-id="02dda-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="02dda-203">Wacht een paar minuten en controleer de instellingen opnieuw om er zeker van te zijn dat uw wijzigingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="02dda-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="02dda-204">Automatische back-up configureren</span><span class="sxs-lookup"><span data-stu-id="02dda-204">Configure Automated Backup</span></span>
<span data-ttu-id="02dda-205">U kunt PowerShell gebruiken om in te schakelen van automatische back-up ook garantie voor de configuratie en het gedrag op elk gewenst moment wijzigen.</span><span class="sxs-lookup"><span data-stu-id="02dda-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="02dda-206">Eerst, selecteer of maak een opslagaccount voor de back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="02dda-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="02dda-207">Het volgende script selecteert een opslagaccount of gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="02dda-207">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="02dda-208">Automatische back-up biedt geen ondersteuning voor back-ups van opslag in premium-opslag, maar het kan duren voordat de back-ups van VM-schijven die met Premium-opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02dda-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="02dda-209">Gebruik vervolgens de **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht inschakelen en configureren van de instellingen voor automatische back-up voor het opslaan van back-ups in de Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="02dda-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="02dda-210">In dit voorbeeld zijn de back-ups ingesteld op 10 dagen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="02dda-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="02dda-211">De tweede opdracht **Set AzureRmVMSqlServerExtension**, updates van de opgegeven Azure-VM met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="02dda-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="02dda-212">Dit kan enige tijd duren om te installeren en configureren van de SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="02dda-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="02dda-213">Er zijn andere instellingen voor **nieuw AzureRmVMSqlServerAutoBackupConfig** die alleen van toepassing op SQL Server 2016 en automatische back-up v2.</span><span class="sxs-lookup"><span data-stu-id="02dda-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="02dda-214">SQL Server 2014 biedt geen ondersteuning voor de volgende instellingen: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, en **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="02dda-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="02dda-215">Als u probeert deze instellingen te configureren op een virtuele machine van SQL Server 2014, er is geen fout, maar kunnen de instellingen niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="02dda-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="02dda-216">Als u het gebruik van deze instellingen op een virtuele machine van SQL Server 2016 wilt, Zie [automatische back-up v2 voor SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="02dda-217">Wijzig het vorige script om door te geven voor het inschakelen van versleuteling de **EnableEncryption** parameter samen met een wachtwoord (beveiligde tekenreeks) op voor de **CertificatePassword** parameter.</span><span class="sxs-lookup"><span data-stu-id="02dda-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="02dda-218">Het volgende script kunt de instellingen voor automatische back-up in het vorige voorbeeld en versleuteling wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="02dda-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="02dda-219">Om te bevestigen dat de instellingen worden toegepast, [de configuratie van de automatische back-up](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="02dda-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="02dda-220">Uitschakelen van automatische back-up</span><span class="sxs-lookup"><span data-stu-id="02dda-220">Disable Automated Backup</span></span>

<span data-ttu-id="02dda-221">Schakel automatische back-up uitvoeren hetzelfde script zonder de **-inschakelen** -parameter voor de **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht.</span><span class="sxs-lookup"><span data-stu-id="02dda-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="02dda-222">Het ontbreken van de **-inschakelen** parameter geeft u de opdracht uit om de functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="02dda-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="02dda-223">Net als bij de installatie, kan het enkele minuten uitschakelen van automatische back-up duren.</span><span class="sxs-lookup"><span data-stu-id="02dda-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="02dda-224">Voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="02dda-224">Example script</span></span>

<span data-ttu-id="02dda-225">Het volgende script geeft een set van variabelen die u aanpassen kunt als u wilt inschakelen en configureren van automatische back-up voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="02dda-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="02dda-226">In het geval is moet u wellicht aanpassen van het script op basis van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="02dda-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="02dda-227">U moet bijvoorbeeld wijzigen als u versleuteling in-of uitschakelen van de back-up van systeemdatabases.</span><span class="sxs-lookup"><span data-stu-id="02dda-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="02dda-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02dda-228">Next steps</span></span>

<span data-ttu-id="02dda-229">Automatische back-up configureert Managed Backup op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="02dda-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="02dda-230">Daarom is het belangrijk dat [Raadpleeg de documentatie voor Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) om te begrijpen van het gedrag en de gevolgen.</span><span class="sxs-lookup"><span data-stu-id="02dda-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="02dda-231">U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp: [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="02dda-232">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="02dda-233">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02dda-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

