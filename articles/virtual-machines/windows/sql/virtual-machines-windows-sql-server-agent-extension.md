---
title: aaaAutomate beheertaken op SQL-machines (Resource Manager) | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toomanage Hallo voor SQL Server agent-extensie, die specifieke SQL Server-beheertaken worden geautomatiseerd. Het gaat hierbij om automatische back-up automatisch patchen en integratie van Azure Sleutelkluis. In dit onderwerp maakt gebruik van modus Hallo Resource Manager-implementatie.
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
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="14514-105">Automatiseren beheertaken op Azure Virtual Machines Hello SQL Server Agent-extensie (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="14514-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="14514-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="14514-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="14514-107">Klassiek</span><span class="sxs-lookup"><span data-stu-id="14514-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="14514-108">Hallo uitbreiding IaaS-Agent voor SQL Server (SQLIaaSExtension) wordt uitgevoerd op virtuele machines in Azure tooautomate beheertaken.</span><span class="sxs-lookup"><span data-stu-id="14514-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="14514-109">Dit onderwerp bevat een overzicht van Hallo-services wordt ondersteund door het Hallo-extensie, evenals de instructies voor installatie, status en verwijdering.</span><span class="sxs-lookup"><span data-stu-id="14514-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="14514-110">tooview hello klassieke versie van dit artikel, Zie [SQL Server Agent-extensie voor SQL Server-machines klassieke](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="14514-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="14514-111">Ondersteunde services</span><span class="sxs-lookup"><span data-stu-id="14514-111">Supported services</span></span>
<span data-ttu-id="14514-112">Hallo uitbreiding voor SQL Server IaaS-Agent ondersteunt Hallo beheertaken te volgen:</span><span class="sxs-lookup"><span data-stu-id="14514-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="14514-113">Beheer-functie</span><span class="sxs-lookup"><span data-stu-id="14514-113">Administration feature</span></span> | <span data-ttu-id="14514-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="14514-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="14514-115">**Automatische back-up van SQL**</span><span class="sxs-lookup"><span data-stu-id="14514-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="14514-116">Automatiseert Hallo planning van de back-ups voor alle databases voor het standaardexemplaar van SQL Server in Hallo VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="14514-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="14514-117">Zie voor meer informatie [automatische back-up voor SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="14514-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="14514-118">**Automatisch patchen van SQL**</span><span class="sxs-lookup"><span data-stu-id="14514-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="14514-119">Hiermee configureert u een onderhoudsvenster tijdens welke updates plaatsen tooyour VM kan duren, zodat u voorkomen de updates tijdens piektijden voor uw workload dat kunt.</span><span class="sxs-lookup"><span data-stu-id="14514-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="14514-120">Zie voor meer informatie [automatisch patchen voor SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="14514-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="14514-121">**Integratie van Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="14514-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="14514-122">Hiermee schakelt u tooautomatically installeren en configureren van Azure Sleutelkluis op uw SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="14514-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="14514-123">Zie voor meer informatie [configureren Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual machines (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="14514-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="14514-124">Eenmaal geïnstalleerd en uitgevoerd, maakt Hallo uitbreiding voor SQL Server IaaS-Agent deze beheerfuncties beschikbaar in SQL Server-paneel Hallo van Hallo virtuele machine in Azure Portal Hallo en via Azure PowerShell voor SQL Server marketplace-installatiekopieën en via Azure PowerShell voor handmatige installaties van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="14514-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="14514-125">Vereisten</span><span class="sxs-lookup"><span data-stu-id="14514-125">Prerequisites</span></span>
<span data-ttu-id="14514-126">Vereisten toouse Hallo uitbreiding van SQL Server IaaS-Agent op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="14514-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="14514-127">**Besturingssysteem**:</span><span class="sxs-lookup"><span data-stu-id="14514-127">**Operating System**:</span></span>

* <span data-ttu-id="14514-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="14514-128">Windows Server 2012</span></span>
* <span data-ttu-id="14514-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="14514-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="14514-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="14514-130">Windows Server 2016</span></span>

<span data-ttu-id="14514-131">**SQL Server-versies**:</span><span class="sxs-lookup"><span data-stu-id="14514-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="14514-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="14514-132">SQL Server 2012</span></span>
* <span data-ttu-id="14514-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="14514-133">SQL Server 2014</span></span>
* <span data-ttu-id="14514-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="14514-134">SQL Server 2016</span></span>

<span data-ttu-id="14514-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="14514-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="14514-136">Downloaden en configureren van de meest recente Azure PowerShell-opdrachten Hallo</span><span class="sxs-lookup"><span data-stu-id="14514-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="14514-137">Installeren</span><span class="sxs-lookup"><span data-stu-id="14514-137">Installation</span></span>
<span data-ttu-id="14514-138">Hallo uitbreiding voor SQL Server IaaS-Agent wordt automatisch geïnstalleerd wanneer u een van de Hallo SQL Server-virtuele machine afbeeldingen inricht.</span><span class="sxs-lookup"><span data-stu-id="14514-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="14514-139">Als u tooreinstall Hallo uitbreiding handmatig op een van deze VM's van SQL Server moet, gebruikt u Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="14514-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="14514-140">Het is ook mogelijk tooinstall Hallo uitbreiding voor SQL Server IaaS-Agent op de virtuele machine van een alleen-OS Windows-Server.</span><span class="sxs-lookup"><span data-stu-id="14514-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="14514-141">Dit wordt alleen ondersteund als u SQL Server ook handmatig hebt geïnstalleerd op deze machine.</span><span class="sxs-lookup"><span data-stu-id="14514-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="14514-142">En vervolgens installeren Hallo extensie handmatig met behulp van dezelfde Hallo **Set AzureVMSqlServerExtension** PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="14514-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="14514-143">Als u Hallo uitbreiding voor SQL Server IaaS-Agent handmatig op een alleen-besturingssysteem Windows Server-VM installeren, kunt u geen Hallo SQL Server-configuratie-instellingen via hello Azure-portal beheren.</span><span class="sxs-lookup"><span data-stu-id="14514-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="14514-144">In dit scenario moet u alle wijzigingen met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14514-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="14514-145">Status</span><span class="sxs-lookup"><span data-stu-id="14514-145">Status</span></span>
<span data-ttu-id="14514-146">Eenzijdige tooverify dat Hallo-uitbreiding is geïnstalleerd is tooview hello agentstatus in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="14514-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="14514-147">Selecteer **alle instellingen** in Hallo blade van de virtuele machine en klik vervolgens op **extensies**.</span><span class="sxs-lookup"><span data-stu-id="14514-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="14514-148">U ziet Hallo **SQLIaaSExtension** extensie vermeld.</span><span class="sxs-lookup"><span data-stu-id="14514-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![SQL Server IaaS-Agent-extensie in de Azure-Portal](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="14514-150">U kunt ook Hallo **Get-AzureVMSqlServerExtension** Azure Powershell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="14514-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="14514-151">vorige opdracht Hallo bevestigt Hallo-agent is geïnstalleerd en vindt u algemene statusinformatie.</span><span class="sxs-lookup"><span data-stu-id="14514-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="14514-152">U kunt ook specifieke statusinformatie ophalen over automatische back-up en Patching Hello opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="14514-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="14514-153">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="14514-153">Removal</span></span>
<span data-ttu-id="14514-154">U kunt in Azure Portal Hallo, Hallo extensie verwijderen door te klikken op Hallo weglatingsteken op Hallo **extensies** blade van de eigenschappen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="14514-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="14514-155">Klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="14514-155">Then click **Delete**.</span></span>

![Hallo SQL Server IaaS-agentextensie in de Azure Portal verwijderen](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="14514-157">U kunt ook Hallo **verwijderen AzureRmVMSqlServerExtension** Powershell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="14514-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="14514-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14514-158">Next Steps</span></span>
<span data-ttu-id="14514-159">Beginnen met een Hallo-services worden ondersteund door Hallo extension.</span><span class="sxs-lookup"><span data-stu-id="14514-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="14514-160">Zie voor meer informatie, Hallo onderwerpen waarnaar wordt verwezen in Hallo [ondersteunde services](#supported-services) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="14514-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="14514-161">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual Machines [SQL Server op Azure Virtual Machines-overzicht](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14514-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

