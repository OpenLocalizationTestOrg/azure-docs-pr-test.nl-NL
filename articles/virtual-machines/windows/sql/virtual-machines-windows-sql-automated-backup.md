---
title: aaaAutomated back-up voor SQL Server 2014 Azure Virtual Machines | Microsoft Docs
description: Verklaart Hallo automatische back-up-functie voor SQL Server 2014 virtuele machines in Azure wordt uitgevoerd. Dit artikel is een specifieke tooVMs met Hallo Resource Manager.
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="3afdd-104">Automatische back-up voor virtuele Machines (Resource Manager) voor SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="3afdd-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3afdd-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="3afdd-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="3afdd-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="3afdd-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="3afdd-107">Automatische back-up configureert automatisch [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) voor alle bestaande en nieuwe databases op een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3afdd-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="3afdd-108">Hiermee kunt u tooconfigure reguliere databaseback-ups die gebruikmaken van duurzame Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="3afdd-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="3afdd-109">Automatische back-up, is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="3afdd-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3afdd-110">Prerequisites</span></span>
<span data-ttu-id="3afdd-111">toouse automatische back-up, kunt u overwegen Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="3afdd-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="3afdd-112">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="3afdd-112">**Operating System**:</span></span>

- <span data-ttu-id="3afdd-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3afdd-113">Windows Server 2012</span></span>
- <span data-ttu-id="3afdd-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3afdd-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="3afdd-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3afdd-115">Windows Server 2016</span></span>

