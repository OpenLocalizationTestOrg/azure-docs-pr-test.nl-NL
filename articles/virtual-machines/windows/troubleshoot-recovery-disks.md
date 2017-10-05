---
title: Gebruik een virtuele machine met Azure PowerShell probleemoplossing Windows | Microsoft Docs
description: Meer informatie over het oplossen van problemen van de virtuele machine van Windows in Azure door verbinding te maken van de besturingssysteemschijf voor een herstel-VM met Azure PowerShell
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
ms.openlocfilehash: 8b7821b4285e73d461af426bfdfb3fdcc4454517
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="c71a7-103">Een virtuele machine van Windows oplossen door de OS-schijf koppelen aan een herstel-VM met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c71a7-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="c71a7-104">Als uw Windows-machine (VM) in Azure een opstart- of -fout optreedt, moet u wellicht de stappen voor probleemoplossing uitvoeren op de virtuele harde schijf zelf.</span><span class="sxs-lookup"><span data-stu-id="c71a7-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="c71a7-105">Een veelvoorkomend voorbeeld is een mislukte toepassingsupdate die verhindert dat de virtuele machine kunnen opstarten is.</span><span class="sxs-lookup"><span data-stu-id="c71a7-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="c71a7-106">Dit artikel wordt uitgelegd hoe u Azure PowerShell gebruiken voor verbinding van de virtuele harde schijf met een andere virtuele machine van Windows op eventuele fouten te corrigeren en vervolgens opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="c71a7-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="c71a7-107">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="c71a7-107">Recovery process overview</span></span>
<span data-ttu-id="c71a7-108">Het probleemoplossingsproces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="c71a7-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="c71a7-109">Verwijder de virtuele machine zonder problemen, om de virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="c71a7-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="c71a7-110">Koppelen en koppel de virtuele harde schijf aan een andere Windows-VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="c71a7-111">Maak verbinding met de VM voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="c71a7-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="c71a7-112">Bewerken van bestanden of alle hulpmiddelen voor het oplossen van problemen op de oorspronkelijke virtuele harde schijf worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c71a7-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="c71a7-113">Koppel de virtuele harde schijf van de VM voor probleemoplossing los.</span><span class="sxs-lookup"><span data-stu-id="c71a7-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="c71a7-114">Een virtuele machine maken met de oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="c71a7-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="c71a7-115">Zorg ervoor dat u hebt [de meest recente Azure PowerShell](/powershell/azure/overview) geïnstalleerd en aangemeld bij uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="c71a7-115">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="c71a7-116">In de volgende voorbeelden kunt u parameternamen vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="c71a7-116">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="c71a7-117">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c71a7-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="c71a7-118">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="c71a7-118">Determine boot issues</span></span>
<span data-ttu-id="c71a7-119">U kunt een schermopname van uw virtuele machine weergeven in Azure opstartproblemen op te lossen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="c71a7-120">Deze schermafbeelding kunt nagaan waarom een virtuele machine niet kan worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="c71a7-120">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="c71a7-121">Het volgende voorbeeld wordt de schermafbeelding van de Windows-VM met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c71a7-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="c71a7-122">Controleer de schermopname om te bepalen waarom de virtuele machine kan niet worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="c71a7-122">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="c71a7-123">Houd er rekening mee specifieke foutberichten of foutcodes die zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c71a7-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="c71a7-124">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="c71a7-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="c71a7-125">Voordat u de virtuele harde schijf aan een andere virtuele machine koppelen kunt, moet u de naam van de virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="c71a7-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span>

<span data-ttu-id="c71a7-126">Het volgende voorbeeld wordt de informatie voor de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c71a7-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="c71a7-127">Zoek naar `Vhd URI` binnen de `StorageProfile` sectie uit de uitvoer van de voorgaande opdracht.</span><span class="sxs-lookup"><span data-stu-id="c71a7-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span></span> <span data-ttu-id="c71a7-128">Het volgende voorbeeld ziet u uitvoer afgekapt de `Vhd URI` aan het einde van het codeblok:</span><span class="sxs-lookup"><span data-stu-id="c71a7-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span></span>

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


