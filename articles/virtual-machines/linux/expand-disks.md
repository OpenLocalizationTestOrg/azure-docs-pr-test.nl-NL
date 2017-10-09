---
title: aaaExpand virtuele harde schijven op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe tooexpand virtuele harde schijven op een Linux-VM met Azure CLI 2.0 Hallo
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="dc277-103">Hoe tooexpand virtuele harde schijven op een Linux-VM met Azure CLI Hallo</span><span class="sxs-lookup"><span data-stu-id="dc277-103">How tooexpand virtual hard disks on a Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="dc277-104">Hallo standaardgrootte virtuele harde schijf voor Hallo besturingssysteem (OS) is doorgaans 30 GB op een Linux virtuele machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc277-104">hello default virtual hard disk size for hello operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="dc277-105">U kunt [gegevensschijven toevoegen](add-disk.md) tooprovide voor extra opslagruimte, maar u kunt ook desgewenst voor tooexpand een bestaande gegevensschijf.</span><span class="sxs-lookup"><span data-stu-id="dc277-105">You can [add data disks](add-disk.md) tooprovide for additional storage space, but you may also wish tooexpand an existing data disk.</span></span> <span data-ttu-id="dc277-106">Dit artikel wordt uitgelegd hoe tooexpand schijven voor een Linux-VM met hello Azure CLI 2.0 beheerd.</span><span class="sxs-lookup"><span data-stu-id="dc277-106">This article details how tooexpand managed disks for a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="dc277-107">U kunt ook de besturingssysteemschijf Hallo zonder begeleiding Hello uitvouwen [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="dc277-107">You can also expand hello unmanaged OS disk with hello [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="dc277-108">Zorg er altijd dat u maakt u een back-up van uw gegevens voordat u de schijf uitvoert de grootte van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="dc277-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="dc277-109">Zie voor meer informatie [Back-up van Linux virtuele machines in Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="dc277-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="dc277-110">Schijf uitbreiden</span><span class="sxs-lookup"><span data-stu-id="dc277-110">Expand disk</span></span>
<span data-ttu-id="dc277-111">Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="dc277-111">Make sure that you have hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="dc277-112">In dit artikel is een bestaande virtuele machine in Azure met ten minste één schijf met gegevens die zijn gekoppeld en voorbereid vereist.</span><span class="sxs-lookup"><span data-stu-id="dc277-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="dc277-113">Als u nog geen een virtuele machine die u kunt gebruiken, raadpleegt u [maken en voorbereiden van een virtuele machine met gegevensschijven](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="dc277-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="dc277-114">In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="dc277-114">In hello following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="dc277-115">De namen van de voorbeeld-parameter *myResourceGroup* en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="dc277-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="dc277-116">Bewerkingen op virtuele harde schijven kunnen niet worden uitgevoerd met Hallo VM uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc277-116">Operations on virtual hard disks cannot be performed with hello VM running.</span></span> <span data-ttu-id="dc277-117">Toewijzing van uw virtuele machine met [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="dc277-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="dc277-118">Hallo volgende voorbeeld deallocates Hallo VM met de naam *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="dc277-118">hello following example deallocates hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="dc277-119">`az vm stop`Geeft de rekenresources Hallo niet vrij.</span><span class="sxs-lookup"><span data-stu-id="dc277-119">`az vm stop` does not release hello compute resources.</span></span> <span data-ttu-id="dc277-120">toorelease rekenresources, gebruikt u `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="dc277-120">toorelease compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="dc277-121">Hallo VM moet ongedaan tooexpand Hallo virtuele hardeschijf.</span><span class="sxs-lookup"><span data-stu-id="dc277-121">hello VM must be deallocated tooexpand hello virtual hard disk.</span></span>

2. <span data-ttu-id="dc277-122">Een lijst met beheerde schijven weergeven in een resourcegroep met [az Schijflijst](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="dc277-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="dc277-123">Hallo volgende voorbeeld wordt een lijst met beheerde schijven in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="dc277-123">hello following example displays a list of managed disks in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="dc277-124">Vouw de benodigde schijfruimte Hallo met [az schijf update](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="dc277-124">Expand hello required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="dc277-125">Hallo volgende voorbeeld wordt uitgebreid beheerde Hallo-schijf met de naam *myDataDisk* toobe *200*Gb in grootte:</span><span class="sxs-lookup"><span data-stu-id="dc277-125">hello following example expands hello managed disk named *myDataDisk* toobe *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="dc277-126">Wanneer u een beheerde schijf wilt uitbreiden, is bijgewerkt Hallo grootte toegewezen toohello dichtstbijzijnde beheerde schijfgrootte.</span><span class="sxs-lookup"><span data-stu-id="dc277-126">When you expand a managed disk, hello updated size is mapped toohello nearest managed disk size.</span></span> <span data-ttu-id="dc277-127">Zie voor een tabel van Hallo beheerde schijfgrootten beschikbaar en lagen [beheerd schijven overzicht van Azure - prijzen en facturering](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="dc277-127">For a table of hello available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="dc277-128">Start de virtuele machine met [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="dc277-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="dc277-129">Hallo volgende voorbeeld wordt gestart met de naam VM Hallo *myVM* in Hallo resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="dc277-129">hello following example starts hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="dc277-130">SSH tooyour VM met de juiste referenties Hallo.</span><span class="sxs-lookup"><span data-stu-id="dc277-130">SSH tooyour VM with hello appropriate credentials.</span></span> <span data-ttu-id="dc277-131">U kunt verkrijgen Hallo openbare IP-adres van uw virtuele machine met [az vm weergeven](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="dc277-131">You can obtain hello public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="dc277-132">Hallo toouse schijf uitgebreid, moet u tooexpand Hallo onderliggende partitie en het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="dc277-132">toouse hello expanded disk, you need tooexpand hello underlying partition and filesystem.</span></span>

    <span data-ttu-id="dc277-133">a.</span><span class="sxs-lookup"><span data-stu-id="dc277-133">a.</span></span> <span data-ttu-id="dc277-134">Als al is gekoppeld, ontkoppelt Hallo schijf:</span><span class="sxs-lookup"><span data-stu-id="dc277-134">If already mounted, unmount hello disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="dc277-135">b.</span><span class="sxs-lookup"><span data-stu-id="dc277-135">b.</span></span> <span data-ttu-id="dc277-136">Gebruik `parted` tooview informatie schijf en het formaat Hallo-partitie:</span><span class="sxs-lookup"><span data-stu-id="dc277-136">Use `parted` tooview disk information and resize hello partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="dc277-137">Informatie weergeven over Hallo bestaande partitie-indeling met `print`.</span><span class="sxs-lookup"><span data-stu-id="dc277-137">View information about hello existing partition layout with `print`.</span></span> <span data-ttu-id="dc277-138">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld ziet u de onderliggende schijf Hallo is 215Gb groot:</span><span class="sxs-lookup"><span data-stu-id="dc277-138">hello output is similar toohello following example, which shows hello underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="dc277-139">c.</span><span class="sxs-lookup"><span data-stu-id="dc277-139">c.</span></span> <span data-ttu-id="dc277-140">Vouw Hallo-partitie met `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="dc277-140">Expand hello partition with `resizepart`.</span></span> <span data-ttu-id="dc277-141">Voer Hallo partitienummer, *1*, en een grootte voor de nieuwe partitie Hallo:</span><span class="sxs-lookup"><span data-stu-id="dc277-141">Enter hello partition number, *1*, and a size for hello new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="dc277-142">d.</span><span class="sxs-lookup"><span data-stu-id="dc277-142">d.</span></span> <span data-ttu-id="dc277-143">tooexit, invoeren`quit`</span><span class="sxs-lookup"><span data-stu-id="dc277-143">tooexit, enter `quit`</span></span>

5. <span data-ttu-id="dc277-144">Controleren met Hallo partitie is gewijzigd, Hallo partitie consistentie met `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="dc277-144">With hello partition resized, verify hello partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="dc277-145">Nu vergroten of verkleinen Hallo bestandssysteem met `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="dc277-145">Now resize hello filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="dc277-146">Koppelpunt Hallo partitie toohello gewenste locatie, zoals `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="dc277-146">Mount hello partition toohello desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="dc277-147">tooverify hello OS-schijf is gewijzigd, gebruikt u `df -h`.</span><span class="sxs-lookup"><span data-stu-id="dc277-147">tooverify hello OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="dc277-148">Hallo volgende voorbeelduitvoer toont Hallo gegevensstation, */dev/sdc1*, is nu 200 GB:</span><span class="sxs-lookup"><span data-stu-id="dc277-148">hello following example output shows hello data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="dc277-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc277-149">Next steps</span></span>
<span data-ttu-id="dc277-150">Als u extra opslagruimte, moet u ook [gegevens schijven tooa Linux VM toevoegen](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="dc277-150">If you need additional storage, you also [add data disks tooa Linux VM](add-disk.md).</span></span> <span data-ttu-id="dc277-151">Zie voor meer informatie over schijfversleuteling [versleutelen schijven op een Linux-VM met behulp van Azure CLI Hallo](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="dc277-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using hello Azure CLI](encrypt-disks.md).</span></span>
