---
title: aaaAutomated patchen voor SQL Server-VM's (Resource Manager) | Microsoft Docs
description: Verklaart Hallo automatisch patchen functie voor SQL Server Virtual Machines worden uitgevoerd in Azure Resource Manager gebruiken.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="bc363-103">Automated Patching voor SQL Server in virtuele machines van Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="bc363-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc363-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc363-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="bc363-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="bc363-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="bc363-106">Geautomatiseerde Patching stelt u een onderhoudsvenster voor een virtuele Machine van Azure met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bc363-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="bc363-107">Automatische Updates kunnen alleen worden geïnstalleerd tijdens deze periode.</span><span class="sxs-lookup"><span data-stu-id="bc363-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="bc363-108">Voor SQL Server zorgt deze rescriction systeemupdates en eventuele bijbehorende opnieuw is opgestart op Hallo best mogelijke tijdstip voor Hallo-database optreden.</span><span class="sxs-lookup"><span data-stu-id="bc363-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="bc363-109">Geautomatiseerde Patching is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bc363-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="bc363-110">tooview hello klassieke versie van dit artikel, Zie [automatisch patchen voor SQL Server in Azure virtuele Machines klassieke](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="bc363-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc363-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bc363-111">Prerequisites</span></span>
<span data-ttu-id="bc363-112">toouse automatisch patchen, overweeg Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="bc363-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="bc363-113">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="bc363-113">**Operating System**:</span></span>

* <span data-ttu-id="bc363-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bc363-114">Windows Server 2012</span></span>
* <span data-ttu-id="bc363-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bc363-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="bc363-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bc363-116">Windows Server 2016</span></span>

<span data-ttu-id="bc363-117">**SQL Server-versie**:</span><span class="sxs-lookup"><span data-stu-id="bc363-117">**SQL Server version**:</span></span>

* <span data-ttu-id="bc363-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="bc363-118">SQL Server 2012</span></span>
* <span data-ttu-id="bc363-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="bc363-119">SQL Server 2014</span></span>
* <span data-ttu-id="bc363-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="bc363-120">SQL Server 2016</span></span>

