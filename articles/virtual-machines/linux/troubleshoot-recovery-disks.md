---
title: Gebruik een op Linux VM met de Azure CLI 2.0 probleemoplossing | Microsoft Docs
description: Meer informatie over het oplossen van problemen van Linux VM door verbinding te maken van de besturingssysteemschijf voor een herstel-VM met de Azure CLI 2.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 7a28accce1bd328b2b486b588c44d91b03e42122
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-with-the-azure-cli-20"></a><span data-ttu-id="89893-103">Problemen oplossen van een Linux-VM met de OS-schijf koppelen aan een herstel-VM met de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="89893-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM with the Azure CLI 2.0</span></span>
<span data-ttu-id="89893-104">Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u wellicht de stappen voor probleemoplossing uitvoeren op de virtuele harde schijf zelf.</span><span class="sxs-lookup"><span data-stu-id="89893-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="89893-105">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` die verhindert dat de virtuele machine kunnen opstarten is.</span><span class="sxs-lookup"><span data-stu-id="89893-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="89893-106">Dit artikel wordt uitgelegd hoe u met de Azure CLI 2.0 verbinding maken met de virtuele harde schijf aan een andere Linux VM eventuele fouten te corrigeren en vervolgens opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="89893-106">This article details how to use the Azure CLI 2.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span> <span data-ttu-id="89893-107">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89893-107">You can also perform these steps with the [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="89893-108">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="89893-108">Recovery process overview</span></span>
<span data-ttu-id="89893-109">Het probleemoplossingsproces is als volgt:</span><span class="sxs-lookup"><span data-stu-id="89893-109">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="89893-110">Verwijder de virtuele machine zonder problemen, om de virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="89893-110">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="89893-111">Koppelen en koppel de virtuele harde schijf aan een andere Linux VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="89893-111">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="89893-112">Maak verbinding met de VM voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="89893-112">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="89893-113">Bewerken van bestanden of alle hulpmiddelen voor het oplossen van problemen op de oorspronkelijke virtuele harde schijf worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="89893-113">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="89893-114">Koppel de virtuele harde schijf van de VM voor probleemoplossing los.</span><span class="sxs-lookup"><span data-stu-id="89893-114">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="89893-115">Een virtuele machine maken met de oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="89893-115">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="89893-116">Voor deze stappen voor probleemoplossing, moet u de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="89893-116">To perform these troubleshooting steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="89893-117">In de volgende voorbeelden kunt u parameternamen vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="89893-117">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="89893-118">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="89893-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="89893-119">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="89893-119">Determine boot issues</span></span>
<span data-ttu-id="89893-120">Bekijk de uitvoer seriële om te bepalen waarom de virtuele machine kan niet correct worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="89893-120">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="89893-121">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of de onderliggende virtuele harde schijf wordt verwijderd of verplaatst.</span><span class="sxs-lookup"><span data-stu-id="89893-121">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="89893-122">De logboeken opstarten met [az vm diagnostische gegevens over opstarten get-boot-logboek](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="89893-122">Get the boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="89893-123">Het volgende voorbeeld wordt de uitvoer van de seriële van de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89893-123">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="89893-124">Bekijk de uitvoer van de seriële om te bepalen waarom de virtuele machine kan niet worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="89893-124">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="89893-125">Als de uitvoer van de seriële is niet een aanwijzing biedt, moet u mogelijk Raadpleeg logboekbestanden in `/var/log` zodra u de virtuele harde schijf is verbonden met een VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="89893-125">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="89893-126">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="89893-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="89893-127">Voordat u de virtuele harde schijf (VHD) aan een andere virtuele machine koppelen kunt, moet u de URI van de besturingssysteemschijf te identificeren.</span><span class="sxs-lookup"><span data-stu-id="89893-127">Before you can attach your virtual hard disk (VHD) to another VM, you need to identify the URI of the OS disk.</span></span> 

<span data-ttu-id="89893-128">Informatie weergeven over uw virtuele machine met [az vm weergeven](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="89893-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="89893-129">Gebruik de `--query` vlag uitpakken van de URI moet een schijf met het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="89893-129">Use the `--query` flag to extract the URI to the OS disk.</span></span> <span data-ttu-id="89893-130">Het volgende voorbeeld wordt informatie over de schijven voor de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89893-130">The following example gets disk information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="89893-131">De URI is vergelijkbaar met **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="89893-131">The URI is similar to **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="89893-132">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="89893-132">Delete existing VM</span></span>
<span data-ttu-id="89893-133">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="89893-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="89893-134">Een virtuele harde schijf is waar het besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="89893-134">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="89893-135">De virtuele machine zelf zijn gewoon metagegevens die definieert de grootte of locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="89893-135">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="89893-136">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld aan een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="89893-136">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="89893-137">Hoewel gegevensschijven zelfs wanneer de virtuele machine wordt uitgevoerd, kunnen worden gekoppeld en losgekoppeld, kan de besturingssysteemschijf niet worden losgekoppeld tenzij de VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="89893-137">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="89893-138">De lease blijft de OS-schijf koppelen aan een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="89893-138">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="89893-139">De eerste stap voor het herstellen van uw virtuele machine is de VM-resource zelf verwijderen.</span><span class="sxs-lookup"><span data-stu-id="89893-139">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="89893-140">Wanneer de virtuele machine wordt verwijderd, blijven de virtuele harde schijven aanwezig in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="89893-140">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="89893-141">Nadat de virtuele machine wordt verwijderd, kunt u de virtuele harde schijf koppelen aan een andere virtuele machine kunt u de fouten oplossen.</span><span class="sxs-lookup"><span data-stu-id="89893-141">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="89893-142">Verwijderen van de virtuele machine met [az vm verwijderen](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="89893-142">Delete the VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="89893-143">Het volgende voorbeeld wordt de virtuele machine met de naam `myVM` uit de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89893-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="89893-144">Wacht totdat de virtuele machine verwijderen voordat u de virtuele harde schijf aan een andere virtuele machine koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="89893-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="89893-145">De lease op de virtuele harde schijf waarin deze zijn gekoppeld aan de virtuele machine moet worden vrijgegeven voordat u de virtuele harde schijf aan een andere virtuele machine koppelen kunt.</span><span class="sxs-lookup"><span data-stu-id="89893-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="89893-146">Bestaande virtuele harde schijf koppelen aan een andere virtuele machine</span><span class="sxs-lookup"><span data-stu-id="89893-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="89893-147">Voor de volgende stappen gebruikt u een andere virtuele machine voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="89893-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="89893-148">U koppelen de bestaande virtuele harde schijf aan deze VM voor probleemoplossing om te bladeren en de inhoud van de schijf bewerken.</span><span class="sxs-lookup"><span data-stu-id="89893-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="89893-149">Dit proces kunt u eventuele configuratiefouten te corrigeren of extra toepassing of een systeem-logboekbestanden, bijvoorbeeld controleren.</span><span class="sxs-lookup"><span data-stu-id="89893-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="89893-150">Kies of maak een andere virtuele machine moet worden gebruikt voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="89893-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="89893-151">Koppel de bestaande virtuele harde schijf met [zonder begeleiding az vm-schijf koppelen](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="89893-151">Attach the existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="89893-152">Wanneer u de bestaande virtuele harde schijf koppelt, geeft u de URI naar de schijf die is verkregen in de voorgaande `az vm show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="89893-152">When you attach the existing virtual hard disk, specify the URI to the disk obtained in the preceding `az vm show` command.</span></span> <span data-ttu-id="89893-153">Het volgende voorbeeld wordt een bestaande virtuele harde schijf voor het oplossen van problemen met de naam VM `myVMRecovery` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89893-153">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="89893-154">Koppel de gekoppelde gegevensschijf</span><span class="sxs-lookup"><span data-stu-id="89893-154">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="89893-155">De volgende voorbeelden worden de stappen die nodig is op een VM Ubuntu in detail beschreven.</span><span class="sxs-lookup"><span data-stu-id="89893-155">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="89893-156">Als u gebruikmaakt van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE, de locaties van het logboekbestand en `mount` opdrachten mogelijk enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="89893-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="89893-157">Raadpleeg de documentatie voor uw specifieke distro voor de benodigde wijzigingen in de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="89893-157">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="89893-158">SSH met uw probleemoplossing virtuele machine met de juiste referenties.</span><span class="sxs-lookup"><span data-stu-id="89893-158">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="89893-159">Als u deze schijf is de eerste gegevensschijf gekoppeld aan uw VM voor het oplossen van problemen, de schijf waarschijnlijk is verbonden met `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="89893-159">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="89893-160">Gebruik `dmseg` om gekoppelde schijven weer te geven:</span><span class="sxs-lookup"><span data-stu-id="89893-160">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="89893-161">De uitvoer lijkt op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="89893-161">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="89893-162">In het voorgaande voorbeeld de OS-schijf is op `/dev/sda` en de tijdelijke schijf die is opgegeven voor elke virtuele machine is op `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="89893-162">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="89893-163">Als u meerdere gegevensschijven had, moeten ze op `/dev/sdd`, `/dev/sde`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="89893-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="89893-164">Maak een map voor het koppelen van uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="89893-164">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="89893-165">Het volgende voorbeeld wordt een map met de naam `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="89893-165">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="89893-166">Als u meerdere partities op de bestaande virtuele harde schijf hebt, koppelt u de vereiste partitie.</span><span class="sxs-lookup"><span data-stu-id="89893-166">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="89893-167">Het volgende voorbeeld koppelt de eerste primaire partitie op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="89893-167">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="89893-168">Er is een aanbevolen procedure gegevensschijven koppelen aan virtuele machines in Azure met behulp van de UUID universally unique identifier () van de virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="89893-168">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="89893-169">In dit scenario voor korte voor probleemoplossing voor is het koppelen van de virtuele harde schijf met de UUID niet nodig.</span><span class="sxs-lookup"><span data-stu-id="89893-169">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="89893-170">Echter, bij normaal gebruik bewerken `/etc/fstab` koppelen van virtuele harde schijven met de apparaatnaam van het in plaats van UUID kan ertoe leiden dat de virtuele machine niet kunnen worden opgestart.</span><span class="sxs-lookup"><span data-stu-id="89893-170">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="89893-171">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="89893-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="89893-172">Met de bestaande virtuele harde schijf dat wordt gekoppeld, kunt u nu onderhoud en stappen voor probleemoplossing naar behoefte uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="89893-172">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="89893-173">Zodra u de problemen hebt opgelost, kunt u doorgaan met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="89893-173">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="89893-174">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="89893-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="89893-175">Zodra de fouten opgelost zijn, kunt u ontkoppelen en loskoppelen van de bestaande virtuele harde schijf van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="89893-175">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="89893-176">U kunt de virtuele harde schijf niet gebruiken met eventuele andere virtuele machine totdat de lease koppelen van de virtuele harde schijf voor het oplossen van problemen VM is uitgebracht.</span><span class="sxs-lookup"><span data-stu-id="89893-176">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="89893-177">Ontkoppel de bestaande virtuele harde schijf van de SSH-sessie voor uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="89893-177">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="89893-178">Eerst buiten de bovenliggende map voor uw koppelpunt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="89893-178">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="89893-179">Nu Ontkoppel de bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="89893-179">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="89893-180">Het volgende voorbeeld het apparaat op ontkoppelt `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="89893-180">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="89893-181">Nu loskoppelen van de virtuele harde schijf van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="89893-181">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="89893-182">De SSH-sessie voor de probleemoplossing VM afsluiten.</span><span class="sxs-lookup"><span data-stu-id="89893-182">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="89893-183">Lijst van de schijven bijgesloten gegevens voor uw VM het oplossen van problemen met [az vm zonder begeleiding schijf lijst](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="89893-183">List the attached data disks to your troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="89893-184">Het volgende voorbeeld worden de gegevensschijven gekoppeld aan de virtuele machine met de naam `myVMRecovery` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89893-184">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="89893-185">Noteer de naam van uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="89893-185">Note the name for your existing virtual hard disk.</span></span> <span data-ttu-id="89893-186">Bijvoorbeeld, de naam van een schijf met de URI van **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="89893-186">For example, the name of a disk with the URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="89893-187">Ontkoppel de gegevensschijf van uw VM [zonder begeleiding az vm-schijf loskoppelen](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="89893-187">Detach the data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="89893-188">Het volgende voorbeeld wordt losgekoppeld van de schijf met de naam `myVHD` van de virtuele machine met de naam `myVMRecovery` in de `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="89893-188">The following example detaches the disk named `myVHD` from the VM named `myVMRecovery` in the `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="89893-189">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="89893-189">Create VM from original hard disk</span></span>
<span data-ttu-id="89893-190">Gebruik voor het maken van een virtuele machine van de oorspronkelijke virtuele harde schijf [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="89893-190">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="89893-191">De werkelijke JSON-sjabloon is op de volgende koppeling:</span><span class="sxs-lookup"><span data-stu-id="89893-191">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="89893-192">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="89893-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="89893-193">De sjabloon implementeert u een virtuele machine met behulp van de VHD-URI van de vorige opdracht.</span><span class="sxs-lookup"><span data-stu-id="89893-193">The template deploys a VM using the VHD URI from the earlier command.</span></span> <span data-ttu-id="89893-194">Implementeren van de sjabloon met [az implementatie maken](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="89893-194">Deploy the template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="89893-195">De URI voor uw oorspronkelijke VHD bieden en geef het type besturingssysteem, de VM-grootte en de naam van de VM als volgt:</span><span class="sxs-lookup"><span data-stu-id="89893-195">Provide the URI to your original VHD and then specify the OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="89893-196">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="89893-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="89893-197">Wanneer u uw virtuele machine van de bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="89893-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="89893-198">Schakel diagnostische gegevens over opstarten met [az vm-diagnostische gegevens over opstarten inschakelen](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="89893-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="89893-199">Het volgende voorbeeld wordt de diagnostische uitbreiding op de virtuele machine met de naam `myDeployedVM` in de resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89893-199">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="89893-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="89893-200">Next steps</span></span>
<span data-ttu-id="89893-201">Als u verbinding maakt met uw virtuele machine problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen met een Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89893-201">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="89893-202">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="89893-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>