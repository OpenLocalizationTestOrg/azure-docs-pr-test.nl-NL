---
title: Automatisch patchen voor SQL Server-VM's (Resource Manager) | Microsoft Docs
description: Verklaart de functie automatisch patchen voor SQL Server Virtual Machines worden uitgevoerd in Azure Resource Manager gebruiken.
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
ms.openlocfilehash: 7d501ab45a85010a8dbfd6135d77f18f1743354e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="f062f-103">Automated Patching voor SQL Server in virtuele machines van Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="f062f-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f062f-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f062f-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="f062f-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="f062f-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="f062f-106">Geautomatiseerde Patching stelt u een onderhoudsvenster voor een virtuele Machine van Azure met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f062f-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="f062f-107">Automatische Updates kunnen alleen worden geïnstalleerd tijdens deze periode.</span><span class="sxs-lookup"><span data-stu-id="f062f-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="f062f-108">Voor SQL Server zorgt deze rescriction systeemupdates en eventuele bijbehorende opnieuw is opgestart bij de best mogelijke voor de database optreden.</span><span class="sxs-lookup"><span data-stu-id="f062f-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="f062f-109">Geautomatiseerde Patching is afhankelijk van de [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f062f-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="f062f-110">De klassieke versie van dit artikel vindt u [automatisch patchen voor SQL Server in Azure virtuele Machines klassieke](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="f062f-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f062f-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f062f-111">Prerequisites</span></span>
<span data-ttu-id="f062f-112">Voor het gebruik van automatisch patchen, kunt u overwegen de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="f062f-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="f062f-113">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="f062f-113">**Operating System**:</span></span>

* <span data-ttu-id="f062f-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="f062f-114">Windows Server 2012</span></span>
* <span data-ttu-id="f062f-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="f062f-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="f062f-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f062f-116">Windows Server 2016</span></span>

<span data-ttu-id="f062f-117">**SQL Server-versie**:</span><span class="sxs-lookup"><span data-stu-id="f062f-117">**SQL Server version**:</span></span>

* <span data-ttu-id="f062f-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="f062f-118">SQL Server 2012</span></span>
* <span data-ttu-id="f062f-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="f062f-119">SQL Server 2014</span></span>
* <span data-ttu-id="f062f-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="f062f-120">SQL Server 2016</span></span>

