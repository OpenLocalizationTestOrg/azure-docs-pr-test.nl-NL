---
title: aaaUse een Linux VM Hello Azure CLI 1.0 probleemoplossing | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Linux VM verstrekt via verbindende Hallo OS schijf tooa herstel VM hello Azure CLI 1.0
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 398f681d1149299d444fcfdab20737315db02855
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-cli-10"></a><span data-ttu-id="31c96-103">Linux-VM oplossen door het Hallo OS tooa schijfherstel VM koppelen met behulp van Azure CLI 1.0 Hallo</span><span class="sxs-lookup"><span data-stu-id="31c96-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="31c96-104">Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf.</span><span class="sxs-lookup"><span data-stu-id="31c96-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="31c96-105">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` dat verhindert Hallo VM kunnen tooboot is.</span><span class="sxs-lookup"><span data-stu-id="31c96-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="31c96-106">De details van dit artikel hoe toouse hello Azure CLI 1.0 tooconnect uw virtuele harde schijf tooanother Linux VM toofix geen fouten bevat en klik vervolgens opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="31c96-106">This article details how toouse hello Azure CLI 1.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="31c96-107">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="31c96-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="31c96-108">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="31c96-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="31c96-109">[Azure CLI 1.0](#recovery-process-overview) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="31c96-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="31c96-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="31c96-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="31c96-111">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="31c96-111">Recovery process overview</span></span>
<span data-ttu-id="31c96-112">Hallo procedure voor probleemoplossing is als volgt:</span><span class="sxs-lookup"><span data-stu-id="31c96-112">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="31c96-113">Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="31c96-113">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="31c96-114">Koppelen en koppelen van Hallo virtuele harde schijf tooanother Linux-VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="31c96-114">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="31c96-115">Verbinding maken met toohello VM probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="31c96-115">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="31c96-116">Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-116">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="31c96-117">Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="31c96-117">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="31c96-118">Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-118">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="31c96-119">Zorg ervoor dat u hebt [nieuwste Azure CLI 1.0 Hallo](../../cli-install-nodejs.md) geïnstalleerd en geregistreerd in en gebruikt de modus Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="31c96-119">Make sure that you have [hello latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="31c96-120">In Hallo vervangen volgende voorbeelden parameternamen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="31c96-120">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="31c96-121">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="31c96-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="31c96-122">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="31c96-122">Determine boot issues</span></span>
<span data-ttu-id="31c96-123">Hallo seriële uitvoer toodetermine waarom uw virtuele machine niet kunnen tooboot correct is onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="31c96-123">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="31c96-124">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of Hallo onderliggende virtuele harde schijf wordt verwijderd of verplaatst.</span><span class="sxs-lookup"><span data-stu-id="31c96-124">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="31c96-125">Hallo volgende voorbeeld krijgt Hallo seriële uitvoer van Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-125">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="31c96-126">Hallo seriële uitvoer toodetermine waarom hello VM tooboot mislukt bekijken.</span><span class="sxs-lookup"><span data-stu-id="31c96-126">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="31c96-127">Als Hallo seriële uitvoer is niet een aanwijzing bieden, moet u mogelijk de logboekbestanden tooreview in `/var/log` zodra er Hallo virtuele harde schijf tooa probleemoplossing VM gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="31c96-127">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="31c96-128">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="31c96-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="31c96-129">Voordat u uw virtuele harde schijf tooanother VM koppelen kunt, moet u tooidentify Hallo-naam van Hallo virtuele harde schijf (VHD).</span><span class="sxs-lookup"><span data-stu-id="31c96-129">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="31c96-130">Hallo volgende voorbeeld worden gegevens opgehaald voor virtuele machine met de naam Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-130">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="31c96-131">Zoek naar `Vhd URI` in Hallo-uitvoer van de voorgaande opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="31c96-131">Look for `Vhd URI` in hello output from hello preceding command.</span></span> <span data-ttu-id="31c96-132">Hallo volgende ingekorte voorbeelduitvoer wordt weergegeven Hallo `Vhd URI` op Hallo laatste regel:</span><span class="sxs-lookup"><span data-stu-id="31c96-132">hello following truncated example output shows hello `Vhd URI` on hello last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myVM"
+ Looking up hello NIC "myNic"
+ Looking up hello public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="31c96-133">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="31c96-133">Delete existing VM</span></span>
<span data-ttu-id="31c96-134">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="31c96-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="31c96-135">Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="31c96-135">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="31c96-136">Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="31c96-136">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="31c96-137">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM.</span><span class="sxs-lookup"><span data-stu-id="31c96-137">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="31c96-138">Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="31c96-138">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="31c96-139">Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="31c96-139">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="31c96-140">eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf.</span><span class="sxs-lookup"><span data-stu-id="31c96-140">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="31c96-141">Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="31c96-141">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="31c96-142">Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.</span><span class="sxs-lookup"><span data-stu-id="31c96-142">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="31c96-143">Hallo volgende voorbeeld verwijdert met de naam VM Hallo `myVM` van Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="31c96-144">Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="31c96-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="31c96-145">Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="31c96-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="31c96-146">Bestaande virtuele harde schijf tooanother VM koppelen</span><span class="sxs-lookup"><span data-stu-id="31c96-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="31c96-147">Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="31c96-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="31c96-148">U koppelt Hallo bestaande virtuele harde schijf toothis VM toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="31c96-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="31c96-149">Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="31c96-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="31c96-150">Kies of maak een ander VM-toouse voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="31c96-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="31c96-151">Wanneer u een bestaande virtuele harde schijf van Hallo koppelt, geef Hallo URL toohello schijf verkregen in de voorgaande Hallo `azure vm show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="31c96-151">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `azure vm show` command.</span></span> <span data-ttu-id="31c96-152">Hallo volgende voorbeeld wordt een bestaande virtuele harde schijf toohello het oplossen van problemen met de naam VM `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-152">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="31c96-153">Hallo bijgesloten gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="31c96-153">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="31c96-154">Hallo beschreven hieronder Hallo stappen vereist op een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="31c96-154">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="31c96-155">Als u van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE gebruikmaakt, Hallo locaties logboekbestand en `mount` opdrachten mogelijk enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="31c96-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="31c96-156">Raadpleeg toohello-documentatie voor uw specifieke distro voor Hallo benodigde wijzigingen in de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="31c96-156">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="31c96-157">SSH-tooyour het oplossen van problemen met de juiste referenties Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="31c96-157">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="31c96-158">Als deze schijf Hallo eerste gegevens schijf is gekoppeld aan tooyour VM probleemoplossing, Hallo is waarschijnlijk verbonden schijf te`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="31c96-158">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="31c96-159">Gebruik `dmseg` tooview gekoppelde schijven:</span><span class="sxs-lookup"><span data-stu-id="31c96-159">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="31c96-160">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="31c96-160">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="31c96-161">In de Hallo voorgaande voorbeeld, Hallo OS-schijf is op `/dev/sda` en Hallo tijdelijke schijf opgegeven voor elke virtuele machine is op `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="31c96-161">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="31c96-162">Als u meerdere gegevensschijven had, moeten ze op `/dev/sdd`, `/dev/sde`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="31c96-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="31c96-163">Maak een map toomount uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-163">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="31c96-164">Hallo volgende voorbeeld maakt u een map met de naam `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="31c96-164">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="31c96-165">Als u meerdere partities op de bestaande virtuele harde schijf hebt, koppel Hallo vereist partitie.</span><span class="sxs-lookup"><span data-stu-id="31c96-165">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="31c96-166">Hallo volgende voorbeeld koppelt Hallo eerste primaire partitie op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="31c96-166">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="31c96-167">Aanbevolen procedure is toomount gegevensschijven op virtuele machines in Azure worden verkregen met Hallo (UUID) universally unique identifier van Hallo virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-167">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="31c96-168">Voor dit scenario voor de korte voor probleemoplossing is koppelen Hallo virtuele harde schijf met behulp van Hallo UUID niet nodig.</span><span class="sxs-lookup"><span data-stu-id="31c96-168">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="31c96-169">Echter, bij normaal gebruik bewerken `/etc/fstab` toomount virtuele harde schijven met de apparaatnaam van het in plaats van UUID kan ertoe leiden dat Hallo VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="31c96-169">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="31c96-170">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="31c96-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="31c96-171">Hallo bestaande virtuele harde schijf gekoppeld, kunt u eventuele onderhoud en probleemoplossing naar behoefte nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="31c96-171">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="31c96-172">Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="31c96-172">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="31c96-173">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="31c96-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="31c96-174">Zodra de fouten opgelost zijn, kunt u ontkoppelen en Hallo bestaande virtuele harde schijf los te koppelen van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="31c96-174">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="31c96-175">U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="31c96-175">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="31c96-176">Ontkoppelen van Hallo SSH-sessie tooyour VM probleemoplossing, Hallo bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-176">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="31c96-177">Eerst buiten Hallo van de bovenliggende map voor uw koppelpunt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="31c96-177">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="31c96-178">Nu Ontkoppel Hallo bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-178">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="31c96-179">Hallo volgende voorbeeld ontkoppelt Hallo-apparaat op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="31c96-179">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="31c96-180">Nu loskoppelen Hallo virtuele harde schijf van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="31c96-180">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="31c96-181">Hallo SSH-sessie tooyour probleemoplossing VM af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="31c96-181">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="31c96-182">Eerste lijst Hallo gekoppeld in hello Azure CLI, gegevens schijven tooyour VM probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="31c96-182">In hello Azure CLI, first list hello attached data disks tooyour troubleshooting VM.</span></span> <span data-ttu-id="31c96-183">Hallo volgt een lijst met gegevensschijven Hallo gekoppeld toohello VM met de naam `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-183">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="31c96-184">Opmerking Hallo `Lun` waarde voor de bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="31c96-184">Note hello `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="31c96-185">Hallo volgende opdracht voorbeelduitvoer wordt weergegeven Hallo bestaande virtuele schijf voor LUN 0 is gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="31c96-185">hello following example command output shows hello existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up hello VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="31c96-186">Hallo gegevensschijf loskoppelen van uw virtuele machine met behulp van toepassing hello `Lun` waarde:</span><span class="sxs-lookup"><span data-stu-id="31c96-186">Detach hello data disk from your VM using hello applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="31c96-187">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="31c96-187">Create VM from original hard disk</span></span>
<span data-ttu-id="31c96-188">toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="31c96-188">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="31c96-189">Hallo werkelijke JSON-sjabloon is op Hallo koppeling:</span><span class="sxs-lookup"><span data-stu-id="31c96-189">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="31c96-190">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="31c96-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="31c96-191">Hallo sjabloon een virtuele machine implementeert in een bestaand virtueel netwerk met behulp van Hallo VHD URL uit Hallo eerder opdracht.</span><span class="sxs-lookup"><span data-stu-id="31c96-191">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="31c96-192">Hallo volgende voorbeeld implementeert Hallo sjabloon toohello resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-192">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="31c96-193">Antwoord Hallo vraagt om Hallo sjabloon zoals VM-naam (`myDeployedVM` Hallo volgende voorbeeld), type besturingssysteem (`Linux`), en VM-grootte (`Standard_DS1_v2`).</span><span class="sxs-lookup"><span data-stu-id="31c96-193">Answer hello prompts for hello template such as VM name (`myDeployedVM` hello following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="31c96-194">Hallo `osDiskVhdUri` is dezelfde als eerder is gebruikt bij het toevoegen van Hallo bestaande virtuele harde schijf toohello probleemoplossing VM Hallo.</span><span class="sxs-lookup"><span data-stu-id="31c96-194">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span> <span data-ttu-id="31c96-195">Een voorbeeld van uitvoer van de opdracht Hallo en wordt u gevraagd is als volgt:</span><span class="sxs-lookup"><span data-stu-id="31c96-195">An example of hello command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment toocomplete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="31c96-196">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="31c96-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="31c96-197">Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="31c96-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="31c96-198">Hallo volgende voorbeeld wordt de diagnostische Hallo-extensie op Hallo VM met de naam `myDeployedVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="31c96-198">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="31c96-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31c96-199">Next steps</span></span>
<span data-ttu-id="31c96-200">Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31c96-200">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="31c96-201">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="31c96-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