## <a name="delete-existing-vm"></a><span data-ttu-id="c71a7-129">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="c71a7-129">Delete existing VM</span></span>
<span data-ttu-id="c71a7-130">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="c71a7-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="c71a7-131">Een virtuele harde schijf is waar het besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="c71a7-132">De virtuele machine zelf zijn gewoon metagegevens die definieert de grootte of locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="c71a7-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="c71a7-133">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c71a7-133">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="c71a7-134">Hoewel gegevensschijven zelfs wanneer de virtuele machine wordt uitgevoerd, kunnen worden gekoppeld en losgekoppeld, kan de besturingssysteemschijf niet worden losgekoppeld tenzij de VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c71a7-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="c71a7-135">De lease blijft de OS-schijf koppelen aan een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="c71a7-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="c71a7-136">De eerste stap voor het herstellen van uw virtuele machine is de VM-resource zelf verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-136">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="c71a7-137">Wanneer de virtuele machine wordt verwijderd, blijven de virtuele harde schijven aanwezig in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c71a7-137">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="c71a7-138">Nadat de virtuele machine wordt verwijderd, kunt u de virtuele harde schijf koppelen aan een andere virtuele machine kunt u de fouten oplossen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="c71a7-139">Het volgende voorbeeld wordt de virtuele machine met de naam `myVM` uit de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c71a7-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="c71a7-140">Wacht totdat de virtuele machine verwijderen voordat u de virtuele harde schijf aan een andere virtuele machine koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c71a7-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="c71a7-141">De lease op de virtuele harde schijf waarin deze zijn gekoppeld aan de virtuele machine moet worden vrijgegeven voordat u de virtuele harde schijf aan een andere virtuele machine koppelen kunt.</span><span class="sxs-lookup"><span data-stu-id="c71a7-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="c71a7-142">Bestaande virtuele harde schijf koppelen aan een andere virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c71a7-142">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="c71a7-143">Voor de volgende stappen gebruikt u een andere virtuele machine voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-143">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="c71a7-144">U koppelen de bestaande virtuele harde schijf aan deze VM voor probleemoplossing om te bladeren en de inhoud van de schijf bewerken.</span><span class="sxs-lookup"><span data-stu-id="c71a7-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="c71a7-145">Dit proces kunt u eventuele configuratiefouten te corrigeren of extra toepassing of een systeem-logboekbestanden, bijvoorbeeld controleren.</span><span class="sxs-lookup"><span data-stu-id="c71a7-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="c71a7-146">Kies of maak een andere virtuele machine moet worden gebruikt voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-146">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="c71a7-147">Wanneer u de bestaande virtuele harde schijf koppelt, geef de URL naar de schijf die is verkregen in de voorgaande `Get-AzureRmVM` opdracht.</span><span class="sxs-lookup"><span data-stu-id="c71a7-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="c71a7-148">Het volgende voorbeeld wordt een bestaande virtuele harde schijf voor het oplossen van problemen met de naam VM `myVMRecovery` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c71a7-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="c71a7-149">Een schijf toevoegen, moet u de grootte van de schijf opgeven.</span><span class="sxs-lookup"><span data-stu-id="c71a7-149">Adding a disk requires you to specify the size of the disk.</span></span> <span data-ttu-id="c71a7-150">Als er een bestaande schijf koppelen de `-DiskSizeInGB` is opgegeven als `$null`.</span><span class="sxs-lookup"><span data-stu-id="c71a7-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="c71a7-151">Deze waarde zorgt ervoor dat de gegevensschijf correct is gekoppeld, en zonder de noodzaak om te bepalen van de waarde true grootte van de gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="c71a7-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span></span>


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="c71a7-152">Koppel de gekoppelde gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="c71a7-152">Mount the attached data disk</span></span>

