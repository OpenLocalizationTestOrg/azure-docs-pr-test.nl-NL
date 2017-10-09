---
title: aaaAutomate beheertaken op SQL-machines (klassiek) | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toomanage Hallo voor SQL Server agent-extensie, die specifieke SQL Server-beheertaken worden geautomatiseerd. Het gaat hierbij om automatische back-up automatisch patchen en integratie van Azure Sleutelkluis. In dit onderwerp maakt gebruik van de klassieke implementatiemodus Hallo.
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="ceee0-105">Automatiseren beheertaken op Azure Virtual Machines Hello SQL Server Agent-extensie (klassiek)</span><span class="sxs-lookup"><span data-stu-id="ceee0-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ceee0-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ceee0-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="ceee0-107">Klassiek</span><span class="sxs-lookup"><span data-stu-id="ceee0-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="ceee0-108">Hallo uitbreiding IaaS-Agent voor SQL Server (SQLIaaSAgent) wordt uitgevoerd op virtuele machines in Azure tooautomate beheertaken.</span><span class="sxs-lookup"><span data-stu-id="ceee0-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="ceee0-109">Dit onderwerp bevat een overzicht van Hallo-services wordt ondersteund door het Hallo-extensie, evenals de instructies voor installatie, status en verwijdering.</span><span class="sxs-lookup"><span data-stu-id="ceee0-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ceee0-110">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ceee0-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ceee0-111">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="ceee0-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ceee0-112">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ceee0-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ceee0-113">tooview hello Resource Manager-versie van dit artikel, Zie [SQL Server Agent-extensie voor SQL Server VM's Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ceee0-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="ceee0-114">Ondersteunde services</span><span class="sxs-lookup"><span data-stu-id="ceee0-114">Supported services</span></span>
<span data-ttu-id="ceee0-115">Hallo uitbreiding voor SQL Server IaaS-Agent ondersteunt Hallo beheertaken te volgen:</span><span class="sxs-lookup"><span data-stu-id="ceee0-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="ceee0-116">Beheer-functie</span><span class="sxs-lookup"><span data-stu-id="ceee0-116">Administration feature</span></span> | <span data-ttu-id="ceee0-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ceee0-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ceee0-118">**Automatische back-up van SQL**</span><span class="sxs-lookup"><span data-stu-id="ceee0-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="ceee0-119">Automatiseert Hallo planning van de back-ups voor alle databases voor het standaardexemplaar van SQL Server in Hallo VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="ceee0-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="ceee0-120">Zie voor meer informatie [automatische back-up voor SQL Server in Azure Virtual Machines (klassiek)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ceee0-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="ceee0-121">**Automatisch patchen van SQL**</span><span class="sxs-lookup"><span data-stu-id="ceee0-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="ceee0-122">Hiermee configureert u een onderhoudsvenster tijdens welke updates plaatsen tooyour VM kan duren, zodat u voorkomen de updates tijdens piektijden voor uw workload dat kunt.</span><span class="sxs-lookup"><span data-stu-id="ceee0-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="ceee0-123">Zie voor meer informatie [automatisch patchen voor SQL Server in Azure Virtual Machines (klassiek)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="ceee0-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="ceee0-124">**Integratie van Azure Key Vault**</span><span class="sxs-lookup"><span data-stu-id="ceee0-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="ceee0-125">Hiermee schakelt u tooautomatically installeren en configureren van Azure Sleutelkluis op uw SQL Server-VM.</span><span class="sxs-lookup"><span data-stu-id="ceee0-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="ceee0-126">Zie voor meer informatie [configureren Azure Sleutelkluis-integratie voor SQL Server op Azure Virtual machines (klassiek)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="ceee0-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="ceee0-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ceee0-127">Prerequisites</span></span>
<span data-ttu-id="ceee0-128">Vereisten toouse Hallo uitbreiding van SQL Server IaaS-Agent op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="ceee0-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="ceee0-129">Besturingssysteem:</span><span class="sxs-lookup"><span data-stu-id="ceee0-129">Operating System:</span></span>
* <span data-ttu-id="ceee0-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ceee0-130">Windows Server 2012</span></span>
* <span data-ttu-id="ceee0-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ceee0-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ceee0-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ceee0-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="ceee0-133">SQL Server-versies:</span><span class="sxs-lookup"><span data-stu-id="ceee0-133">SQL Server versions:</span></span>
* <span data-ttu-id="ceee0-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="ceee0-134">SQL Server 2012</span></span>
* <span data-ttu-id="ceee0-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="ceee0-135">SQL Server 2014</span></span>
* <span data-ttu-id="ceee0-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="ceee0-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="ceee0-137">Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ceee0-137">Azure PowerShell:</span></span>
<span data-ttu-id="ceee0-138">[Downloaden en configureren van de meest recente Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ceee0-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="ceee0-139">Start Windows PowerShell en tooyour Azure-abonnement verbinden met de Hallo **Add-AzureAccount** opdracht.</span><span class="sxs-lookup"><span data-stu-id="ceee0-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="ceee0-140">Als u meerdere abonnementen hebt, gebruikt u **Select-AzureSubscription** tooselect Hallo abonnement met het doel-klassieke VM.</span><span class="sxs-lookup"><span data-stu-id="ceee0-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="ceee0-141">Op dit moment kunt u een lijst van Hallo klassieke virtuele machines en hun bijbehorende servicenamen Hello opvragen **Get-AzureVM** opdracht.</span><span class="sxs-lookup"><span data-stu-id="ceee0-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="ceee0-142">Installeren</span><span class="sxs-lookup"><span data-stu-id="ceee0-142">Installation</span></span>
<span data-ttu-id="ceee0-143">Voor klassieke virtuele machines, moet u PowerShell tooinstall Hallo uitbreiding voor IaaS-Agent van SQL Server gebruiken en configureren van de gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="ceee0-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="ceee0-144">Gebruik Hallo **Set AzureVMSqlServerExtension** PowerShell cmdlet tooinstall Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="ceee0-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="ceee0-145">Hallo volgende opdracht wordt bijvoorbeeld Hallo extensie installeert op een Windows Server-VM (klassiek) en naam 'SQLIaaSExtension'.</span><span class="sxs-lookup"><span data-stu-id="ceee0-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="ceee0-146">Als u de meest recente versie van de toohello Hallo SQL IaaS-agentextensie bijwerkt, moet u uw virtuele machine opnieuw opstarten na het bijwerken van Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="ceee0-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="ceee0-147">Klassieke virtuele machines niet op een optie tooinstall hebben en Hallo SQL IaaS-Agent uitbreiding via Hallo portal configureren.</span><span class="sxs-lookup"><span data-stu-id="ceee0-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="ceee0-148">Status</span><span class="sxs-lookup"><span data-stu-id="ceee0-148">Status</span></span>
<span data-ttu-id="ceee0-149">Eenzijdige tooverify dat Hallo-uitbreiding is geïnstalleerd is tooview hello agentstatus in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="ceee0-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="ceee0-150">Selecteer een virtuele machine die worden vermeld in de blade van Hallo virtuele machine en klik vervolgens op **extensies**.</span><span class="sxs-lookup"><span data-stu-id="ceee0-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="ceee0-151">U ziet Hallo **SQLIaaSAgent** extensie vermeld.</span><span class="sxs-lookup"><span data-stu-id="ceee0-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![SQL Server IaaS-Agent-extensie in de Azure-Portal](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="ceee0-153">U kunt ook Hallo **Get-AzureVMSqlServerExtension** Azure Powershell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ceee0-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="ceee0-154">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="ceee0-154">Removal</span></span>
<span data-ttu-id="ceee0-155">U kunt in Azure Portal Hallo, Hallo extensie verwijderen door te klikken op Hallo weglatingsteken op Hallo **extensies** blade van de eigenschappen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ceee0-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="ceee0-156">Klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="ceee0-156">Then click **Uninstall**.</span></span>

![Hallo SQL Server IaaS-agentextensie in de Azure Portal verwijderen](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="ceee0-158">U kunt ook Hallo **verwijderen AzureVMSqlServerExtension** Powershell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ceee0-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="ceee0-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ceee0-159">Next Steps</span></span>
<span data-ttu-id="ceee0-160">Beginnen met een Hallo-services worden ondersteund door Hallo extension.</span><span class="sxs-lookup"><span data-stu-id="ceee0-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="ceee0-161">Zie voor meer informatie, Hallo onderwerpen waarnaar wordt verwezen in Hallo [ondersteunde services](#supported-services) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ceee0-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="ceee0-162">Zie voor meer informatie over het uitvoeren van SQL Server op Azure Virtual Machines [SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ceee0-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

