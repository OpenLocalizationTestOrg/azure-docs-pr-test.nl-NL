---
title: rekenknooppunten aaaManage HPC Pack cluster | Microsoft Docs
description: Meer informatie over PowerShell-script extra tooadd, verwijderen, starten en stoppen van HPC Pack 2012 R2-cluster-rekenknooppunten in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="55e15-103">Hallo aantal en de beschikbaarheid van rekenknooppunten in een cluster HPC Pack in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="55e15-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="55e15-104">Als u een HPC Pack 2012 R2-cluster in Azure VM's hebt gemaakt, kunt u manieren tooeasily toevoegen, verwijderen, (ingericht) starten of stoppen (deprovision) sommige compute knooppunt VM's in het cluster.</span><span class="sxs-lookup"><span data-stu-id="55e15-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="55e15-105">toodo deze taken uitvoeren Azure PowerShell-scripts die zijn geïnstalleerd op Hallo hoofdknooppunt VM.</span><span class="sxs-lookup"><span data-stu-id="55e15-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="55e15-106">Deze scripts met help u Hallo aantal en de beschikbaarheid van uw cluster HPC Pack resources beheren zodat u de kosten kunt bepalen.</span><span class="sxs-lookup"><span data-stu-id="55e15-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="55e15-107">Dit artikel geldt alleen tooHPC Pack 2012 R2 clusters in Azure gemaakt met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="55e15-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="55e15-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55e15-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="55e15-109">Hallo PowerShell-scripts die worden beschreven in dit artikel zijn niet beschikbaar in HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="55e15-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55e15-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="55e15-110">Prerequisites</span></span>
* <span data-ttu-id="55e15-111">**HPC Pack 2012 R2-cluster in Azure VM's**: een HPC Pack 2012 R2-cluster maken in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="55e15-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="55e15-112">U kunt bijvoorbeeld Hallo-implementatie automatiseren met behulp van Hallo HPC Pack 2012 R2 VM-installatiekopie in Azure Marketplace Hallo en een Azure PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="55e15-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="55e15-113">Zie voor informatie en vereisten [een HPC-Cluster maken met Hallo HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="55e15-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="55e15-114">Na de implementatie Hallo zoeken knooppunt management scripts in Hallo % CCP\_HOME % bin-map op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="55e15-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="55e15-115">Elk Hallo scripts worden uitgevoerd als een beheerder.</span><span class="sxs-lookup"><span data-stu-id="55e15-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="55e15-116">**Azure publish certificaat voor het bestand of het beheer van instellingen**: U moet toodo een van de volgende Hallo Hallo hoofdknooppunt van:</span><span class="sxs-lookup"><span data-stu-id="55e15-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="55e15-117">**Importeren hello Azure bestand publicatie-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="55e15-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="55e15-118">toodo deze, voer hello Azure PowerShell-cmdlets volgen op Hallo hoofdknooppunt:</span><span class="sxs-lookup"><span data-stu-id="55e15-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="55e15-119">**Hello Azure-beheercertificaat configureren op het hoofdknooppunt Hallo**.</span><span class="sxs-lookup"><span data-stu-id="55e15-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="55e15-120">Als u Hallo cer-bestand hebt, importeer het in het certificaatarchief van Hallo CurrentUser\My en voer vervolgens hello Azure PowerShell-cmdlet voor uw Azure-omgeving (AzureCloud of AzureChinaCloud) te volgen:</span><span class="sxs-lookup"><span data-stu-id="55e15-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="55e15-121">Rekenknooppunt virtuele machines toevoegen</span><span class="sxs-lookup"><span data-stu-id="55e15-121">Add compute node VMs</span></span>
<span data-ttu-id="55e15-122">Toevoegen van rekenknooppunten Hello **toevoegen HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="55e15-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="55e15-123">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="55e15-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="55e15-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="55e15-124">Parameters</span></span>
* <span data-ttu-id="55e15-125">**ServiceName**: naam van de cloudservice Hallo die nieuwe berekening knooppunt virtuele machines worden toegevoegd aan.</span><span class="sxs-lookup"><span data-stu-id="55e15-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="55e15-126">**ImageName**: Azure VM-installatiekopienaam, die kan worden verkregen via de klassieke Azure-portal Hallo of Azure PowerShell-cmdlet **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="55e15-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="55e15-127">Hallo installatiekopie moet voldoen aan Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="55e15-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="55e15-128">Een Windows-besturingssysteem moet worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="55e15-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="55e15-129">HPC Pack moet worden geïnstalleerd in de berekeningsfunctie knooppunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="55e15-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="55e15-130">Hallo afbeelding moet een persoonlijke installatiekopie in gebruikerscategorie hello, niet een openbare Azure VM-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="55e15-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="55e15-131">**Aantal**: aantal compute knooppunt VMs toobe toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="55e15-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="55e15-132">**InstanceSize**: grootte van Hallo compute knooppunt virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="55e15-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="55e15-133">**DomainUserName**: domeingebruikersnaam, dat wil gebruikte toojoin Hallo nieuwe virtuele machines toohello domein zeggen.</span><span class="sxs-lookup"><span data-stu-id="55e15-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="55e15-134">**DomainUserPassword**: wachtwoord van de domeingebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="55e15-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="55e15-135">**NodeNameSeries** (optioneel): patroon naamgeving voor Hallo rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="55e15-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="55e15-136">Hallo-indeling moet &lt; *hoofdmap\_naam*&gt;&lt;*Start\_getal*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="55e15-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="55e15-137">Bijvoorbeeld, compute MyCN % 10%: een reeks Hallo knooppuntnamen vanaf MyCN11.</span><span class="sxs-lookup"><span data-stu-id="55e15-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="55e15-138">Als niet wordt opgegeven, Hallo script gebruikt Hallo knooppunt naming reeks geconfigureerd in Hallo HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="55e15-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="55e15-139">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="55e15-139">Example</span></span>
<span data-ttu-id="55e15-140">Hallo volgende voorbeeld wordt 20 grootte grote rekenknooppunt virtuele machines in de cloudservice hello *hpcservice1*, op basis van de VM-installatiekopie Hallo *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="55e15-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="55e15-141">Rekenknooppunt virtuele machines verwijderen</span><span class="sxs-lookup"><span data-stu-id="55e15-141">Remove compute node VMs</span></span>
<span data-ttu-id="55e15-142">Verwijderen van rekenknooppunten Hello **verwijderen HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="55e15-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="55e15-143">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="55e15-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="55e15-144">Parameters</span><span class="sxs-lookup"><span data-stu-id="55e15-144">Parameters</span></span>
* <span data-ttu-id="55e15-145">**Naam**: namen van de cluster knooppunten toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="55e15-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="55e15-146">Jokertekens worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="55e15-146">Wildcards are supported.</span></span> <span data-ttu-id="55e15-147">Hallo-parameternaam set is.</span><span class="sxs-lookup"><span data-stu-id="55e15-147">hello parameter set name is Name.</span></span> <span data-ttu-id="55e15-148">U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.</span><span class="sxs-lookup"><span data-stu-id="55e15-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="55e15-149">**Knooppunt**: Hallo HpcNode object voor Hallo knooppunten toobe verwijderd, die kan worden verkregen via Hallo HPC PowerShell-cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="55e15-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="55e15-150">naam van de parameter Hallo is knooppunt.</span><span class="sxs-lookup"><span data-stu-id="55e15-150">hello parameter set name is Node.</span></span> <span data-ttu-id="55e15-151">U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.</span><span class="sxs-lookup"><span data-stu-id="55e15-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="55e15-152">**DeleteVHD** (optioneel): instelling toodelete Hallo gekoppeld schijven voor Hallo virtuele machines die zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="55e15-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="55e15-153">**Force** (optioneel): tooforce offline HPC-knooppunten instellen voordat u ze verwijdert.</span><span class="sxs-lookup"><span data-stu-id="55e15-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="55e15-154">**Bevestig** (optioneel): vragen om bevestiging voordat het Hallo-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="55e15-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="55e15-155">**WhatIf**: toodescribe instellen wat er zou gebeuren als u Hallo-opdracht uitvoert, zonder het Hallo-opdracht daadwerkelijk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="55e15-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="55e15-156">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="55e15-156">Example</span></span>
<span data-ttu-id="55e15-157">Hallo volgende voorbeeld zorgt ervoor dat offline Hallo knooppunten met namen die beginnen *HPCNode-CN -* en ze Hallo knooppunten en hun bijbehorende schijven worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="55e15-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="55e15-158">Rekenknooppunt virtuele machines starten</span><span class="sxs-lookup"><span data-stu-id="55e15-158">Start compute node VMs</span></span>
<span data-ttu-id="55e15-159">Start de rekenknooppunten Hello **Start HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="55e15-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="55e15-160">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="55e15-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="55e15-161">Parameters</span><span class="sxs-lookup"><span data-stu-id="55e15-161">Parameters</span></span>
* <span data-ttu-id="55e15-162">**Naam**: namen van Hallo cluster knooppunten toobe gestart.</span><span class="sxs-lookup"><span data-stu-id="55e15-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="55e15-163">Jokertekens worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="55e15-163">Wildcards are supported.</span></span> <span data-ttu-id="55e15-164">Hallo-parameternaam set is.</span><span class="sxs-lookup"><span data-stu-id="55e15-164">hello parameter set name is Name.</span></span> <span data-ttu-id="55e15-165">U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.</span><span class="sxs-lookup"><span data-stu-id="55e15-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="55e15-166">**Knooppunt**-Hallo HpcNode object voor Hallo knooppunten toobe gestart, die kan worden verkregen via Hallo HPC PowerShell-cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="55e15-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="55e15-167">naam van de parameter Hallo is knooppunt.</span><span class="sxs-lookup"><span data-stu-id="55e15-167">hello parameter set name is Node.</span></span> <span data-ttu-id="55e15-168">U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.</span><span class="sxs-lookup"><span data-stu-id="55e15-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="55e15-169">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="55e15-169">Example</span></span>
<span data-ttu-id="55e15-170">Hallo volgende voorbeeld begint knooppunten met namen die beginnen *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="55e15-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="55e15-171">Rekenknooppunt virtuele machines stoppen</span><span class="sxs-lookup"><span data-stu-id="55e15-171">Stop compute node VMs</span></span>
<span data-ttu-id="55e15-172">Stoppen van rekenknooppunten Hello **Stop HpcIaaSNode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="55e15-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="55e15-173">Syntaxis</span><span class="sxs-lookup"><span data-stu-id="55e15-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="55e15-174">Parameters</span><span class="sxs-lookup"><span data-stu-id="55e15-174">Parameters</span></span>
* <span data-ttu-id="55e15-175">**Naam**-namen van Hallo cluster knooppunten toobe gestopt.</span><span class="sxs-lookup"><span data-stu-id="55e15-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="55e15-176">Jokertekens worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="55e15-176">Wildcards are supported.</span></span> <span data-ttu-id="55e15-177">Hallo-parameternaam set is.</span><span class="sxs-lookup"><span data-stu-id="55e15-177">hello parameter set name is Name.</span></span> <span data-ttu-id="55e15-178">U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.</span><span class="sxs-lookup"><span data-stu-id="55e15-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="55e15-179">**Knooppunt**: Hallo HpcNode object voor Hallo knooppunten toobe is gestopt, die kan worden verkregen via Hallo HPC PowerShell-cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="55e15-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="55e15-180">naam van de parameter Hallo is knooppunt.</span><span class="sxs-lookup"><span data-stu-id="55e15-180">hello parameter set name is Node.</span></span> <span data-ttu-id="55e15-181">U kunt niet beide Hallo opgeven **naam** en **knooppunt** parameters.</span><span class="sxs-lookup"><span data-stu-id="55e15-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="55e15-182">**Force** (optioneel): tooforce offline HPC-knooppunten instellen voordat u ze stopt.</span><span class="sxs-lookup"><span data-stu-id="55e15-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="55e15-183">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="55e15-183">Example</span></span>
<span data-ttu-id="55e15-184">Hallo volgende voorbeeld zorgt ervoor dat offline knooppunten met namen die beginnen *HPCNode-CN -* en vervolgens stopt Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="55e15-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="55e15-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55e15-185">Next steps</span></span>
* <span data-ttu-id="55e15-186">tooautomatically vergroten of verkleinen van de clusterknooppunten Hallo volgens de huidige werkbelasting Hallo van jobs en taken op Hallo cluster, Zie [automatisch vergroten of verkleinen Hallo HPC Pack clusterbronnen in Azure volgens toohello clusterbelasting](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="55e15-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