1. <span data-ttu-id="c71a7-153">RDP met uw probleemoplossing virtuele machine met de juiste referenties.</span><span class="sxs-lookup"><span data-stu-id="c71a7-153">RDP to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="c71a7-154">Het volgende voorbeeld het RDP-verbindingsbestand downloads voor de virtuele machine met de naam `myVMRecovery` in de resourcegroep met de naam `myResourceGroup`, en deze is gedownload `C:\Users\ops\Documents`'</span><span class="sxs-lookup"><span data-stu-id="c71a7-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="c71a7-155">De gegevensschijf wordt automatisch gedetecteerd en gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="c71a7-155">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="c71a7-156">De lijst met gekoppelde volumes om te bepalen van de stationsletter als volgt bekijken:</span><span class="sxs-lookup"><span data-stu-id="c71a7-156">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="c71a7-157">De volgende voorbeelduitvoer wordt weergegeven op de virtuele harde schijf een schijf verbonden **2**.</span><span class="sxs-lookup"><span data-stu-id="c71a7-157">The following example output shows the virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="c71a7-158">(U kunt ook `Get-Volume` om weer te geven van de stationsletter):</span><span class="sxs-lookup"><span data-stu-id="c71a7-158">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="c71a7-159">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="c71a7-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="c71a7-160">Met de bestaande virtuele harde schijf dat wordt gekoppeld, kunt u nu onderhoud en stappen voor probleemoplossing naar behoefte uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c71a7-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="c71a7-161">Zodra u de problemen hebt opgelost, kunt u doorgaan met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-161">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="c71a7-162">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="c71a7-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="c71a7-163">Zodra de fouten opgelost zijn, kunt u ontkoppelen en loskoppelen van de bestaande virtuele harde schijf van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="c71a7-164">U kunt de virtuele harde schijf niet gebruiken met eventuele andere virtuele machine totdat de lease koppelen van de virtuele harde schijf voor het oplossen van problemen VM is uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="c71a7-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="c71a7-165">Ontkoppel de gegevensschijf binnen uw RDP-sessie op de herstel-VM.</span><span class="sxs-lookup"><span data-stu-id="c71a7-165">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="c71a7-166">U moet het schijfnummer van de vorige `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c71a7-166">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="c71a7-167">Vervolgens gebruikt u `Set-Disk` de schijf als offline instellen:</span><span class="sxs-lookup"><span data-stu-id="c71a7-167">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="c71a7-168">Controleer de schijf is nu ingesteld als het gebruik van offline `Get-Disk` opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c71a7-168">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="c71a7-169">De volgende voorbeelduitvoer wordt weergegeven op dat de schijf is nu ingesteld als offline:</span><span class="sxs-lookup"><span data-stu-id="c71a7-169">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="c71a7-170">De RDP-sessie af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="c71a7-170">Exit your RDP session.</span></span> <span data-ttu-id="c71a7-171">Verwijder de virtuele harde schijf van de probleemoplossing VM van Azure PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="c71a7-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="c71a7-172">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="c71a7-172">Create VM from original hard disk</span></span>
<span data-ttu-id="c71a7-173">Gebruik voor het maken van een virtuele machine van de oorspronkelijke virtuele harde schijf [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="c71a7-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="c71a7-174">De werkelijke JSON-sjabloon is op de volgende koppeling:</span><span class="sxs-lookup"><span data-stu-id="c71a7-174">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="c71a7-175">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD-existing-vnet/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="c71a7-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="c71a7-176">De sjabloon implementeert een virtuele machine in een bestaand virtueel netwerk met behulp van de VHD-URL van de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="c71a7-176">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="c71a7-177">Het volgende voorbeeld implementeert u de sjabloon in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c71a7-177">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="c71a7-178">Beantwoord de aanwijzingen voor de sjabloon zoals VM-naam, type besturingssysteem en VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="c71a7-178">Answer the prompts for the template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="c71a7-179">De `osDiskVhdUri` is hetzelfde als eerder gebruikt als de bestaande virtuele harde schijf koppelen aan de VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="c71a7-179">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="c71a7-180">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="c71a7-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="c71a7-181">Wanneer u uw virtuele machine van de bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c71a7-181">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="c71a7-182">Het volgende voorbeeld wordt de diagnostische uitbreiding op de virtuele machine met de naam `myVMDeployed` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="c71a7-182">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="c71a7-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c71a7-183">Next steps</span></span>
<span data-ttu-id="c71a7-184">Als u verbinding maakt met uw virtuele machine problemen ondervindt, raadpleegt u [problemen met RDP-verbindingen naar een Azure-virtuele machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c71a7-184">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="c71a7-185">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c71a7-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c71a7-186">Zie voor meer informatie over het gebruik van Resource Manager [overzicht van Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c71a7-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
