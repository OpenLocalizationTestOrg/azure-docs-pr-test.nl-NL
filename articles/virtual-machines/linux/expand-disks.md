---
title: Vouw de virtuele harde schijven op een Linux VM in Azure | Microsoft Docs
description: Meer informatie over het uitbreiden van de virtuele harde schijven op een Linux-VM met de Azure CLI 2.0
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
ms.openlocfilehash: b82cc0473c003da767ee230ab485c69b233977d1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-expand-virtual-hard-disks-on-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="3797c-103">Het uitbreiden van de virtuele harde schijven op een Linux-VM met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3797c-103">How to expand virtual hard disks on a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="3797c-104">Grootte van de virtuele harde schijf voor het besturingssysteem (OS) is doorgaans 30 GB op een Linux virtuele machine (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="3797c-104">The default virtual hard disk size for the operating system (OS) is typically 30 GB on a Linux virtual machine (VM) in Azure.</span></span> <span data-ttu-id="3797c-105">U kunt [gegevensschijven toevoegen](add-disk.md) te voorzien in extra opslagruimte, maar u kunnen ook desgewenst een bestaande gegevensschijf wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="3797c-105">You can [add data disks](add-disk.md) to provide for additional storage space, but you may also wish to expand an existing data disk.</span></span> <span data-ttu-id="3797c-106">Dit artikel wordt uitgelegd hoe u beheerde schijven voor een Linux-VM met de Azure CLI 2.0 uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="3797c-106">This article details how to expand managed disks for a Linux VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="3797c-107">U kunt ook uitbreiden met de niet-beheerde OS-schijf met de [Azure CLI 1.0](expand-disks-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3797c-107">You can also expand the unmanaged OS disk with the [Azure CLI 1.0](expand-disks-nodejs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="3797c-108">Zorg er altijd dat u maakt u een back-up van uw gegevens voordat u de schijf uitvoert de grootte van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="3797c-108">Always make sure that you back up your data before you perform disk resize operations.</span></span> <span data-ttu-id="3797c-109">Zie voor meer informatie [Back-up van Linux virtuele machines in Azure](tutorial-backup-vms.md).</span><span class="sxs-lookup"><span data-stu-id="3797c-109">For more information, see [Back up Linux VMs in Azure](tutorial-backup-vms.md).</span></span>

## <a name="expand-disk"></a><span data-ttu-id="3797c-110">Schijf uitbreiden</span><span class="sxs-lookup"><span data-stu-id="3797c-110">Expand disk</span></span>
<span data-ttu-id="3797c-111">Zorg ervoor dat u de meest recente hebt [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3797c-111">Make sure that you have the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3797c-112">In dit artikel is een bestaande virtuele machine in Azure met ten minste één schijf met gegevens die zijn gekoppeld en voorbereid vereist.</span><span class="sxs-lookup"><span data-stu-id="3797c-112">This article requires an existing VM in Azure with at least one data disk attached and prepared.</span></span> <span data-ttu-id="3797c-113">Als u nog geen een virtuele machine die u kunt gebruiken, raadpleegt u [maken en voorbereiden van een virtuele machine met gegevensschijven](tutorial-manage-disks.md#create-and-attach-disks).</span><span class="sxs-lookup"><span data-stu-id="3797c-113">If you do not already have a VM that you can use, see [Create and prepare a VM with data disks](tutorial-manage-disks.md#create-and-attach-disks).</span></span>

<span data-ttu-id="3797c-114">In de volgende voorbeelden kunt u de parameternamen voorbeeld vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="3797c-114">In the following samples, replace example parameter names with your own values.</span></span> <span data-ttu-id="3797c-115">De namen van de voorbeeld-parameter *myResourceGroup* en *myVM*.</span><span class="sxs-lookup"><span data-stu-id="3797c-115">Example parameter names include *myResourceGroup* and *myVM*.</span></span>

1. <span data-ttu-id="3797c-116">Bewerkingen op virtuele harde schijven kunnen niet worden uitgevoerd met de virtuele machine uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3797c-116">Operations on virtual hard disks cannot be performed with the VM running.</span></span> <span data-ttu-id="3797c-117">Toewijzing van uw virtuele machine met [az vm ongedaan](/cli/azure/vm#deallocate).</span><span class="sxs-lookup"><span data-stu-id="3797c-117">Deallocate your VM with [az vm deallocate](/cli/azure/vm#deallocate).</span></span> <span data-ttu-id="3797c-118">Het volgende voorbeeld de virtuele machine met de naam deallocates *myVM* in de resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3797c-118">The following example deallocates the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > <span data-ttu-id="3797c-119">`az vm stop`Geeft de rekenresources niet vrij.</span><span class="sxs-lookup"><span data-stu-id="3797c-119">`az vm stop` does not release the compute resources.</span></span> <span data-ttu-id="3797c-120">Gebruik om rekenresources release `az vm deallocate`.</span><span class="sxs-lookup"><span data-stu-id="3797c-120">To release compute resources, use `az vm deallocate`.</span></span> <span data-ttu-id="3797c-121">De virtuele machine moet ongedaan als u de virtuele harde schijf wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="3797c-121">The VM must be deallocated to expand the virtual hard disk.</span></span>

2. <span data-ttu-id="3797c-122">Een lijst met beheerde schijven weergeven in een resourcegroep met [az Schijflijst](/cli/azure/disk#list).</span><span class="sxs-lookup"><span data-stu-id="3797c-122">View a list of managed disks in a resource group with [az disk list](/cli/azure/disk#list).</span></span> <span data-ttu-id="3797c-123">Het volgende voorbeeld wordt een lijst met beheerde schijven in de resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3797c-123">The following example displays a list of managed disks in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    <span data-ttu-id="3797c-124">Vouw de benodigde schijfruimte met [az schijf update](/cli/azure/disk#update).</span><span class="sxs-lookup"><span data-stu-id="3797c-124">Expand the required disk with [az disk update](/cli/azure/disk#update).</span></span> <span data-ttu-id="3797c-125">Het volgende voorbeeld wordt de beheerde schijf met de naam *myDataDisk* worden *200*Gb in grootte:</span><span class="sxs-lookup"><span data-stu-id="3797c-125">The following example expands the managed disk named *myDataDisk* to be *200*Gb in size:</span></span>

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > <span data-ttu-id="3797c-126">Wanneer u een beheerde schijf uitbreidt, worden de bijgewerkte grootte is toegewezen aan de dichtstbijzijnde beheerde schijfgrootte.</span><span class="sxs-lookup"><span data-stu-id="3797c-126">When you expand a managed disk, the updated size is mapped to the nearest managed disk size.</span></span> <span data-ttu-id="3797c-127">Zie voor een tabel van de beschikbare beheerde schijfgrootten en lagen [beheerd schijven overzicht van Azure - prijzen en facturering](../windows/managed-disks-overview.md#pricing-and-billing).</span><span class="sxs-lookup"><span data-stu-id="3797c-127">For a table of the available managed disk sizes and tiers, see [Azure Managed Disks Overview - Pricing and Billing](../windows/managed-disks-overview.md#pricing-and-billing).</span></span>

3. <span data-ttu-id="3797c-128">Start de virtuele machine met [az vm start](/cli/azure/vm#start).</span><span class="sxs-lookup"><span data-stu-id="3797c-128">Start your VM with [az vm start](/cli/azure/vm#start).</span></span> <span data-ttu-id="3797c-129">Het volgende voorbeeld wordt de virtuele machine met de naam *myVM* in de resourcegroep met de naam *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="3797c-129">The following example starts the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. <span data-ttu-id="3797c-130">SSH met uw virtuele machine met de juiste referenties.</span><span class="sxs-lookup"><span data-stu-id="3797c-130">SSH to your VM with the appropriate credentials.</span></span> <span data-ttu-id="3797c-131">U kunt het openbare IP-adres van uw virtuele machine met verkrijgen [az vm weergeven](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="3797c-131">You can obtain the public IP address of your VM with [az vm show](/cli/azure/vm#show):</span></span>

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. <span data-ttu-id="3797c-132">Voor het gebruik van de uitgevouwen schijf, moet u de onderliggende partitie en bestandssysteem uitvouwen.</span><span class="sxs-lookup"><span data-stu-id="3797c-132">To use the expanded disk, you need to expand the underlying partition and filesystem.</span></span>

    <span data-ttu-id="3797c-133">a.</span><span class="sxs-lookup"><span data-stu-id="3797c-133">a.</span></span> <span data-ttu-id="3797c-134">Als al is gekoppeld, ontkoppelt u de schijf:</span><span class="sxs-lookup"><span data-stu-id="3797c-134">If already mounted, unmount the disk:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

    <span data-ttu-id="3797c-135">b.</span><span class="sxs-lookup"><span data-stu-id="3797c-135">b.</span></span> <span data-ttu-id="3797c-136">Gebruik `parted` schijfgegevens wilt bekijken en grootte van de partitie:</span><span class="sxs-lookup"><span data-stu-id="3797c-136">Use `parted` to view disk information and resize the partition:</span></span>

    ```bash
    sudo parted /dev/sdc
    ```

    <span data-ttu-id="3797c-137">Informatie weergeven over de bestaande partitie-indeling met `print`.</span><span class="sxs-lookup"><span data-stu-id="3797c-137">View information about the existing partition layout with `print`.</span></span> <span data-ttu-id="3797c-138">De uitvoer is vergelijkbaar met het volgende voorbeeld, waarin dat de onderliggende schijf 215Gb groot is:</span><span class="sxs-lookup"><span data-stu-id="3797c-138">The output is similar to the following example, which shows the underlying disk is 215Gb in size:</span></span>

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome to GNU Parted! Type 'help' to view a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    <span data-ttu-id="3797c-139">c.</span><span class="sxs-lookup"><span data-stu-id="3797c-139">c.</span></span> <span data-ttu-id="3797c-140">Vouw de partitie met `resizepart`.</span><span class="sxs-lookup"><span data-stu-id="3797c-140">Expand the partition with `resizepart`.</span></span> <span data-ttu-id="3797c-141">Voer het partitienummer *1*, en een grootte voor de nieuwe partitie:</span><span class="sxs-lookup"><span data-stu-id="3797c-141">Enter the partition number, *1*, and a size for the new partition:</span></span>

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    <span data-ttu-id="3797c-142">d.</span><span class="sxs-lookup"><span data-stu-id="3797c-142">d.</span></span> <span data-ttu-id="3797c-143">Voer om af te sluiten`quit`</span><span class="sxs-lookup"><span data-stu-id="3797c-143">To exit, enter `quit`</span></span>

5. <span data-ttu-id="3797c-144">Bij de partitie is gewijzigd, Controleer de consistentie van de partitie met `e2fsck`:</span><span class="sxs-lookup"><span data-stu-id="3797c-144">With the partition resized, verify the partition consistency with `e2fsck`:</span></span>

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. <span data-ttu-id="3797c-145">Nu het formaat van het bestandssysteem met `resize2fs`:</span><span class="sxs-lookup"><span data-stu-id="3797c-145">Now resize the filesystem with `resize2fs`:</span></span>

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. <span data-ttu-id="3797c-146">Koppelen van de partitie naar de gewenste locatie, zoals `/datadrive`:</span><span class="sxs-lookup"><span data-stu-id="3797c-146">Mount the partition to the desired location, such as `/datadrive`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. <span data-ttu-id="3797c-147">Gebruiken om te controleren of de grootte van de besturingssysteemschijf is gewijzigd, `df -h`.</span><span class="sxs-lookup"><span data-stu-id="3797c-147">To verify the OS disk has been resized, use `df -h`.</span></span> <span data-ttu-id="3797c-148">De volgende voorbeelduitvoer wordt weergegeven voor het gegevensstation */dev/sdc1*, is nu 200 GB:</span><span class="sxs-lookup"><span data-stu-id="3797c-148">The following example output shows the data drive, */dev/sdc1*, is now 200 GB:</span></span>

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a><span data-ttu-id="3797c-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3797c-149">Next steps</span></span>
<span data-ttu-id="3797c-150">Als u extra opslagruimte, moet u ook [gegevensschijven toevoegen aan een Linux-VM](add-disk.md).</span><span class="sxs-lookup"><span data-stu-id="3797c-150">If you need additional storage, you also [add data disks to a Linux VM](add-disk.md).</span></span> <span data-ttu-id="3797c-151">Zie voor meer informatie over schijfversleuteling [schijven op een Linux-VM met de Azure CLI versleutelen](encrypt-disks.md).</span><span class="sxs-lookup"><span data-stu-id="3797c-151">For more information about disk encryption, see [Encrypt disks on a Linux VM using the Azure CLI](encrypt-disks.md).</span></span>