<span data-ttu-id="bc363-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="bc363-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="bc363-122">[Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview) als u van plan tooconfigure bent automatisch patchen met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc363-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="bc363-123">Geautomatiseerde Patching is afhankelijk van Hallo uitbreiding voor SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="bc363-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="bc363-124">Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bc363-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="bc363-125">Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bc363-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="bc363-126">Instellingen</span><span class="sxs-lookup"><span data-stu-id="bc363-126">Settings</span></span>
<span data-ttu-id="bc363-127">Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="bc363-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="bc363-128">de werkelijke configuratiestappen Hallo variëren afhankelijk van of u hello Azure-portal of Azure Windows PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc363-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="bc363-129">Instelling</span><span class="sxs-lookup"><span data-stu-id="bc363-129">Setting</span></span> | <span data-ttu-id="bc363-130">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="bc363-130">Possible values</span></span> | <span data-ttu-id="bc363-131">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc363-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc363-132">**Automatisch patch toepassen**</span><span class="sxs-lookup"><span data-stu-id="bc363-132">**Automated Patching**</span></span> |<span data-ttu-id="bc363-133">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="bc363-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="bc363-134">Hiermee schakelt automatisch patchen voor een virtuele machine van Azure of.</span><span class="sxs-lookup"><span data-stu-id="bc363-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="bc363-135">**Onderhoudsplanning**</span><span class="sxs-lookup"><span data-stu-id="bc363-135">**Maintenance schedule**</span></span> |<span data-ttu-id="bc363-136">Dagelijks, maandag, dinsdag, woensdag, donderdag, vrijdag, zaterdag, zondag</span><span class="sxs-lookup"><span data-stu-id="bc363-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="bc363-137">Hallo-schema voor het downloaden en installeren van Windows, SQL Server en de Microsoft-updates voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bc363-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="bc363-138">**Beginuur van het onderhoud**</span><span class="sxs-lookup"><span data-stu-id="bc363-138">**Maintenance start hour**</span></span> |<span data-ttu-id="bc363-139">0-24</span><span class="sxs-lookup"><span data-stu-id="bc363-139">0-24</span></span> |<span data-ttu-id="bc363-140">Hallo lokale start tijd tooupdate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bc363-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="bc363-141">**Duur van het venster Onderhoud**</span><span class="sxs-lookup"><span data-stu-id="bc363-141">**Maintenance window duration**</span></span> |<span data-ttu-id="bc363-142">30-180</span><span class="sxs-lookup"><span data-stu-id="bc363-142">30-180</span></span> |<span data-ttu-id="bc363-143">het aantal minuten Hallo toegestaan toocomplete Hallo downloaden en installeren van updates.</span><span class="sxs-lookup"><span data-stu-id="bc363-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="bc363-144">**Patch categorie**</span><span class="sxs-lookup"><span data-stu-id="bc363-144">**Patch Category**</span></span> |<span data-ttu-id="bc363-145">Belangrijk</span><span class="sxs-lookup"><span data-stu-id="bc363-145">Important</span></span> |<span data-ttu-id="bc363-146">Hallo categorie van updates toodownload downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="bc363-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="bc363-147">De configuratie in Hallo Portal</span><span class="sxs-lookup"><span data-stu-id="bc363-147">Configuration in hello Portal</span></span>
<span data-ttu-id="bc363-148">U kunt hello Azure portal tooconfigure automatisch patchen tijdens het inrichten of voor een bestaande virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bc363-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="bc363-149">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="bc363-149">New VMs</span></span>
<span data-ttu-id="bc363-150">Gebruik hello Azure portal tooconfigure automatisch patchen wanneer u een nieuwe virtuele Machine van SQL Server in Hallo Resource Manager-implementatiemodel maakt.</span><span class="sxs-lookup"><span data-stu-id="bc363-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="bc363-151">In Hallo **SQL Server-instellingen** blade Selecteer **automatisch patchen**.</span><span class="sxs-lookup"><span data-stu-id="bc363-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="bc363-152">Hallo volgende Azure portal schermafbeelding ziet u Hallo **SQL automatisch patchen** blade.</span><span class="sxs-lookup"><span data-stu-id="bc363-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![SQL automatisch patchen in Azure-portal](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="bc363-154">Zie voor context is voltooid onderwerp Hallo op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bc363-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="bc363-155">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="bc363-155">Existing VMs</span></span>
<span data-ttu-id="bc363-156">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="bc363-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="bc363-157">Selecteer vervolgens Hallo **SQL Server-configuratiebestand** sectie Hallo **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="bc363-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Automatisch patchen van SQL voor bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="bc363-159">In Hallo **SQL Server-configuratiebestand** blade, klikt u op Hallo **bewerken** knop in Hallo automatische toepassing van patches sectie.</span><span class="sxs-lookup"><span data-stu-id="bc363-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Configureer SQL automatisch patchen voor bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="bc363-161">Wanneer u klaar bent, klikt u op Hallo **OK** knop op Hallo Hallo onderaan **SQL Server-configuratiebestand** blade toosave uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="bc363-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="bc363-162">Als u automatisch patchen voor Hallo eerst inschakelen wilt, configureert Azure Hallo SQL Server IaaS-Agent op de achtergrond Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc363-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="bc363-163">Gedurende deze tijd hello Azure-portal mogelijk niet weergegeven dat automatisch patchen is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bc363-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="bc363-164">Wacht enkele minuten voor Hallo agent toobe is geïnstalleerd, geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="bc363-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="bc363-165">Nadat de die hello Azure aangegeven portal Hallo nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="bc363-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="bc363-166">U kunt ook configureren met behulp van een sjabloon automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="bc363-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="bc363-167">Zie voor meer informatie [Azure quickstart-sjabloon voor het automatisch patchen](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="bc363-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="bc363-168">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc363-168">Configuration with PowerShell</span></span>
<span data-ttu-id="bc363-169">Na het inrichten van uw SQL VM Gebruik PowerShell tooconfigure automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="bc363-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="bc363-170">In de Hallo voorbeeld te volgen, PowerShell gebruikte tooconfigure is automatisch patchen op een bestaande SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="bc363-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="bc363-171">Hallo **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** opdracht configureert u een nieuw onderhoudsvenster voor automatische updates.</span><span class="sxs-lookup"><span data-stu-id="bc363-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="bc363-172">Op basis van dit voorbeeld, hello volgende tabel staan Hallo praktisch effect op Hallo doel-virtuele machine van Azure:</span><span class="sxs-lookup"><span data-stu-id="bc363-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="bc363-173">Parameter</span><span class="sxs-lookup"><span data-stu-id="bc363-173">Parameter</span></span> | <span data-ttu-id="bc363-174">Effect</span><span class="sxs-lookup"><span data-stu-id="bc363-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="bc363-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="bc363-175">**DayOfWeek**</span></span> |<span data-ttu-id="bc363-176">Patches elke donderdag geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="bc363-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="bc363-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="bc363-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="bc363-178">Begin updates om 11:00 uur.</span><span class="sxs-lookup"><span data-stu-id="bc363-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="bc363-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="bc363-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="bc363-180">Patches moeten worden geïnstalleerd binnen 120 minuten.</span><span class="sxs-lookup"><span data-stu-id="bc363-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="bc363-181">Op basis van de begintijd hello, moeten ze volledig 13:00 uur.</span><span class="sxs-lookup"><span data-stu-id="bc363-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="bc363-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="bc363-182">**PatchCategory**</span></span> |<span data-ttu-id="bc363-183">Hallo alleen mogelijk instellen voor deze parameter is **belangrijk**.</span><span class="sxs-lookup"><span data-stu-id="bc363-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="bc363-184">Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.</span><span class="sxs-lookup"><span data-stu-id="bc363-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="bc363-185">toodisable automatisch patchen uitvoeren Hallo dezelfde zonder Hallo script **-inschakelen** parameter toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="bc363-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="bc363-186">gebrek aan Hallo Hallo **-inschakelen** parameter signalen Hallo opdracht toodisable Hallo functie.</span><span class="sxs-lookup"><span data-stu-id="bc363-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc363-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc363-187">Next steps</span></span>
<span data-ttu-id="bc363-188">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bc363-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="bc363-189">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc363-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