<span data-ttu-id="f062f-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="f062f-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="f062f-122">[Installeer de nieuwste Azure PowerShell-opdrachten](/powershell/azure/overview) als u van plan bent automatisch patchen configureren met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f062f-122">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="f062f-123">Er is een geautomatiseerde Patching afhankelijk van de uitbreiding met SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="f062f-123">Automated Patching relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="f062f-124">Huidige SQL-virtuele machine afbeeldingen deze extensie standaard toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f062f-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="f062f-125">Zie voor meer informatie [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f062f-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="f062f-126">Instellingen</span><span class="sxs-lookup"><span data-stu-id="f062f-126">Settings</span></span>
<span data-ttu-id="f062f-127">De volgende tabel beschrijft de opties die kunnen worden geconfigureerd voor automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="f062f-127">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="f062f-128">De werkelijke configuratiestappen variëren afhankelijk van of u de Azure portal of Azure Windows PowerShell-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f062f-128">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="f062f-129">Instelling</span><span class="sxs-lookup"><span data-stu-id="f062f-129">Setting</span></span> | <span data-ttu-id="f062f-130">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="f062f-130">Possible values</span></span> | <span data-ttu-id="f062f-131">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f062f-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f062f-132">**Automatisch patch toepassen**</span><span class="sxs-lookup"><span data-stu-id="f062f-132">**Automated Patching**</span></span> |<span data-ttu-id="f062f-133">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="f062f-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="f062f-134">Hiermee schakelt automatisch patchen voor een virtuele machine van Azure of.</span><span class="sxs-lookup"><span data-stu-id="f062f-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="f062f-135">**Onderhoudsplanning**</span><span class="sxs-lookup"><span data-stu-id="f062f-135">**Maintenance schedule**</span></span> |<span data-ttu-id="f062f-136">Dagelijks, maandag, dinsdag, woensdag, donderdag, vrijdag, zaterdag, zondag</span><span class="sxs-lookup"><span data-stu-id="f062f-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="f062f-137">De planning voor het downloaden en installeren van Windows, SQL Server en de Microsoft-updates voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f062f-137">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="f062f-138">**Beginuur van het onderhoud**</span><span class="sxs-lookup"><span data-stu-id="f062f-138">**Maintenance start hour**</span></span> |<span data-ttu-id="f062f-139">0-24</span><span class="sxs-lookup"><span data-stu-id="f062f-139">0-24</span></span> |<span data-ttu-id="f062f-140">De lokale tijd voor het bijwerken van de virtuele machine start.</span><span class="sxs-lookup"><span data-stu-id="f062f-140">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="f062f-141">**Duur van het venster Onderhoud**</span><span class="sxs-lookup"><span data-stu-id="f062f-141">**Maintenance window duration**</span></span> |<span data-ttu-id="f062f-142">30-180</span><span class="sxs-lookup"><span data-stu-id="f062f-142">30-180</span></span> |<span data-ttu-id="f062f-143">Het aantal minuten over toegangsrechten voor het downloaden en installeren van updates te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f062f-143">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="f062f-144">**Patch categorie**</span><span class="sxs-lookup"><span data-stu-id="f062f-144">**Patch Category**</span></span> |<span data-ttu-id="f062f-145">Belangrijk</span><span class="sxs-lookup"><span data-stu-id="f062f-145">Important</span></span> |<span data-ttu-id="f062f-146">De categorie van updates te downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="f062f-146">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="f062f-147">De configuratie in de Portal</span><span class="sxs-lookup"><span data-stu-id="f062f-147">Configuration in the Portal</span></span>
<span data-ttu-id="f062f-148">U kunt de Azure-portal gebruiken voor het configureren van automatisch patchen tijdens het inrichten of voor een bestaande virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f062f-148">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="f062f-149">Nieuwe virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f062f-149">New VMs</span></span>
<span data-ttu-id="f062f-150">De Azure portal gebruiken voor het automatisch patchen te configureren wanneer u een nieuwe virtuele Machine van SQL Server in het Resource Manager-implementatiemodel maakt.</span><span class="sxs-lookup"><span data-stu-id="f062f-150">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="f062f-151">In de **SQL Server-instellingen** blade Selecteer **automatisch patchen**.</span><span class="sxs-lookup"><span data-stu-id="f062f-151">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="f062f-152">De volgende schermopname van Azure portal bevat de **SQL automatisch patchen** blade.</span><span class="sxs-lookup"><span data-stu-id="f062f-152">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![SQL automatisch patchen in Azure-portal](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="f062f-154">Zie voor context is het volledig onderwerp op [inrichten van een virtuele machine van SQL Server in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="f062f-154">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="f062f-155">Bestaande virtuele machines</span><span class="sxs-lookup"><span data-stu-id="f062f-155">Existing VMs</span></span>
<span data-ttu-id="f062f-156">Selecteer de virtuele machine van SQL Server voor een bestaande SQL Server-virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="f062f-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="f062f-157">Selecteer vervolgens de **SQL Server-configuratiebestand** sectie van de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="f062f-157">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Automatisch patchen van SQL voor bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="f062f-159">In de **SQL Server-configuratiebestand** blade, klikt u op de **bewerken** knop in de sectie patchen automatisch.</span><span class="sxs-lookup"><span data-stu-id="f062f-159">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![Configureer SQL automatisch patchen voor bestaande virtuele machines](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="f062f-161">Wanneer u klaar bent, klikt u op de **OK** knop aan de onderkant van de **SQL Server-configuratiebestand** blade uw wijzigingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="f062f-161">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="f062f-162">Als u automatisch patchen voor het eerst inschakelen wilt, configureert Azure de SQL Server IaaS-Agent op de achtergrond.</span><span class="sxs-lookup"><span data-stu-id="f062f-162">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="f062f-163">Gedurende deze tijd de Azure-portal mogelijk niet weergegeven dat automatisch patchen is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f062f-163">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="f062f-164">Wacht enkele minuten voor de agent moet worden geïnstalleerd of geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f062f-164">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="f062f-165">Daarna de Azure-portal duidt op de nieuwe instellingen.</span><span class="sxs-lookup"><span data-stu-id="f062f-165">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="f062f-166">U kunt ook configureren met behulp van een sjabloon automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="f062f-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="f062f-167">Zie voor meer informatie [Azure quickstart-sjabloon voor het automatisch patchen](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="f062f-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="f062f-168">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="f062f-168">Configuration with PowerShell</span></span>
<span data-ttu-id="f062f-169">Na het inrichten van uw SQL VM PowerShell te gebruiken voor het configureren van automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="f062f-169">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="f062f-170">In het volgende voorbeeld wordt PowerShell gebruikt automatisch patchen op een bestaande SQL Server-VM configureren.</span><span class="sxs-lookup"><span data-stu-id="f062f-170">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="f062f-171">De **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** opdracht configureert u een nieuw onderhoudsvenster voor automatische updates.</span><span class="sxs-lookup"><span data-stu-id="f062f-171">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="f062f-172">Op basis van dit voorbeeld, beschrijft de volgende tabel de praktische gevolgen voor de doel-virtuele machine van Azure:</span><span class="sxs-lookup"><span data-stu-id="f062f-172">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="f062f-173">Parameter</span><span class="sxs-lookup"><span data-stu-id="f062f-173">Parameter</span></span> | <span data-ttu-id="f062f-174">Effect</span><span class="sxs-lookup"><span data-stu-id="f062f-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="f062f-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="f062f-175">**DayOfWeek**</span></span> |<span data-ttu-id="f062f-176">Patches elke donderdag geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f062f-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="f062f-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="f062f-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="f062f-178">Begin updates om 11:00 uur.</span><span class="sxs-lookup"><span data-stu-id="f062f-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="f062f-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="f062f-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="f062f-180">Patches moeten worden geïnstalleerd binnen 120 minuten.</span><span class="sxs-lookup"><span data-stu-id="f062f-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="f062f-181">Op basis van de begintijd, moeten ze volledig 13:00 uur.</span><span class="sxs-lookup"><span data-stu-id="f062f-181">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="f062f-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="f062f-182">**PatchCategory**</span></span> |<span data-ttu-id="f062f-183">De enige mogelijke-instelling voor deze parameter is **belangrijk**.</span><span class="sxs-lookup"><span data-stu-id="f062f-183">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="f062f-184">Dit kan enige tijd duren om te installeren en configureren van de SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="f062f-184">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="f062f-185">Schakel automatisch patchen uitvoeren hetzelfde script zonder de **-inschakelen** -parameter voor de **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="f062f-185">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="f062f-186">Het ontbreken van de **-inschakelen** parameter geeft u de opdracht uit om de functie uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="f062f-186">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f062f-187">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f062f-187">Next steps</span></span>
<span data-ttu-id="f062f-188">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f062f-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="f062f-189">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f062f-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