<span data-ttu-id="3afdd-116">**SQL Server-versie /-editie**:</span><span class="sxs-lookup"><span data-stu-id="3afdd-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="3afdd-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="3afdd-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="3afdd-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="3afdd-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3afdd-119">Automatische back-up werkt met SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="3afdd-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="3afdd-120">Als u SQL Server 2016 gebruikt, kunt u automatische back-up v2 tooback van uw databases.</span><span class="sxs-lookup"><span data-stu-id="3afdd-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="3afdd-121">Zie voor meer informatie [automatische back-up v2 voor SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="3afdd-122">**Databaseconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="3afdd-122">**Database configuration**:</span></span>

- <span data-ttu-id="3afdd-123">Doeldatabases moeten het volledige herstelmodel hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3afdd-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="3afdd-124">Zie voor meer informatie over Hallo impact van het volledige herstelmodel Hallo op back-ups [back-up onder Hallo volledig herstelmodel](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="3afdd-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="3afdd-125">Doeldatabases zich op Hallo standaard SQL Server-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="3afdd-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="3afdd-126">Hallo IaaS-uitbreiding voor SQL Server biedt geen ondersteuning voor benoemde exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3afdd-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="3afdd-127">**Azure-implementatiemodel**:</span><span class="sxs-lookup"><span data-stu-id="3afdd-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="3afdd-128">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3afdd-128">Resource Manager</span></span>

<span data-ttu-id="3afdd-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="3afdd-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="3afdd-130">[Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview) als u van plan tooconfigure automatische back-up met PowerShell bent.</span><span class="sxs-lookup"><span data-stu-id="3afdd-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="3afdd-131">Automatische back-up, is afhankelijk van Hallo uitbreiding voor SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="3afdd-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="3afdd-132">Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3afdd-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="3afdd-133">Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="3afdd-134">Instellingen</span><span class="sxs-lookup"><span data-stu-id="3afdd-134">Settings</span></span>

<span data-ttu-id="3afdd-135">Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="3afdd-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="3afdd-136">de werkelijke configuratiestappen Hallo variëren afhankelijk van of u hello Azure-portal of Azure Windows PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3afdd-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="3afdd-137">Instelling</span><span class="sxs-lookup"><span data-stu-id="3afdd-137">Setting</span></span> | <span data-ttu-id="3afdd-138">Bereik (standaard)</span><span class="sxs-lookup"><span data-stu-id="3afdd-138">Range (Default)</span></span> | <span data-ttu-id="3afdd-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3afdd-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3afdd-140">**Automatische back-up**</span><span class="sxs-lookup"><span data-stu-id="3afdd-140">**Automated Backup**</span></span> | <span data-ttu-id="3afdd-141">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="3afdd-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="3afdd-142">Hiermee schakelt automatische back-up voor een virtuele machine in Azure met SQL Server 2014 Standard of Enterprise of.</span><span class="sxs-lookup"><span data-stu-id="3afdd-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="3afdd-143">**Bewaarperiode**</span><span class="sxs-lookup"><span data-stu-id="3afdd-143">**Retention Period**</span></span> | <span data-ttu-id="3afdd-144">1 tot 30 dagen (30 dagen)</span><span class="sxs-lookup"><span data-stu-id="3afdd-144">1-30 days (30 days)</span></span> | <span data-ttu-id="3afdd-145">Hallo aantal dagen tooretain een back-up.</span><span class="sxs-lookup"><span data-stu-id="3afdd-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="3afdd-146">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="3afdd-146">**Storage Account**</span></span> | <span data-ttu-id="3afdd-147">Azure Storage-account</span><span class="sxs-lookup"><span data-stu-id="3afdd-147">Azure storage account</span></span> | <span data-ttu-id="3afdd-148">Een Azure storage-account toouse voor automatische back-up bestanden opslaan in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="3afdd-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="3afdd-149">Een container is gemaakt op deze locatie toostore alle back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="3afdd-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="3afdd-150">de back-upbestand Hallo naamgevingsconventie omvat Hallo datum, tijd en de machinenaam van de.</span><span class="sxs-lookup"><span data-stu-id="3afdd-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="3afdd-151">**Versleuteling**</span><span class="sxs-lookup"><span data-stu-id="3afdd-151">**Encryption**</span></span> | <span data-ttu-id="3afdd-152">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="3afdd-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="3afdd-153">Hiermee schakelt versleuteling of.</span><span class="sxs-lookup"><span data-stu-id="3afdd-153">Enables or disables encryption.</span></span> <span data-ttu-id="3afdd-154">Als versleuteling is ingeschakeld, Hallo certificaten gebruikt toorestore Hallo back-up bevinden zich in de opgegeven Hallo storage-account in Hallo dezelfde `automaticbackup` container met behulp van dezelfde naamgevingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="3afdd-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="3afdd-155">Als Hallo wachtwoord wordt gewijzigd, een nieuw certificaat wordt gegenereerd met dit wachtwoord, maar het oude certificaat Hallo blijft toorestore eerdere back-ups.</span><span class="sxs-lookup"><span data-stu-id="3afdd-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="3afdd-156">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="3afdd-156">**Password**</span></span> | <span data-ttu-id="3afdd-157">Wachtwoord tekst</span><span class="sxs-lookup"><span data-stu-id="3afdd-157">Password text</span></span> | <span data-ttu-id="3afdd-158">Een wachtwoord voor versleutelingssleutels.</span><span class="sxs-lookup"><span data-stu-id="3afdd-158">A password for encryption keys.</span></span> <span data-ttu-id="3afdd-159">Dit is alleen vereist als versleuteling is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3afdd-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="3afdd-160">In volgorde toorestore een versleutelde back-up, hebt u het juiste wachtwoord Hallo en verwante certificaat dat is gebruikt tijdens het Hallo Hallo back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3afdd-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="3afdd-161">De configuratie in Hallo Portal</span><span class="sxs-lookup"><span data-stu-id="3afdd-161">Configuration in hello Portal</span></span>

<span data-ttu-id="3afdd-162">U kunt hello Azure portal tooconfigure automatische back-up gebruiken tijdens het inrichten of voor een bestaande SQL Server 2014 virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3afdd-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="3afdd-163">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="3afdd-163">New VMs</span></span>

<span data-ttu-id="3afdd-164">Hello Azure portal tooconfigure automatische back-up gebruiken bij het maken van een nieuwe virtuele Machine van SQL Server 2014 in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3afdd-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="3afdd-165">In Hallo **SQL Server-instellingen** blade Selecteer **automatische back-up**.</span><span class="sxs-lookup"><span data-stu-id="3afdd-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="3afdd-166">Hallo volgende Azure portal schermafbeelding ziet u Hallo **SQL automatische back-up** blade.</span><span class="sxs-lookup"><span data-stu-id="3afdd-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuratie SQL automatische back-up in Azure-portal](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="3afdd-168">Zie voor context is voltooid onderwerp Hallo op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="3afdd-169">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="3afdd-169">Existing VMs</span></span>

<span data-ttu-id="3afdd-170">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3afdd-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="3afdd-171">Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="3afdd-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="3afdd-173">In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo automatische back-sectie.</span><span class="sxs-lookup"><span data-stu-id="3afdd-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![SQL automatische back-up voor de bestaande virtuele machines configureren](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="3afdd-175">Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3afdd-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="3afdd-176">Als u automatische back-up voor Hallo eerst inschakelt, configureert Azure Hallo SQL Server IaaS-Agent op de achtergrond Hallo.</span><span class="sxs-lookup"><span data-stu-id="3afdd-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="3afdd-177">Gedurende deze tijd hello Azure-portal mogelijk niet weergegeven of automatische back-up is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3afdd-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="3afdd-178">Wacht enkele minuten voor Hallo agent toobe is geïnstalleerd, geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3afdd-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="3afdd-179">Na deze hello Azure bevatten portal Hallo nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="3afdd-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="3afdd-180">U kunt ook automatische back-up-met een sjabloon configureren.</span><span class="sxs-lookup"><span data-stu-id="3afdd-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="3afdd-181">Zie voor meer informatie [Azure quickstart-sjabloon voor automatische back-up](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="3afdd-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="3afdd-182">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="3afdd-182">Configuration with PowerShell</span></span>

<span data-ttu-id="3afdd-183">U kunt PowerShell tooconfigure automatische back-up gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3afdd-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="3afdd-184">Voordat u begint, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="3afdd-184">Before you begin, you must:</span></span>

- <span data-ttu-id="3afdd-185">[Download en installeer Hallo nieuwste Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="3afdd-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="3afdd-186">Open Windows PowerShell en deze koppelen aan uw account.</span><span class="sxs-lookup"><span data-stu-id="3afdd-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="3afdd-187">U kunt dit doen door de stappen te volgen Hallo in Hallo [configureren van uw abonnement](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) sectie Hallo onderwerp inrichten.</span><span class="sxs-lookup"><span data-stu-id="3afdd-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="3afdd-188">Hallo SQL IaaS-uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="3afdd-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="3afdd-189">Als u een virtuele machine van SQL Server uit hello Azure-portal hebt ingericht, Hallo uitbreiding van SQL Server IaaS al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3afdd-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="3afdd-190">U kunt bepalen of het voor uw virtuele machine is geïnstalleerd door het aanroepen van **Get-AzureRmVM** opdracht en onderzoeken Hallo **extensies** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3afdd-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="3afdd-191">Als Hallo uitbreiding van de SQL Server IaaS-Agent is geïnstalleerd, ziet u dat het weergegeven als 'SqlIaaSAgent' of 'SQLIaaSExtension'.</span><span class="sxs-lookup"><span data-stu-id="3afdd-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="3afdd-192">**ProvisioningState** voor Hallo-uitbreiding moet ook 'Voltooid' weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3afdd-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="3afdd-193">Als deze is niet geïnstalleerd of toobe ingericht mislukt, kunt u deze met de volgende opdracht Hallo installeren.</span><span class="sxs-lookup"><span data-stu-id="3afdd-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="3afdd-194">Toevoeging toohello VM en de bron-groep, moet u ook opgeven Hallo regio (**$region**) waarin uw VM zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="3afdd-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="3afdd-195"><a id="verifysettings"></a>Controleer of de huidige instellingen</span><span class="sxs-lookup"><span data-stu-id="3afdd-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="3afdd-196">Als u automatische back-up ingeschakeld tijdens het inrichten, kunt u PowerShell toocheck uw huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="3afdd-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="3afdd-197">Voer Hallo **Get-AzureRmVMSqlServerExtension** opdracht en bekijk het Hallo **AutoBackupSettings** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="3afdd-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="3afdd-198">U moet uitvoer vergelijkbare toohello volgende krijgen:</span><span class="sxs-lookup"><span data-stu-id="3afdd-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="3afdd-199">Als u de uitvoer ziet dat **inschakelen** te is ingesteld,**False**, hebt u tooenable automatische back-up.</span><span class="sxs-lookup"><span data-stu-id="3afdd-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="3afdd-200">Hallo goed nieuws is dat u inschakelen en configureren van automatische back-up in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="3afdd-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="3afdd-201">Zie de volgende sectie Hallo voor deze informatie.</span><span class="sxs-lookup"><span data-stu-id="3afdd-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="3afdd-202">Als u instellingen Hallo onmiddellijk na een wijziging selectievakje, is het mogelijk dat u terug Hallo oude configuratiewaarden krijgt.</span><span class="sxs-lookup"><span data-stu-id="3afdd-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="3afdd-203">Wacht een paar minuten en controleer de instellingen van Hallo opnieuw toomake ervoor dat uw wijzigingen zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="3afdd-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="3afdd-204">Automatische back-up configureren</span><span class="sxs-lookup"><span data-stu-id="3afdd-204">Configure Automated Backup</span></span>
<span data-ttu-id="3afdd-205">U kunt PowerShell tooenable automatische back-up, evenals toomodify de configuratie en het gedrag op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="3afdd-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="3afdd-206">Eerst, selecteer of maak een opslagaccount voor Hallo back-upbestanden.</span><span class="sxs-lookup"><span data-stu-id="3afdd-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="3afdd-207">Hallo volgende script selecteert een opslagaccount of gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="3afdd-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="3afdd-208">Automatische back-up biedt geen ondersteuning voor back-ups van opslag in premium-opslag, maar het kan duren voordat de back-ups van VM-schijven die met Premium-opslag gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3afdd-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="3afdd-209">Gebruik vervolgens Hallo **nieuw AzureRmVMSqlServerAutoBackupConfig** tooenable opdracht en Hallo automatische back-up instellingen toostore back-ups in hello Azure storage-account configureren.</span><span class="sxs-lookup"><span data-stu-id="3afdd-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="3afdd-210">In dit voorbeeld worden back-ups Hallo ingesteld toobe 10 dagen bewaard.</span><span class="sxs-lookup"><span data-stu-id="3afdd-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="3afdd-211">tweede opdracht Hallo **Set AzureRmVMSqlServerExtension**, updates Hallo opgegeven virtuele machine van Azure met deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="3afdd-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="3afdd-212">Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.</span><span class="sxs-lookup"><span data-stu-id="3afdd-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="3afdd-213">Er zijn andere instellingen voor **nieuw AzureRmVMSqlServerAutoBackupConfig** die van toepassing zijn alleen tooSQL Server 2016 en automatische back-up v2.</span><span class="sxs-lookup"><span data-stu-id="3afdd-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="3afdd-214">Hallo instellingen na biedt geen ondersteuning voor SQL Server 2014: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, en **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="3afdd-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="3afdd-215">Als u deze instellingen op een virtuele machine van SQL Server 2014 tooconfigure probeert, er is geen fout, maar komen Hallo-instellingen niet toegepast.</span><span class="sxs-lookup"><span data-stu-id="3afdd-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="3afdd-216">Als u deze instellingen op een virtuele machine van SQL Server 2016 toouse wilt, Zie [automatische back-up v2 voor SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="3afdd-217">tooenable versleuteling, Hallo vorige script toopass Hallo wijzigen **EnableEncryption** parameter samen met een wachtwoord (beveiligde tekenreeks) voor Hallo **CertificatePassword** parameter.</span><span class="sxs-lookup"><span data-stu-id="3afdd-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="3afdd-218">Hallo volgende script Hiermee Hallo automatische back-up-instellingen in het vorige voorbeeld Hallo en versleuteling wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3afdd-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="3afdd-219">uw instellingen worden toegepast, tooconfirm [Hallo automatische back-up-configuratie controleren](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="3afdd-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="3afdd-220">Uitschakelen van automatische back-up</span><span class="sxs-lookup"><span data-stu-id="3afdd-220">Disable Automated Backup</span></span>

<span data-ttu-id="3afdd-221">Automatische back-up, Voer Hallo dezelfde script zonder Hallo toodisable **-inschakelen** parameter toohello **nieuw AzureRmVMSqlServerAutoBackupConfig** opdracht.</span><span class="sxs-lookup"><span data-stu-id="3afdd-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="3afdd-222">gebrek aan Hallo Hallo **-inschakelen** parameter signalen Hallo opdracht toodisable Hallo functie.</span><span class="sxs-lookup"><span data-stu-id="3afdd-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="3afdd-223">Net als bij de installatie kan enkele minuten toodisable automatische back-up duren.</span><span class="sxs-lookup"><span data-stu-id="3afdd-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="3afdd-224">Voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="3afdd-224">Example script</span></span>

<span data-ttu-id="3afdd-225">Hallo volgende script geeft een reeks variabelen tooenable aanpassen en het configureren van automatische back-up voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3afdd-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="3afdd-226">In uw geval moet u wellicht toocustomize Hallo script op basis van uw vereisten.</span><span class="sxs-lookup"><span data-stu-id="3afdd-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="3afdd-227">U zou bijvoorbeeld toomake wijzigingen hebben als u deze toodisable Hallo back-up van de systeemdatabases wilde of versleuteling inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3afdd-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="3afdd-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3afdd-228">Next steps</span></span>

<span data-ttu-id="3afdd-229">Automatische back-up configureert Managed Backup op Azure Virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3afdd-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="3afdd-230">Dus is het belangrijk te[Hallo-documentatie voor back-up beheerd lezen](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Hallo gedrag en de gevolgen.</span><span class="sxs-lookup"><span data-stu-id="3afdd-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="3afdd-231">U vindt aanvullende back-up en herstellen van de richtlijnen voor het SQL Server op Azure VM's in het volgende onderwerp Hallo: [back-up en herstel voor SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="3afdd-232">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="3afdd-233">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3afdd-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

