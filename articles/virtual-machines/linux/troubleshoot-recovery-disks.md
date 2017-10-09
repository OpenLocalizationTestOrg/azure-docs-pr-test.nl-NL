---
title: aaaUse een Linux VM Hello Azure CLI 2.0 probleemoplossing | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot Linux VM verstrekt via verbindende Hallo OS schijf tooa herstel VM hello Azure CLI 2.0
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
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="44cde-103">Linux-VM oplossen door het koppelen van Hallo OS tooa schijfherstel VM Hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="44cde-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="44cde-104">Als uw virtuele Linux-machine (VM) een opstart- of -fout optreedt, moet u mogelijk tooperform stappen voor probleemoplossing in het virtuele harde schijf hello, zelf.</span><span class="sxs-lookup"><span data-stu-id="44cde-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="44cde-105">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab` dat verhindert Hallo VM kunnen tooboot is.</span><span class="sxs-lookup"><span data-stu-id="44cde-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="44cde-106">De details van dit artikel hoe toouse hello Azure CLI 2.0 tooconnect uw virtuele harde schijf tooanother Linux VM toofix geen fouten bevat en klik vervolgens opnieuw maken van de oorspronkelijke VM.</span><span class="sxs-lookup"><span data-stu-id="44cde-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="44cde-107">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44cde-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="44cde-108">Overzicht van het herstelproces</span><span class="sxs-lookup"><span data-stu-id="44cde-108">Recovery process overview</span></span>
<span data-ttu-id="44cde-109">Hallo procedure voor probleemoplossing is als volgt:</span><span class="sxs-lookup"><span data-stu-id="44cde-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="44cde-110">Verwijder Hallo VM zonder problemen Hallo virtuele harde schijven te houden.</span><span class="sxs-lookup"><span data-stu-id="44cde-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="44cde-111">Koppelen en koppelen van Hallo virtuele harde schijf tooanother Linux-VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="44cde-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="44cde-112">Verbinding maken met toohello VM probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="44cde-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="44cde-113">Bestanden bewerken of toofix problemen van alle hulpprogramma's uitvoeren op Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="44cde-114">Ontkoppel en Hallo virtuele harde schijf van Hallo probleemoplossing VM loskoppelen.</span><span class="sxs-lookup"><span data-stu-id="44cde-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="44cde-115">Een virtuele machine maken met Hallo oorspronkelijke virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="44cde-116">tooperform deze probleemoplossingsstappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="44cde-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="44cde-117">In Hallo vervangen volgende voorbeelden parameternamen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="44cde-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="44cde-118">De namen van de voorbeeld-parameter `myResourceGroup`, `mystorageaccount`, en `myVM`.</span><span class="sxs-lookup"><span data-stu-id="44cde-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="44cde-119">Opstartproblemen bepalen</span><span class="sxs-lookup"><span data-stu-id="44cde-119">Determine boot issues</span></span>
<span data-ttu-id="44cde-120">Hallo seriële uitvoer toodetermine waarom uw virtuele machine niet kunnen tooboot correct is onderzoeken.</span><span class="sxs-lookup"><span data-stu-id="44cde-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="44cde-121">Een veelvoorkomend voorbeeld is een ongeldige waarde in `/etc/fstab`, of Hallo onderliggende virtuele harde schijf wordt verwijderd of verplaatst.</span><span class="sxs-lookup"><span data-stu-id="44cde-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="44cde-122">Hallo opstarten logboeken met [az vm diagnostische gegevens over opstarten get-boot-logboek](/cli/azure/vm/boot-diagnostics#get-boot-log).</span><span class="sxs-lookup"><span data-stu-id="44cde-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="44cde-123">Hallo volgende voorbeeld krijgt Hallo seriële uitvoer van Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="44cde-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="44cde-124">Hallo seriële uitvoer toodetermine waarom hello VM tooboot mislukt bekijken.</span><span class="sxs-lookup"><span data-stu-id="44cde-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="44cde-125">Als Hallo seriële uitvoer is niet een aanwijzing bieden, moet u mogelijk de logboekbestanden tooreview in `/var/log` zodra er Hallo virtuele harde schijf tooa probleemoplossing VM gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="44cde-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="44cde-126">Bestaande virtuele harde schijf details weergeven</span><span class="sxs-lookup"><span data-stu-id="44cde-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="44cde-127">Voordat u uw virtuele harde schijf (VHD) tooanother VM koppelen kunt, moet u tooidentify Hallo-URI van de besturingssysteemschijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="44cde-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="44cde-128">Informatie weergeven over uw virtuele machine met [az vm weergeven](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="44cde-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="44cde-129">Gebruik Hallo `--query` vlag tooextract Hallo URI toohello OS-schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="44cde-130">Hallo volgende voorbeeld wordt opgehaald schijfgegevens voor virtuele machine met de naam Hallo `myVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="44cde-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="44cde-131">Hallo URI lijkt te**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span><span class="sxs-lookup"><span data-stu-id="44cde-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="44cde-132">Bestaande virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="44cde-132">Delete existing VM</span></span>
<span data-ttu-id="44cde-133">Virtuele harde schijven en virtuele machines zijn twee verschillende resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="44cde-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="44cde-134">Een virtuele harde schijf is waar Hallo besturingssysteem zelf, toepassingen en configuraties worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="44cde-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="44cde-135">Hallo VM zelf zijn gewoon metagegevens die definieert Hallo grootte of de locatie en verwijst naar resources, zoals een virtuele harde schijf of virtuele netwerkinterfacekaart (NIC).</span><span class="sxs-lookup"><span data-stu-id="44cde-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="44cde-136">Elke virtuele harde schijf heeft een lease toegewezen wanneer gekoppeld tooa VM.</span><span class="sxs-lookup"><span data-stu-id="44cde-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="44cde-137">Hoewel gegevensschijven kunnen worden gekoppeld en ontkoppeld, zelfs wanneer Hallo VM wordt uitgevoerd, kan de besturingssysteemschijf Hallo kan niet worden losgekoppeld tenzij Hallo VM-resource wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="44cde-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="44cde-138">Hallo lease blijft tooassociate Hallo OS-schijf met een virtuele machine, zelfs wanneer die VM een status gestopt en de toewijzing ongedaan is gemaakt heeft.</span><span class="sxs-lookup"><span data-stu-id="44cde-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="44cde-139">eerste stap toorecover Hallo uw VM is toodelete Hallo VM-resource zelf.</span><span class="sxs-lookup"><span data-stu-id="44cde-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="44cde-140">Verwijderen Hallo VM verlaat Hallo virtuele harde schijven in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="44cde-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="44cde-141">Na het Hallo die virtuele machine is verwijderd, Hallo virtuele harde schijf tooanother VM tootroubleshoot koppelen en Hallo fouten op te lossen.</span><span class="sxs-lookup"><span data-stu-id="44cde-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="44cde-142">Verwijderen met virtuele machine Hallo [az vm verwijderen](/cli/azure/vm#delete).</span><span class="sxs-lookup"><span data-stu-id="44cde-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="44cde-143">Hallo volgende voorbeeld verwijdert met de naam VM Hallo `myVM` van Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="44cde-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="44cde-144">Wacht totdat het Hallo VM verwijderen voordat u Hallo virtuele harde schijf tooanother VM koppelen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="44cde-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="44cde-145">Hallo-lease op het virtuele harde schijf hello, waarin deze zijn gekoppeld aan VM Hallo moet toobe vrijgegeven voordat u Hallo virtuele harde schijf tooanother VM kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="44cde-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="44cde-146">Bestaande virtuele harde schijf tooanother VM koppelen</span><span class="sxs-lookup"><span data-stu-id="44cde-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="44cde-147">Voor Hallo volgende stappen, u een andere virtuele machine gebruiken voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="44cde-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="44cde-148">U koppelt Hallo bestaande virtuele harde schijf toothis VM toobrowse probleemoplossing en inhoud van de schijf Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="44cde-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="44cde-149">Dit proces kunt u toocorrect eventuele fouten in de configuratie of revisie aanvullende toepassings- of logboekbestanden, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="44cde-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="44cde-150">Kies of maak een ander VM-toouse voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="44cde-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="44cde-151">Koppel Hallo bestaande virtuele harde schijf met [zonder begeleiding az vm-schijf koppelen](/cli/azure/vm/unmanaged-disk#attach).</span><span class="sxs-lookup"><span data-stu-id="44cde-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="44cde-152">Wanneer u een bestaande virtuele harde schijf van Hallo koppelt, geef Hallo URI toohello schijf verkregen in de voorgaande Hallo `az vm show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="44cde-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="44cde-153">Hallo volgende voorbeeld wordt een bestaande virtuele harde schijf toohello het oplossen van problemen met de naam VM `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="44cde-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="44cde-154">Hallo bijgesloten gegevensschijf koppelen</span><span class="sxs-lookup"><span data-stu-id="44cde-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="44cde-155">Hallo beschreven hieronder Hallo stappen vereist op een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="44cde-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="44cde-156">Als u van een andere Linux distro zoals Red Hat Enterprise Linux of SUSE gebruikmaakt, Hallo locaties logboekbestand en `mount` opdrachten mogelijk enigszins anders.</span><span class="sxs-lookup"><span data-stu-id="44cde-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="44cde-157">Raadpleeg toohello-documentatie voor uw specifieke distro voor Hallo benodigde wijzigingen in de opdrachten.</span><span class="sxs-lookup"><span data-stu-id="44cde-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="44cde-158">SSH-tooyour het oplossen van problemen met de juiste referenties Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="44cde-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="44cde-159">Als deze schijf Hallo eerste gegevens schijf is gekoppeld aan tooyour VM probleemoplossing, Hallo is waarschijnlijk verbonden schijf te`/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="44cde-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="44cde-160">Gebruik `dmseg` tooview gekoppelde schijven:</span><span class="sxs-lookup"><span data-stu-id="44cde-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="44cde-161">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="44cde-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="44cde-162">In de Hallo voorgaande voorbeeld, Hallo OS-schijf is op `/dev/sda` en Hallo tijdelijke schijf opgegeven voor elke virtuele machine is op `/dev/sdb`.</span><span class="sxs-lookup"><span data-stu-id="44cde-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="44cde-163">Als u meerdere gegevensschijven had, moeten ze op `/dev/sdd`, `/dev/sde`, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="44cde-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="44cde-164">Maak een map toomount uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="44cde-165">Hallo volgende voorbeeld maakt u een map met de naam `troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="44cde-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="44cde-166">Als u meerdere partities op de bestaande virtuele harde schijf hebt, koppel Hallo vereist partitie.</span><span class="sxs-lookup"><span data-stu-id="44cde-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="44cde-167">Hallo volgende voorbeeld koppelt Hallo eerste primaire partitie op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="44cde-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="44cde-168">Aanbevolen procedure is toomount gegevensschijven op virtuele machines in Azure worden verkregen met Hallo (UUID) universally unique identifier van Hallo virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="44cde-169">Voor dit scenario voor de korte voor probleemoplossing is koppelen Hallo virtuele harde schijf met behulp van Hallo UUID niet nodig.</span><span class="sxs-lookup"><span data-stu-id="44cde-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="44cde-170">Echter, bij normaal gebruik bewerken `/etc/fstab` toomount virtuele harde schijven met de apparaatnaam van het in plaats van UUID kan ertoe leiden dat Hallo VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="44cde-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="44cde-171">Los problemen op de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="44cde-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="44cde-172">Hallo bestaande virtuele harde schijf gekoppeld, kunt u eventuele onderhoud en probleemoplossing naar behoefte nu uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="44cde-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="44cde-173">Zodra u Hallo problemen hebt opgelost, kunt u doorgaan met de Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="44cde-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="44cde-174">Ontkoppel en loskoppelen van de oorspronkelijke virtuele harde schijf</span><span class="sxs-lookup"><span data-stu-id="44cde-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="44cde-175">Zodra de fouten opgelost zijn, kunt u ontkoppelen en Hallo bestaande virtuele harde schijf los te koppelen van uw VM voor het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="44cde-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="44cde-176">U kunt de virtuele harde schijf niet gebruiken met een andere VM tot Hallo lease Hallo virtuele harde schijf toohello probleemoplossing VM koppelen is vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="44cde-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="44cde-177">Ontkoppelen van Hallo SSH-sessie tooyour VM probleemoplossing, Hallo bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="44cde-178">Eerst buiten Hallo van de bovenliggende map voor uw koppelpunt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="44cde-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="44cde-179">Nu Ontkoppel Hallo bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="44cde-180">Hallo volgende voorbeeld ontkoppelt Hallo-apparaat op `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="44cde-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="44cde-181">Nu loskoppelen Hallo virtuele harde schijf van Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="44cde-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="44cde-182">Hallo SSH-sessie tooyour probleemoplossing VM af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="44cde-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="44cde-183">Lijst Hallo gegevens schijven tooyour het oplossen van problemen met virtuele machine gekoppeld [az vm zonder begeleiding schijf lijst](/cli/azure/vm/unmanaged-disk#list).</span><span class="sxs-lookup"><span data-stu-id="44cde-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="44cde-184">Hallo volgt een lijst met gegevensschijven Hallo gekoppeld toohello VM met de naam `myVMRecovery` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="44cde-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="44cde-185">Houd er rekening mee Hallo-naam voor uw bestaande virtuele harde schijf.</span><span class="sxs-lookup"><span data-stu-id="44cde-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="44cde-186">Bijvoorbeeld Hallo-naam van een schijf met de URI van Hallo **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span><span class="sxs-lookup"><span data-stu-id="44cde-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="44cde-187">Hallo gegevensschijf loskoppelen van uw virtuele machine [zonder begeleiding az vm-schijf loskoppelen](/cli/azure/vm/unmanaged-disk#detach).</span><span class="sxs-lookup"><span data-stu-id="44cde-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="44cde-188">Hallo voorbeeld hieronder wordt Hallo-schijf met de naam `myVHD` van Hallo VM met de naam `myVMRecovery` in Hallo `myResourceGroup` resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="44cde-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="44cde-189">Virtuele machine van de oorspronkelijke harde schijf maken</span><span class="sxs-lookup"><span data-stu-id="44cde-189">Create VM from original hard disk</span></span>
<span data-ttu-id="44cde-190">toocreate een virtuele machine van de oorspronkelijke virtuele harde schijf gebruiken [deze Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span><span class="sxs-lookup"><span data-stu-id="44cde-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="44cde-191">Hallo werkelijke JSON-sjabloon is op Hallo koppeling:</span><span class="sxs-lookup"><span data-stu-id="44cde-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="44cde-192">https://RAW.githubusercontent.com/Azure/Azure-QuickStart-templates/master/201-VM-Specialized-VHD/azuredeploy.JSON</span><span class="sxs-lookup"><span data-stu-id="44cde-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="44cde-193">Hallo sjabloon implementeert een VM die gebruikmaakt van Hallo VHD-URI van Hallo eerder opdracht.</span><span class="sxs-lookup"><span data-stu-id="44cde-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="44cde-194">Hallo-sjabloon met implementeren [az implementatie maken](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="44cde-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="44cde-195">Hallo URI tooyour bieden oorspronkelijke VHD en geef vervolgens Hallo OS-type, de grootte van de VM en VM-naam als volgt:</span><span class="sxs-lookup"><span data-stu-id="44cde-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="44cde-196">Diagnostische gegevens over opstarten weer inschakelen</span><span class="sxs-lookup"><span data-stu-id="44cde-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="44cde-197">Wanneer u uw virtuele machine van Hallo bestaande virtuele harde schijf maakt, kan boot diagnostics niet automatisch worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="44cde-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="44cde-198">Schakel diagnostische gegevens over opstarten met [az vm-diagnostische gegevens over opstarten inschakelen](/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="44cde-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="44cde-199">Hallo volgende voorbeeld wordt de diagnostische Hallo-extensie op Hallo VM met de naam `myDeployedVM` in Hallo resourcegroep met de naam `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="44cde-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="44cde-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44cde-200">Next steps</span></span>
<span data-ttu-id="44cde-201">Als u verbinding maken met tooyour VM problemen ondervindt, raadpleegt u [oplossen SSH-verbindingen tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44cde-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="44cde-202">Zie voor problemen met de toegang tot toepassingen die worden uitgevoerd op de virtuele machine [oplossen verbindingsproblemen van toepassing op een Linux-VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="44cde-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
