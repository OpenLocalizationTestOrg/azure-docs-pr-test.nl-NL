---
title: Automatiseren beheertaken op SQL-machines (Resource Manager) | Microsoft Docs
description: In dit onderwerp wordt beschreven hoe voor het beheren van de SQL Server agent-extensie, die specifieke SQL Server-beheertaken worden geautomatiseerd. Het gaat hierbij om automatische back-up automatisch patchen en integratie van Azure Sleutelkluis. In dit onderwerp maakt gebruik van de implementatiemodus Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7152d184bb6d1d4b81aeb47e2c7c9160ada36023
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-the-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="e0e08-105">Automatiseren beheertaken op Azure Virtual Machines met de SQL Server Agent-extensie (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e0e08-105">Automate management tasks on Azure Virtual Machines with the SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e0e08-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e0e08-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="e0e08-107">Klassiek</span><span class="sxs-lookup"><span data-stu-id="e0e08-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="e0e08-108">De extensie in SQL Server IaaS-Agent (SQLIaaSExtension) wordt uitgevoerd op Azure virtuele machines voor het automatiseren van beheertaken.</span><span class="sxs-lookup"><span data-stu-id="e0e08-108">The SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines to automate administration tasks.</span></span> <span data-ttu-id="e0e08-109">In dit onderwerp biedt een overzicht van de services wordt ondersteund door de extensie, evenals de instructies voor installatie, status en verwijdering.</span><span class="sxs-lookup"><span data-stu-id="e0e08-109">This topic provides an overview of the services supported by the extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="e0e08-110">De klassieke versie van dit artikel vindt u [SQL Server Agent-extensie voor SQL Server-machines klassieke](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e0e08-110">To view the classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="e0e08-111">Ondersteunde services</span><span class="sxs-lookup"><span data-stu-id="e0e08-111">Supported services</span></span>
<span data-ttu-id="e0e08-112">De uitbreiding met SQL Server IaaS-Agent ondersteunt de volgende beheertaken:</span><span class="sxs-lookup"><span data-stu-id="e0e08-112">The SQL Server IaaS Agent Extension supports the following administration tasks:</span></span>

| <span data-ttu-id="e0e08-113">Beheer-functie</span><span class="sxs-lookup"><span data-stu-id="e0e08-113">Administration feature</span></span> | <span data-ttu-id="e0e08-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e0e08-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e0e08-115">**Automatische back-up van SQL**</span><span class="sxs-lookup"><span data-stu-id="e0e08-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="e0e08-116">Automatiseert de planning van de back-ups voor alle databases voor het standaardexemplaar van SQL Server in de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e0e08-116">Automates the scheduling of backups for all databases for the default instance of SQL Server in the VM.</span></span> <span data-ttu-id="e0e08-117">Zie voor meer informatie [automatische back-up voor SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e0e08-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="e0e08-118">**Automatisch patchen van SQL**</span><span class="sxs-lookup"><span data-stu-id="e0e08-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="e0e08-119">Hiermee configureert u een onderhoudsvenster waarbinnen updates voor uw virtuele machine kunnen worden uitgevoerd, zodat u voorkomen de updates tijdens piektijden voor uw workload dat kunt.</span><span class="sxs-lookup"><span data-stu-id="e0e08-119">Configures a maintenance window during which updates to your VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="e0e08-120">Zie voor meer informatie [automatisch patchen voor SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="e0e08-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="e0e08-121">**Integratie van Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="e0e08-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="e0e08-122">Hiermee kunt u automatisch installeren en configureren van Azure Sleutelkluis op uw SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="e0e08-122">Enables you to automatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="e0e08-123">Zie voor meer informatie [configureren Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual machines (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="e0e08-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="e0e08-124">Eenmaal geïnstalleerd en wordt uitgevoerd, maakt de uitbreiding met SQL Server IaaS-Agent deze beheerfuncties beschikbaar in het deelvenster SQL Server van de virtuele machine in de Azure-Portal en via Azure PowerShell voor SQL Server marketplace-installatiekopieën en via Azure PowerShell voor handmatige installaties van de extensie.</span><span class="sxs-lookup"><span data-stu-id="e0e08-124">Once installed and running, the SQL Server IaaS Agent Extension makes these administration features available on the SQL Server panel of the virtual machine in the Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of the extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e0e08-125">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e0e08-125">Prerequisites</span></span>
<span data-ttu-id="e0e08-126">Vereisten voor het gebruik van de uitbreiding met SQL Server IaaS-Agent op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="e0e08-126">Requirements to use the SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="e0e08-127">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="e0e08-127">**Operating System**:</span></span>

* <span data-ttu-id="e0e08-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="e0e08-128">Windows Server 2012</span></span>
* <span data-ttu-id="e0e08-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e0e08-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="e0e08-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e0e08-130">Windows Server 2016</span></span>

<span data-ttu-id="e0e08-131">**SQL Server-versies**:</span><span class="sxs-lookup"><span data-stu-id="e0e08-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="e0e08-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="e0e08-132">SQL Server 2012</span></span>
* <span data-ttu-id="e0e08-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e0e08-133">SQL Server 2014</span></span>
* <span data-ttu-id="e0e08-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="e0e08-134">SQL Server 2016</span></span>

<span data-ttu-id="e0e08-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="e0e08-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="e0e08-136">Downloaden en configureren van de meest recente Azure PowerShell-opdrachten</span><span class="sxs-lookup"><span data-stu-id="e0e08-136">Download and configure the latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="e0e08-137">Installeren</span><span class="sxs-lookup"><span data-stu-id="e0e08-137">Installation</span></span>
<span data-ttu-id="e0e08-138">De uitbreiding met SQL Server IaaS-Agent wordt automatisch geïnstalleerd wanneer u een van de SQL Server-installatiekopieën voor virtuele machine galerie inricht.</span><span class="sxs-lookup"><span data-stu-id="e0e08-138">The SQL Server IaaS Agent Extension is automatically installed when you provision one of the SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="e0e08-139">Als u moet de uitbreiding handmatig installeren op een van deze VM's van SQL Server, gebruikt u de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e0e08-139">If you need to reinstall the extension manually on one of these SQL Server VMs, use the following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="e0e08-140">Het is ook mogelijk de uitbreiding met SQL Server IaaS-Agent installeren op een virtuele machine van de OS-alleen Windows-Server.</span><span class="sxs-lookup"><span data-stu-id="e0e08-140">It is also possible to install the SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="e0e08-141">Dit wordt alleen ondersteund als u SQL Server ook handmatig hebt geïnstalleerd op deze machine.</span><span class="sxs-lookup"><span data-stu-id="e0e08-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="e0e08-142">Installeer de uitbreiding handmatig met behulp van dezelfde **Set AzureVMSqlServerExtension** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e0e08-142">Then install the extension manually by using the same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e0e08-143">Als u de uitbreiding met SQL Server IaaS-Agent handmatig op een alleen-besturingssysteem Windows Server-VM installeren, kunt u de SQL Server-configuratie-instellingen via de Azure portal niet beheren.</span><span class="sxs-lookup"><span data-stu-id="e0e08-143">If you manually install the SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage the SQL Server configuration settings through the Azure portal.</span></span> <span data-ttu-id="e0e08-144">In dit scenario moet u alle wijzigingen met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0e08-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="e0e08-145">Status</span><span class="sxs-lookup"><span data-stu-id="e0e08-145">Status</span></span>
<span data-ttu-id="e0e08-146">Er is een manier om te controleren of de uitbreiding is geïnstalleerd om weer te geven van de agent-status in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e0e08-146">One way to verify that the extension is installed is to view the agent status in the Azure Portal.</span></span> <span data-ttu-id="e0e08-147">Selecteer **alle instellingen** in de blade van de virtuele machine en klik vervolgens op **extensies**.</span><span class="sxs-lookup"><span data-stu-id="e0e08-147">Select **All settings** in the virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="e0e08-148">U ziet de **SQLIaaSExtension** extensie vermeld.</span><span class="sxs-lookup"><span data-stu-id="e0e08-148">You should see the **SQLIaaSExtension** extension listed.</span></span>

![SQL Server IaaS-Agent-extensie in de Azure-Portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="e0e08-150">U kunt ook de **Get-AzureVMSqlServerExtension** Azure Powershell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e0e08-150">You can also use the **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="e0e08-151">De vorige opdracht bevestigt de agent is geïnstalleerd en vindt u algemene statusinformatie.</span><span class="sxs-lookup"><span data-stu-id="e0e08-151">The previous command confirms the agent is installed and provides general status information.</span></span> <span data-ttu-id="e0e08-152">U kunt ook specifieke statusinformatie ophalen over automatische back-up en Patching met de volgende opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e0e08-152">You can also get specific status information about Automated Backup and Patching with the following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="e0e08-153">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="e0e08-153">Removal</span></span>
<span data-ttu-id="e0e08-154">In de Azure-Portal kunt u de extensie verwijderen door te klikken op het weglatingsteken op de **extensies** blade van de eigenschappen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e0e08-154">In the Azure Portal, you can uninstall the extension by clicking the ellipsis on the **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="e0e08-155">Klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e0e08-155">Then click **Delete**.</span></span>

![De SQL Server Agent IaaS-uitbreiding in Azure-Portal verwijderen](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="e0e08-157">U kunt ook de **verwijderen AzureRmVMSqlServerExtension** Powershell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e0e08-157">You can also use the **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="e0e08-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e0e08-158">Next Steps</span></span>
<span data-ttu-id="e0e08-159">Beginnen met een van de services wordt ondersteund door de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="e0e08-159">Begin using one of the services supported by the extension.</span></span> <span data-ttu-id="e0e08-160">Voor meer informatie, Zie de onderwerpen waarnaar wordt verwezen in de [ondersteunde services](#supported-services) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="e0e08-160">For more details, see the topics referenced in the [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="e0e08-161">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual Machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0e08-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

