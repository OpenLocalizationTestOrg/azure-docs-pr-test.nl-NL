---
title: aaaUse a Windows VM met Azure PowerShell probleemoplossing | Microsoft Docs
description: Meer informatie over hoe Windows VM tootroubleshoot problemen in Azure door verbinding te maken Hallo OS tooa schijfherstel VM die gebruikmaakt van Azure PowerShell
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="614e8-103">Een virtuele machine van Windows oplossen door het Hallo OS tooa schijfherstel VM die gebruikmaakt van Azure PowerShell koppelen</span><span class="sxs-lookup"><span data-stu-id="614e8-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="614e8-104">Als uw Windows-machine (VM) in Azure een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf.</span><span class="sxs-lookup"><span data-stu-id="614e8-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="614e8-105">Een veelvoorkomend voorbeeld zou een mislukte toepassingsupdate die verhindert dat Hallo VM kunnen tooboot correct zijn.</span><span class="sxs-lookup"><span data-stu-id="614e8-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="614e8-106">Dit artikel details hoe toouse Azure PowerShell tooconnect uw virtuele harde schijf tooanother Windows VM toofix eventuele fouten opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="614e8-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="614e8-107">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="614e8-107">Recovery process overview</span></span>
<span data-ttu-id="614e8-108">Hallo procedure voor probleemoplossing is als volgt:</span><span class="sxs-lookup"><span data-stu-id="614e8-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="614e8-109">Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="614e8-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="614e8-110">Koppelen en koppelen van Hallo virtuele harde schijf tooanother Windows-VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="614e8-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="614e8-111">Verbinding maken met toohello VM probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="614e8-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="614e8-112">Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="614e8-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="614e8-113">Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="614e8-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="614e8-114">Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="614e8-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="614e8-115">Zorg ervoor dat u hebt [nieuwste Azure PowerShell Hallo](/powershell/azure/overview) geïnstalleerd en geregistreerd in tooyour abonnement:</span><span class="sxs-lookup"><span data-stu-id="614e8-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="614e8-116">In Hallo vervangen volgende voorbeelden parameternamen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="614e8-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="614e8-117">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="614e8-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="614e8-118">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="614e8-118">Determine boot issues</span></span>
<span data-ttu-id="614e8-119">U kunt een schermopname van uw virtuele machine weergeven in Azure toohelp problemen met opstarten.</span><span class="sxs-lookup"><span data-stu-id="614e8-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="614e8-120">Deze schermafbeelding kunt nagaan waarom een virtuele machine tooboot mislukt.</span><span class="sxs-lookup"><span data-stu-id="614e8-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="614e8-121">Hallo volgende voorbeeld krijgt Hallo schermafbeelding van virtuele machine met de naam van Windows hello `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="614e8-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="614e8-122">Bekijk Hallo schermafbeelding toodetermine waarom Hallo VM tooboot is mislukt.</span><span class="sxs-lookup"><span data-stu-id="614e8-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="614e8-123">Houd er rekening mee specifieke foutberichten of foutcodes die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="614e8-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="614e8-124">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="614e8-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="614e8-125">Voordat u uw virtuele harde schijf tooanother VM koppelen kunt, moet u tooidentify Hallo-naam van Hallo virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="614e8-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="614e8-126">Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="614e8-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="614e8-127">Zoek naar `Vhd URI` binnen Hallo `StorageProfile` sectie uit Hallo uitvoer van de voorgaande opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="614e8-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="614e8-128">Hallo volgende ingekorte voorbeelduitvoer wordt weergegeven Hallo `Vhd URI` aan einde van het codeblok Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="614e8-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="614e8-129">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="614e8-129">Delete existing VM</span></span>
<span data-ttu-id="614e8-130">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="614e8-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="614e8-131">Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="614e8-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="614e8-132">Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="614e8-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="614e8-133">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM.</span><span class="sxs-lookup"><span data-stu-id="614e8-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="614e8-134">Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="614e8-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="614e8-135">Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="614e8-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="614e8-136">eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf.</span><span class="sxs-lookup"><span data-stu-id="614e8-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="614e8-137">Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="614e8-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="614e8-138">Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.</span><span class="sxs-lookup"><span data-stu-id="614e8-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="614e8-139">Hallo volgende voorbeeld verwijdert met de naam VM Hallo `myVM` van Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="614e8-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="614e8-140">Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="614e8-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="614e8-141">Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="614e8-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="614e8-142">Bestaande virtuele harde schijf tooanother VM koppelen</span><span class="sxs-lookup"><span data-stu-id="614e8-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="614e8-143">Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="614e8-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="614e8-144">U koppelt Hallo bestaande virtuele harde schijf toothis VM toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="614e8-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="614e8-145">Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="614e8-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="614e8-146">Kies of maak een ander VM-toouse voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="614e8-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="614e8-147">Wanneer u een bestaande virtuele harde schijf van Hallo koppelt, geef Hallo URL toohello schijf verkregen in de voorgaande Hallo `Get-AzureRmVM` opdracht.</span><span class="sxs-lookup"><span data-stu-id="614e8-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="614e8-148">Hallo volgende voorbeeld wordt een bestaande virtuele harde schijf toohello het oplossen van problemen met de naam VM `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="614e8-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="614e8-149">Een schijf toevoegen, moet u toospecify Hallo grootte van Hallo schijf.</span><span class="sxs-lookup"><span data-stu-id="614e8-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="614e8-150">Als er een bestaande schijf koppelen, Hallo `-DiskSizeInGB` is opgegeven als `$null`.</span><span class="sxs-lookup"><span data-stu-id="614e8-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="614e8-151">Deze waarde zorgt Hallo gegevensschijf correct is gekoppeld en zonder Hallo moet toodetermine Hallo true grootte van de gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="614e8-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="614e8-152">Hallo bijgesloten gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="614e8-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="614e8-153">RDP-tooyour het oplossen van problemen met de juiste referenties Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="614e8-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="614e8-154">Hallo volgende voorbeeld downloadt Hallo RDP-verbindingsbestand voor Hallo VM met de naam `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`, en te downloadt`C:\Users\ops\Documents`'</span><span class="sxs-lookup"><span data-stu-id="614e8-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="614e8-155">Hallo gegevensschijf wordt automatisch gedetecteerd en gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="614e8-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="614e8-156">Lijst van de stationsletter van gekoppelde volumes toodetermine Hallo Hallo als volgt bekijken:</span><span class="sxs-lookup"><span data-stu-id="614e8-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="614e8-157">Hallo volgende voorbeelduitvoer toont Hallo virtuele hardeschijf een schijf verbonden **2**.</span><span class="sxs-lookup"><span data-stu-id="614e8-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="614e8-158">(U kunt ook `Get-Volume` tooview Hallo stationsletter):</span><span class="sxs-lookup"><span data-stu-id="614e8-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="614e8-159">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="614e8-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="614e8-160">Hallo bestaande virtuele harde schijf gekoppeld, kunt u eventuele onderhoud en probleemoplossing naar behoefte nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="614e8-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="614e8-161">Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="614e8-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="614e8-162">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="614e8-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="614e8-163">Zodra de fouten opgelost zijn, kunt u ontkoppelen en Hallo bestaande virtuele harde schijf los te koppelen van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="614e8-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="614e8-164">U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="614e8-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="614e8-165">Ontkoppel de gegevensschijf Hallo binnen uw RDP-sessie op de herstel-VM.</span><span class="sxs-lookup"><span data-stu-id="614e8-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="614e8-166">Moet u schijfnummer Hallo van Hallo vorige `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="614e8-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="614e8-167">Vervolgens gebruikt u `Set-Disk` tooset Hallo schijf als offline zetten:</span><span class="sxs-lookup"><span data-stu-id="614e8-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="614e8-168">Bevestig het Hallo-schijf is nu ingesteld als het gebruik van offline `Get-Disk` opnieuw.</span><span class="sxs-lookup"><span data-stu-id="614e8-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="614e8-169">Hallo volgende voorbeelduitvoer wordt weergegeven Hallo schijf nu is ingesteld als offline:</span><span class="sxs-lookup"><span data-stu-id="614e8-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="614e8-170">De RDP-sessie af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="614e8-170">Exit your RDP session.</span></span> <span data-ttu-id="614e8-171">Hallo probleemoplossing VM opheffen Hallo virtuele hardeschijf van uw Azure PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="614e8-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="614e8-172">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="614e8-172">Create VM from original hard disk</span></span>
<span data-ttu-id="614e8-173">toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="614e8-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="614e8-174">Hallo werkelijke JSON-sjabloon is op Hallo koppeling:</span><span class="sxs-lookup"><span data-stu-id="614e8-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="614e8-175">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD-existing-vnet/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="614e8-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="614e8-176">Hallo sjabloon een virtuele machine implementeert in een bestaand virtueel netwerk met behulp van Hallo VHD URL uit Hallo eerder opdracht.</span><span class="sxs-lookup"><span data-stu-id="614e8-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="614e8-177">Hallo volgende voorbeeld implementeert Hallo sjabloon toohello resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="614e8-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="614e8-178">Antwoord Hallo vraagt om de sjabloon Hallo zoals VM-naam, type besturingssysteem en VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="614e8-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="614e8-179">Hallo `osDiskVhdUri` is dezelfde als eerder is gebruikt bij het toevoegen van Hallo bestaande virtuele harde schijf toohello probleemoplossing VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="614e8-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="614e8-180">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="614e8-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="614e8-181">Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="614e8-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="614e8-182">Hallo volgende voorbeeld wordt de diagnostische Hallo-extensie op Hallo VM met de naam `myVMDeployed` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="614e8-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="614e8-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="614e8-183">Next steps</span></span>
<span data-ttu-id="614e8-184">Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [problemen met RDP-verbindingen tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="614e8-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="614e8-185">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="614e8-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="614e8-186">Zie voor meer informatie over het gebruik van Resource Manager [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="614e8-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
