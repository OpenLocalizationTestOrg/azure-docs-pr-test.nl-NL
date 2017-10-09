---
title: Azure File storage in Linux VM's met behulp van SMB met Azure CLI 1.0 aaaMount | Microsoft Docs
description: Hoe toomount Azure File storage in Linux VM's via SMB
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
ms.openlocfilehash: 14a4224228cadb0ae2f05e8e5c8022ee84f138a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="aa082-103">Koppelpunt Azure File storage in Linux VM's met behulp van SMB met Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="aa082-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="aa082-104">Dit artikel laat zien hoe toomount Azure File storage in een Linux-VM met behulp van Server Message Block (SMB)-protocol Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa082-104">This article shows how toomount Azure File storage on a Linux VM by using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="aa082-105">File storage biedt bestandsshares in de cloud Hallo via Hallo standaard SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="aa082-105">File storage offers file shares in hello cloud via hello standard SMB protocol.</span></span> <span data-ttu-id="aa082-106">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="aa082-106">hello requirements are:</span></span>

* <span data-ttu-id="aa082-107">Een [Azure-account](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="aa082-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="aa082-108">Secure Shell (SSH) openbare en persoonlijke sleutelbestanden</span><span class="sxs-lookup"><span data-stu-id="aa082-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-toouse"></a><span data-ttu-id="aa082-109">CLI-versies toouse</span><span class="sxs-lookup"><span data-stu-id="aa082-109">CLI versions toouse</span></span>
<span data-ttu-id="aa082-110">U kunt Hallo taak uitvoeren met behulp van een van de volgende versies van de opdrachtregelinterface (CLI) Hallo:</span><span class="sxs-lookup"><span data-stu-id="aa082-110">You can complete hello task by using one of hello following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="aa082-111">[Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="aa082-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="aa082-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)-onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="aa082-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="aa082-113">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="aa082-113">Quick commands</span></span>
<span data-ttu-id="aa082-114">tooaccomplish hello taak snel stappen Hallo in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="aa082-114">tooaccomplish hello task quickly, follow hello steps in this section.</span></span> <span data-ttu-id="aa082-115">Voor meer informatie en context gedetailleerde, beginnen op Hallo ['Gedetailleerd overzicht'](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) sectie.</span><span class="sxs-lookup"><span data-stu-id="aa082-115">For more detailed information and context, begin at hello ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aa082-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa082-116">Prerequisites</span></span>
* <span data-ttu-id="aa082-117">Een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="aa082-117">A resource group</span></span>
* <span data-ttu-id="aa082-118">Een Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="aa082-118">An Azure virtual network</span></span>
* <span data-ttu-id="aa082-119">Een netwerkbeveiligingsgroep met een SSH inkomende</span><span class="sxs-lookup"><span data-stu-id="aa082-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="aa082-120">Een subnet</span><span class="sxs-lookup"><span data-stu-id="aa082-120">A subnet</span></span>
* <span data-ttu-id="aa082-121">Een Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="aa082-121">An Azure storage account</span></span>
* <span data-ttu-id="aa082-122">Sleutels voor Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="aa082-122">Azure storage account keys</span></span>
* <span data-ttu-id="aa082-123">Een Azure File storage-share</span><span class="sxs-lookup"><span data-stu-id="aa082-123">An Azure File storage share</span></span>
* <span data-ttu-id="aa082-124">Een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="aa082-124">A Linux VM</span></span>

<span data-ttu-id="aa082-125">Geen voorbeelden vervangen door uw eigen instellingen.</span><span class="sxs-lookup"><span data-stu-id="aa082-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="aa082-126">Maak een map voor lokale koppeling Hallo</span><span class="sxs-lookup"><span data-stu-id="aa082-126">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="aa082-127">Hallo bestand opslag toohello koppelpunt wordt gehost SMB-share koppelen</span><span class="sxs-lookup"><span data-stu-id="aa082-127">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="aa082-128">Hallo koppelpunt behouden na opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="aa082-128">Persist hello mount after a reboot</span></span>
<span data-ttu-id="aa082-129">Hallo volgt regel te toevoegen`/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="aa082-129">Add hello following line too`/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="aa082-130">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="aa082-130">Detailed walkthrough</span></span>

<span data-ttu-id="aa082-131">File storage biedt bestandsshares in de cloud Hallo Hallo standaard SMB-protocol gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa082-131">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="aa082-132">Met de meest recente release van File storage Hallo kunt u ook een bestandsshare koppelen vanuit elk besturingssysteem dat ondersteuning biedt voor SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="aa082-132">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="aa082-133">Als u een SMB-koppelen op Linux gebruikt, krijgt u eenvoudig back-ups tooa robuuste, permanente archiveren locatie voor de opslag die wordt ondersteund door een SLA.</span><span class="sxs-lookup"><span data-stu-id="aa082-133">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="aa082-134">Verplaatsen van bestanden in een VM tooan SMB koppelpunt wordt gehost op File storage is dat een uitstekende manier toodebug registreert.</span><span class="sxs-lookup"><span data-stu-id="aa082-134">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="aa082-135">Dat komt doordat Hallo dezelfde SMB-share worden gekoppeld, lokaal tooyour Mac, Linux of Windows-werkstation.</span><span class="sxs-lookup"><span data-stu-id="aa082-135">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="aa082-136">SMB niet Hallo beste oplossing voor het streamen van Linux of toepassingslogboeken in real-time, omdat Hallo SMB-protocol niet is ingebouwd toohandle deze rechten zware logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="aa082-136">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="aa082-137">Een speciale, uniforme logboekregistratie laag hulpprogramma zoals Fluentd zou een betere keuze dan SMB zijn voor het verzamelen van Linux- en uitvoer logboekregistratie toepassing.</span><span class="sxs-lookup"><span data-stu-id="aa082-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="aa082-138">Voor deze gedetailleerde procedure maken we Hallo vereisten nodig toofirst Hallo File storage-share maken en klik vervolgens op een Linux-VM via SMB koppelen.</span><span class="sxs-lookup"><span data-stu-id="aa082-138">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="aa082-139">Een Azure storage-account maken met behulp van de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="aa082-139">Create an Azure storage account by using hello following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="aa082-140">Hallo-toegangscodes voor opslag weergeven.</span><span class="sxs-lookup"><span data-stu-id="aa082-140">Show hello storage account keys.</span></span>

    <span data-ttu-id="aa082-141">Wanneer u een opslagaccount maakt, worden de Hallo toegangscodes zodat ze kunnen worden gedraaid zonder onderbreking van de service in paren worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa082-141">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="aa082-142">Wanneer u de tweede sleutel toohello Hallo paar overschakelt, maakt u een nieuw sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="aa082-142">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="aa082-143">Nieuwe toegangscodes voor opslag worden altijd paarsgewijs ervoor te zorgen dat u altijd ten minste één niet-gebruikte opslag sleutel gereed tooswitch te hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa082-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready tooswitch to.</span></span> <span data-ttu-id="aa082-144">tooshow-opslagaccountsleutels voor Hallo Hallo volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="aa082-144">tooshow hello storage account keys, use hello following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="aa082-145">Hallo File storage-share maken.</span><span class="sxs-lookup"><span data-stu-id="aa082-145">Create hello File storage share.</span></span>

    <span data-ttu-id="aa082-146">Hallo File storage-share bevat Hallo SMB-share.</span><span class="sxs-lookup"><span data-stu-id="aa082-146">hello File storage share contains hello SMB share.</span></span> <span data-ttu-id="aa082-147">Hallo quotum wordt altijd uitgedrukt in gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="aa082-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="aa082-148">toocreate Hallo File storage-share, Hallo volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="aa082-148">toocreate hello File storage share, use hello following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="aa082-149">Hallo koppelpunt map maken.</span><span class="sxs-lookup"><span data-stu-id="aa082-149">Create hello mount-point directory.</span></span>

    <span data-ttu-id="aa082-150">U moet een lokale map maken in Hallo Linux bestand system toomount Hallo naar de SMB-share.</span><span class="sxs-lookup"><span data-stu-id="aa082-150">You must create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="aa082-151">Geschreven of gelezen uit de lokale Koppelmap Hallo wordt toohello SMB-share die wordt gehost op de opslag van bestanden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="aa082-151">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="aa082-152">toocreate hello directory gebruik Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa082-152">toocreate hello directory, use hello following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="aa082-153">SMB-share met behulp van de volgende code Hallo Hallo koppelen:</span><span class="sxs-lookup"><span data-stu-id="aa082-153">Mount hello SMB share by using hello following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="aa082-154">Bewaren Hallo SMB koppelen via opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="aa082-154">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="aa082-155">Wanneer u de computer opnieuw Hallo Linux VM opstart, is hello gekoppelde SMB-share ontkoppeld tijdens het afsluiten.</span><span class="sxs-lookup"><span data-stu-id="aa082-155">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="aa082-156">tooremount hello SMB-share op opstarten, moet u een regel toohello Linux /etc/fstab toevoegen.</span><span class="sxs-lookup"><span data-stu-id="aa082-156">tooremount hello SMB share on boot, you must add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="aa082-157">Hallo fstab-bestand toolist Hallo bestandssystemen toomount moet tijdens het opstartproces Hallo maakt gebruik van Linux.</span><span class="sxs-lookup"><span data-stu-id="aa082-157">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="aa082-158">Toe te voegen Hallo SMB-share zorgt ervoor dat Hallo File storage-share is een permanent gekoppelde bestandssysteem voor Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="aa082-158">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="aa082-159">Hallo bestand opslag SMB-share tooa toe te voegen is nieuwe virtuele machine mogelijk wanneer u cloud-init gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa082-159">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="aa082-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa082-160">Next steps</span></span>

- [<span data-ttu-id="aa082-161">Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="aa082-161">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="aa082-162">Voeg een schijf tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="aa082-162">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="aa082-163">Versleutelen van schijven op een Linux-VM met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aa082-163">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
