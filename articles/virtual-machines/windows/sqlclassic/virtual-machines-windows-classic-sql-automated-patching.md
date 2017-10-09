---
title: aaaAutomated patchen voor SQL Server-VM's (klassiek) | Microsoft Docs
description: Automatisch patchen Hallo-functie voor SQL Server virtuele Machines die worden uitgevoerd in Azure met behulp van de klassieke implementatiemodus Hallo uitgelegd.
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
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="12229-103">Automatisch patchen voor SQL Server op Azure Virtual Machines (klassiek)</span><span class="sxs-lookup"><span data-stu-id="12229-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12229-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="12229-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="12229-105">Klassiek</span><span class="sxs-lookup"><span data-stu-id="12229-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="12229-106">Geautomatiseerde Patching stelt u een onderhoudsvenster voor een virtuele Machine van Azure met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="12229-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="12229-107">Automatische Updates kunnen alleen worden geïnstalleerd tijdens deze periode.</span><span class="sxs-lookup"><span data-stu-id="12229-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="12229-108">Voor SQL Server manier op deze systeemupdates en eventuele bijbehorende opnieuw is opgestart op Hallo best mogelijke tijdstip voor Hallo-database optreden.</span><span class="sxs-lookup"><span data-stu-id="12229-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="12229-109">Geautomatiseerde Patching is afhankelijk van Hallo [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="12229-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="12229-110">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="12229-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="12229-111">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="12229-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="12229-112">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="12229-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="12229-113">tooview hello Resource Manager-versie van dit artikel, Zie [automatisch patchen voor SQL Server in Azure Resource Manager voor virtuele Machines](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="12229-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12229-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="12229-114">Prerequisites</span></span>
<span data-ttu-id="12229-115">toouse automatisch patchen, overweeg Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="12229-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="12229-116">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="12229-116">**Operating System**:</span></span>

* <span data-ttu-id="12229-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="12229-117">Windows Server 2012</span></span>
* <span data-ttu-id="12229-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="12229-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="12229-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="12229-119">Windows Server 2016</span></span>

<span data-ttu-id="12229-120">**SQL Server-versie**:</span><span class="sxs-lookup"><span data-stu-id="12229-120">**SQL Server version**:</span></span>

* <span data-ttu-id="12229-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="12229-121">SQL Server 2012</span></span>
* <span data-ttu-id="12229-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="12229-122">SQL Server 2014</span></span>
* <span data-ttu-id="12229-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="12229-123">SQL Server 2016</span></span>

<span data-ttu-id="12229-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="12229-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="12229-125">[Installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12229-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="12229-126">**Uitbreiding van SQL Server IaaS**:</span><span class="sxs-lookup"><span data-stu-id="12229-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="12229-127">[Hallo IaaS-uitbreiding voor SQL-Server installeren](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="12229-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="12229-128">Instellingen</span><span class="sxs-lookup"><span data-stu-id="12229-128">Settings</span></span>
<span data-ttu-id="12229-129">Hallo beschrijft volgende tabel Hallo-opties die kunnen worden geconfigureerd voor automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="12229-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="12229-130">Voor klassieke virtuele machines, moet u PowerShell tooconfigure deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="12229-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="12229-131">Instelling</span><span class="sxs-lookup"><span data-stu-id="12229-131">Setting</span></span> | <span data-ttu-id="12229-132">Mogelijke waarden</span><span class="sxs-lookup"><span data-stu-id="12229-132">Possible values</span></span> | <span data-ttu-id="12229-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="12229-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="12229-134">**Automatisch patch toepassen**</span><span class="sxs-lookup"><span data-stu-id="12229-134">**Automated Patching**</span></span> |<span data-ttu-id="12229-135">In-of uitschakelen (uitgeschakeld)</span><span class="sxs-lookup"><span data-stu-id="12229-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="12229-136">Hiermee schakelt automatisch patchen voor een virtuele machine van Azure of.</span><span class="sxs-lookup"><span data-stu-id="12229-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="12229-137">**Onderhoudsplanning**</span><span class="sxs-lookup"><span data-stu-id="12229-137">**Maintenance schedule**</span></span> |<span data-ttu-id="12229-138">Dagelijks, maandag, dinsdag, woensdag, donderdag, vrijdag, zaterdag, zondag</span><span class="sxs-lookup"><span data-stu-id="12229-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="12229-139">Hallo-schema voor het downloaden en installeren van Windows, SQL Server en de Microsoft-updates voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12229-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="12229-140">**Beginuur van het onderhoud**</span><span class="sxs-lookup"><span data-stu-id="12229-140">**Maintenance start hour**</span></span> |<span data-ttu-id="12229-141">0-24</span><span class="sxs-lookup"><span data-stu-id="12229-141">0-24</span></span> |<span data-ttu-id="12229-142">Hallo lokale start tijd tooupdate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="12229-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="12229-143">**Duur van het venster Onderhoud**</span><span class="sxs-lookup"><span data-stu-id="12229-143">**Maintenance window duration**</span></span> |<span data-ttu-id="12229-144">30-180</span><span class="sxs-lookup"><span data-stu-id="12229-144">30-180</span></span> |<span data-ttu-id="12229-145">het aantal minuten Hallo toegestaan toocomplete Hallo downloaden en installeren van updates.</span><span class="sxs-lookup"><span data-stu-id="12229-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="12229-146">**Patch categorie**</span><span class="sxs-lookup"><span data-stu-id="12229-146">**Patch Category**</span></span> |<span data-ttu-id="12229-147">Belangrijk</span><span class="sxs-lookup"><span data-stu-id="12229-147">Important</span></span> |<span data-ttu-id="12229-148">Hallo categorie van updates toodownload downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="12229-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="12229-149">Configuratie met PowerShell</span><span class="sxs-lookup"><span data-stu-id="12229-149">Configuration with PowerShell</span></span>
<span data-ttu-id="12229-150">In de Hallo voorbeeld te volgen, PowerShell gebruikte tooconfigure is automatisch patchen op een bestaande SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="12229-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="12229-151">Hallo **nieuw AzureVMSqlServerAutoPatchingConfig** opdracht configureert u een nieuw onderhoudsvenster voor automatische updates.</span><span class="sxs-lookup"><span data-stu-id="12229-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="12229-152">Op basis van dit voorbeeld, hello volgende tabel staan Hallo praktisch effect op Hallo doel-virtuele machine van Azure:</span><span class="sxs-lookup"><span data-stu-id="12229-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="12229-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="12229-153">Parameter</span></span> | <span data-ttu-id="12229-154">Effect</span><span class="sxs-lookup"><span data-stu-id="12229-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="12229-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="12229-155">**DayOfWeek**</span></span> |<span data-ttu-id="12229-156">Patches elke donderdag geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="12229-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="12229-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="12229-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="12229-158">Begin updates om 11:00 uur.</span><span class="sxs-lookup"><span data-stu-id="12229-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="12229-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="12229-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="12229-160">Patches moeten worden geïnstalleerd binnen 120 minuten.</span><span class="sxs-lookup"><span data-stu-id="12229-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="12229-161">Op basis van de begintijd hello, moeten ze volledig 13:00 uur.</span><span class="sxs-lookup"><span data-stu-id="12229-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="12229-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="12229-162">**PatchCategory**</span></span> |<span data-ttu-id="12229-163">Hallo is alleen mogelijke instelling voor deze parameter 'Belangrijk'.</span><span class="sxs-lookup"><span data-stu-id="12229-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="12229-164">Het kan tooinstall van enkele minuten duren en Hallo SQL Server IaaS-Agent configureren.</span><span class="sxs-lookup"><span data-stu-id="12229-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="12229-165">toodisable automatisch patchen uitvoeren Hallo dezelfde zonder script Hallo - Enable parameter toohello nieuw AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="12229-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="12229-166">Als met de installatie, het enkele minuten toodisable duurt automatisch patchen.</span><span class="sxs-lookup"><span data-stu-id="12229-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12229-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12229-167">Next steps</span></span>
<span data-ttu-id="12229-168">Zie voor meer informatie over andere beschikbare automatiseringstaken [uitbreiding voor SQL Server IaaS-Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="12229-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="12229-169">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="12229-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

