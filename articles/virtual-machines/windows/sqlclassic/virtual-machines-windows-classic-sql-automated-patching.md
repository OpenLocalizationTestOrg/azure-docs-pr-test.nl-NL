---
title: Automatisch patchen voor SQL Server-VM's (klassiek) | Microsoft Docs
description: De functie automatisch patchen voor SQL Server virtuele Machines die worden uitgevoerd in Azure met behulp van de klassieke implementatiemodus uitgelegd.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="cdfd6-103">Automatisch patchen voor SQL Server op Azure Virtual Machines (klassiek)</span><span class="sxs-lookup"><span data-stu-id="cdfd6-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cdfd6-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cdfd6-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="cdfd6-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="cdfd6-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="cdfd6-106">Geautomatiseerde Patching stelt u een onderhoudsvenster voor een virtuele Machine van Azure met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="cdfd6-107">Automatische Updates kunnen alleen worden geïnstalleerd tijdens deze periode.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="cdfd6-108">Voor SQL Server, zorgt dit ervoor systeemupdates en eventuele bijbehorende opnieuw is opgestart bij de best mogelijke voor de database optreden.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="cdfd6-109">Geautomatiseerde Patching is afhankelijk van de [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="cdfd6-110">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cdfd6-111">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="cdfd6-112">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="cdfd6-113">De Resource Manager-versie van dit artikel vindt u [automatisch patchen voor SQL Server in Azure Resource Manager voor virtuele Machines](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cdfd6-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cdfd6-114">Prerequisites</span></span>
<span data-ttu-id="cdfd6-115">Voor het gebruik van automatisch patchen, kunt u overwegen de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="cdfd6-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="cdfd6-116">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="cdfd6-116">**Operating System**:</span></span>

* <span data-ttu-id="cdfd6-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="cdfd6-117">Windows Server 2012</span></span>
* <span data-ttu-id="cdfd6-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="cdfd6-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="cdfd6-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cdfd6-119">Windows Server 2016</span></span>

<span data-ttu-id="cdfd6-120">**SQL Server-versie**:</span><span class="sxs-lookup"><span data-stu-id="cdfd6-120">**SQL Server version**:</span></span>

* <span data-ttu-id="cdfd6-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="cdfd6-121">SQL Server 2012</span></span>
* <span data-ttu-id="cdfd6-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="cdfd6-122">SQL Server 2014</span></span>
* <span data-ttu-id="cdfd6-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="cdfd6-123">SQL Server 2016</span></span>

<span data-ttu-id="cdfd6-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="cdfd6-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="cdfd6-125">[Installeer de nieuwste Azure PowerShell-opdrachten](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="cdfd6-126">**Uitbreiding van SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="cdfd6-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="cdfd6-127">[Installeer de SQL Server IaaS-extensie](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="cdfd6-128">Instellingen</span><span class="sxs-lookup"><span data-stu-id="cdfd6-128">Settings</span></span>
<span data-ttu-id="cdfd6-129">De volgende tabel beschrijft de opties die kunnen worden geconfigureerd voor automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="cdfd6-130">Voor klassieke virtuele machines, moet u PowerShell gebruiken om deze instellingen te configureren.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="cdfd6-131">Instelling</span><span class="sxs-lookup"><span data-stu-id="cdfd6-131">Setting</span></span> | <span data-ttu-id="cdfd6-132">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="cdfd6-132">Possible values</span></span> | <span data-ttu-id="cdfd6-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cdfd6-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdfd6-134">**Automatisch patch toepassen**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-134">**Automated Patching**</span></span> |<span data-ttu-id="cdfd6-135">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="cdfd6-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="cdfd6-136">Hiermee schakelt automatisch patchen voor een virtuele machine van Azure of.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="cdfd6-137">**Onderhoudsplanning**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-137">**Maintenance schedule**</span></span> |<span data-ttu-id="cdfd6-138">Dagelijks, maandag, dinsdag, woensdag, donderdag, vrijdag, zaterdag, zondag</span><span class="sxs-lookup"><span data-stu-id="cdfd6-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="cdfd6-139">De planning voor het downloaden en installeren van Windows, SQL Server en de Microsoft-updates voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="cdfd6-140">**Beginuur van het onderhoud**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-140">**Maintenance start hour**</span></span> |<span data-ttu-id="cdfd6-141">0-24</span><span class="sxs-lookup"><span data-stu-id="cdfd6-141">0-24</span></span> |<span data-ttu-id="cdfd6-142">De lokale tijd voor het bijwerken van de virtuele machine start.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="cdfd6-143">**Duur van het venster Onderhoud**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-143">**Maintenance window duration**</span></span> |<span data-ttu-id="cdfd6-144">30-180</span><span class="sxs-lookup"><span data-stu-id="cdfd6-144">30-180</span></span> |<span data-ttu-id="cdfd6-145">Het aantal minuten over toegangsrechten voor het downloaden en installeren van updates te voltooien.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="cdfd6-146">**Patch categorie**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-146">**Patch Category**</span></span> |<span data-ttu-id="cdfd6-147">Belangrijk</span><span class="sxs-lookup"><span data-stu-id="cdfd6-147">Important</span></span> |<span data-ttu-id="cdfd6-148">De categorie van updates te downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="cdfd6-149">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdfd6-149">Configuration with PowerShell</span></span>
<span data-ttu-id="cdfd6-150">In het volgende voorbeeld wordt PowerShell gebruikt automatisch patchen op een bestaande SQL Server-VM configureren.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="cdfd6-151">De **nieuw AzureVMSqlServerAutoPatchingConfig** opdracht configureert u een nieuw onderhoudsvenster voor automatische updates.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="cdfd6-152">Op basis van dit voorbeeld, beschrijft de volgende tabel de praktische gevolgen voor de doel-virtuele machine van Azure:</span><span class="sxs-lookup"><span data-stu-id="cdfd6-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="cdfd6-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="cdfd6-153">Parameter</span></span> | <span data-ttu-id="cdfd6-154">Effect</span><span class="sxs-lookup"><span data-stu-id="cdfd6-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="cdfd6-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-155">**DayOfWeek**</span></span> |<span data-ttu-id="cdfd6-156">Patches elke donderdag geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="cdfd6-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="cdfd6-158">Begin updates om 11:00 uur.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="cdfd6-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="cdfd6-160">Patches moeten worden geïnstalleerd binnen 120 minuten.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="cdfd6-161">Op basis van de begintijd, moeten ze volledig 13:00 uur.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="cdfd6-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="cdfd6-162">**PatchCategory**</span></span> |<span data-ttu-id="cdfd6-163">De instelling alleen mogelijk voor deze parameter is 'Belangrijk'.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="cdfd6-164">Dit kan enige tijd duren om te installeren en configureren van de SQL Server IaaS-Agent.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="cdfd6-165">Als u wilt uitschakelen automatisch patchen, voert u de script zonder de - parameter inschakelen voor de nieuw-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="cdfd6-166">Net als bij de installatie, kan het enkele minuten om uit te schakelen automatisch patchen duren.</span><span class="sxs-lookup"><span data-stu-id="cdfd6-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdfd6-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdfd6-167">Next steps</span></span>
<span data-ttu-id="cdfd6-168">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="cdfd6-169">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cdfd6-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

