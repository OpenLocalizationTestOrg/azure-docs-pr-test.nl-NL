---
title: Koppelpunt Azure File storage in Linux VM's met behulp van SMB met Azure CLI 1.0 | Microsoft Docs
description: Het koppelen van Azure File storage op Linux VM's via SMB
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: 4951860630f0aad107d0846d52ebe4423ee0b91c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="f1be0-103">Koppelpunt Azure File storage in Linux VM's met behulp van SMB met Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f1be0-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="f1be0-104">In dit artikel laat zien hoe Azure File storage koppelen aan een Linux-VM met behulp van het protocol Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="f1be0-104">This article shows how to mount Azure File storage on a Linux VM by using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="f1be0-105">File storage biedt bestandsshares in de cloud via het standaard SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="f1be0-105">File storage offers file shares in the cloud via the standard SMB protocol.</span></span> <span data-ttu-id="f1be0-106">De vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="f1be0-106">The requirements are:</span></span>

* <span data-ttu-id="f1be0-107">Een [Azure-account](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="f1be0-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="f1be0-108">Secure Shell (SSH) openbare en persoonlijke sleutelbestanden</span><span class="sxs-lookup"><span data-stu-id="f1be0-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-to-use"></a><span data-ttu-id="f1be0-109">CLI-versies gebruiken</span><span class="sxs-lookup"><span data-stu-id="f1be0-109">CLI versions to use</span></span>
<span data-ttu-id="f1be0-110">U kunt de taak uitvoeren met behulp van een van de volgende versies van de opdrachtregelinterface (CLI):</span><span class="sxs-lookup"><span data-stu-id="f1be0-110">You can complete the task by using one of the following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="f1be0-111">[Azure CLI 1.0](#quick-commands) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="f1be0-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f1be0-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-onze volgende generatie CLI voor de resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="f1be0-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="f1be0-113">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="f1be0-113">Quick commands</span></span>
<span data-ttu-id="f1be0-114">U kunt de taak snel doen, de stappen in deze sectie uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f1be0-114">To accomplish the task quickly, follow the steps in this section.</span></span> <span data-ttu-id="f1be0-115">Voor meer informatie en context gedetailleerde, beginnen bij de ['Gedetailleerd overzicht'](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sectie.</span><span class="sxs-lookup"><span data-stu-id="f1be0-115">For more detailed information and context, begin at the ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f1be0-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f1be0-116">Prerequisites</span></span>
* <span data-ttu-id="f1be0-117">Een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="f1be0-117">A resource group</span></span>
* <span data-ttu-id="f1be0-118">Een Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="f1be0-118">An Azure virtual network</span></span>
* <span data-ttu-id="f1be0-119">Een netwerkbeveiligingsgroep met een SSH inkomende</span><span class="sxs-lookup"><span data-stu-id="f1be0-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="f1be0-120">Een subnet</span><span class="sxs-lookup"><span data-stu-id="f1be0-120">A subnet</span></span>
* <span data-ttu-id="f1be0-121">Een Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="f1be0-121">An Azure storage account</span></span>
* <span data-ttu-id="f1be0-122">Sleutels voor Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="f1be0-122">Azure storage account keys</span></span>
* <span data-ttu-id="f1be0-123">Een Azure File storage-share</span><span class="sxs-lookup"><span data-stu-id="f1be0-123">An Azure File storage share</span></span>
* <span data-ttu-id="f1be0-124">Een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="f1be0-124">A Linux VM</span></span>

<span data-ttu-id="f1be0-125">Geen voorbeelden vervangen door uw eigen instellingen.</span><span class="sxs-lookup"><span data-stu-id="f1be0-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="f1be0-126">Maak een map voor de lokale koppeling</span><span class="sxs-lookup"><span data-stu-id="f1be0-126">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="f1be0-127">De opslag van bestanden naar het koppelpunt de SMB-share koppelen</span><span class="sxs-lookup"><span data-stu-id="f1be0-127">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="f1be0-128">De koppeling behouden na opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="f1be0-128">Persist the mount after a reboot</span></span>
<span data-ttu-id="f1be0-129">De volgende regel toe te voegen `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="f1be0-129">Add the following line to `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f1be0-130">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="f1be0-130">Detailed walkthrough</span></span>

<span data-ttu-id="f1be0-131">File storage biedt bestandsshares in de cloud die het standaard SMB-protocol gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1be0-131">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="f1be0-132">Met de meest recente versie van File storage, kunt u een bestandsshare ook koppelen vanuit elk besturingssysteem dat ondersteuning biedt voor SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="f1be0-132">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="f1be0-133">Als u een SMB-koppelen op Linux gebruikt, krijgt u eenvoudig back-ups naar een robuuste, permanente archiveren opslaglocatie die wordt ondersteund door een SLA.</span><span class="sxs-lookup"><span data-stu-id="f1be0-133">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="f1be0-134">Verplaatsen van bestanden van een virtuele machine naar een SMB-koppelpunt die wordt gehost op File storage is een uitstekende manier om de logboeken voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="f1be0-134">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="f1be0-135">Dat komt doordat de dezelfde SMB-share op de lokaal naar uw werkstation Mac, Linux of Windows worden gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f1be0-135">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="f1be0-136">SMB is de beste oplossing voor het streamen van Linux of toepassingslogboeken in real-time, omdat het SMB-protocol niet is gebouwd voor het afhandelen van deze rechten zware logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="f1be0-136">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="f1be0-137">Een speciale, uniforme logboekregistratie laag hulpprogramma zoals Fluentd zou een betere keuze dan SMB zijn voor het verzamelen van Linux- en uitvoer logboekregistratie toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1be0-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="f1be0-138">Voor deze gedetailleerde procedure we maken van de vereisten die nodig zijn voor het eerst de bestandsshare voor opslag maken en vervolgens via SMB koppelen op een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="f1be0-138">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="f1be0-139">Een Azure storage-account maken met behulp van de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f1be0-139">Create an Azure storage account by using the following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="f1be0-140">De opslagaccountsleutels weergeven.</span><span class="sxs-lookup"><span data-stu-id="f1be0-140">Show the storage account keys.</span></span>

    <span data-ttu-id="f1be0-141">Wanneer u een opslagaccount maakt, worden de sleutels in paren worden gemaakt zodat ze kunnen worden gedraaid zonder onderbreking van de service.</span><span class="sxs-lookup"><span data-stu-id="f1be0-141">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="f1be0-142">Wanneer u naar de tweede sleutel in het paar overschakelt, maakt u een nieuw sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="f1be0-142">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="f1be0-143">Nieuwe toegangscodes voor opslag worden altijd gemaakt in paren, hebt u altijd ten minste één niet-gebruikte opslagsleutel gereed om te activeren.</span><span class="sxs-lookup"><span data-stu-id="f1be0-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready to switch to.</span></span> <span data-ttu-id="f1be0-144">Als u wilt de toegangscodes voor opslag weergeven, moet u de volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f1be0-144">To show the storage account keys, use the following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="f1be0-145">De bestandsshare voor opslag maken.</span><span class="sxs-lookup"><span data-stu-id="f1be0-145">Create the File storage share.</span></span>

    <span data-ttu-id="f1be0-146">De File storage-share bevat de SMB-share.</span><span class="sxs-lookup"><span data-stu-id="f1be0-146">The File storage share contains the SMB share.</span></span> <span data-ttu-id="f1be0-147">Het quotum wordt altijd weergegeven in GB (Gigabyte).</span><span class="sxs-lookup"><span data-stu-id="f1be0-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="f1be0-148">Voor het maken van de bestandsshare voor opslag, moet u de volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f1be0-148">To create the File storage share, use the following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="f1be0-149">Maak de map koppelpunt.</span><span class="sxs-lookup"><span data-stu-id="f1be0-149">Create the mount-point directory.</span></span>

    <span data-ttu-id="f1be0-150">U moet een lokale map maken in het Linux-bestandssysteem naar de SMB-share te koppelen.</span><span class="sxs-lookup"><span data-stu-id="f1be0-150">You must create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="f1be0-151">Geschreven of gelezen uit de lokale Koppelmap wordt doorgestuurd naar de SMB-share die wordt gehost op de opslag van bestanden.</span><span class="sxs-lookup"><span data-stu-id="f1be0-151">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="f1be0-152">Als u wilt maken van de map de volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f1be0-152">To create the directory, use the following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="f1be0-153">Koppel de SMB-share met behulp van de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f1be0-153">Mount the SMB share by using the following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="f1be0-154">Behouden van de SMB-koppelpunt via opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="f1be0-154">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="f1be0-155">Wanneer u de Linux-VM opnieuw opstart, wordt tijdens het afsluiten van de gekoppelde SMB-share ontkoppeld.</span><span class="sxs-lookup"><span data-stu-id="f1be0-155">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="f1be0-156">Als u wilt opnieuw koppelen van de SMB-share op opstarten, moet u een regel toevoegen aan de /etc/fstab Linux.</span><span class="sxs-lookup"><span data-stu-id="f1be0-156">To remount the SMB share on boot, you must add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="f1be0-157">Linux gebruikt het fstab-bestand voor een lijst met de bestandssystemen die nodig is om te koppelen tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="f1be0-157">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="f1be0-158">Het toevoegen van de SMB-share zorgt ervoor dat de File storage-share een permanent gekoppelde bestandssysteem voor de Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="f1be0-158">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="f1be0-159">De File storage SMB-share toe te voegen aan een nieuwe virtuele machine is mogelijk wanneer u cloud-init gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f1be0-159">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="f1be0-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f1be0-160">Next steps</span></span>

- [<span data-ttu-id="f1be0-161">Gebruik van cloud-init voor het aanpassen van een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="f1be0-161">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="f1be0-162">Een schijf toevoegen aan een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="f1be0-162">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="f1be0-163">Versleutelen van schijven op een Linux-VM met behulp van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f1be0-163">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
