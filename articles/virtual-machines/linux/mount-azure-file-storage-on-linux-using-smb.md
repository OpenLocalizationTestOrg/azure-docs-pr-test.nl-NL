---
title: Azure File storage in virtuele Linux-machines met SMB aaaMount | Microsoft Docs
description: Hoe toomount Azure File storage in virtuele Linux-machines met SMB met Azure CLI 2.0 Hallo
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 7b34c81e602748b78c924f44a54b876744c28f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="8ea56-103">Koppelpunt Azure File storage in virtuele Linux-machines met SMB</span><span class="sxs-lookup"><span data-stu-id="8ea56-103">Mount Azure File storage on Linux VMs using SMB</span></span>

<span data-ttu-id="8ea56-104">Dit artikel laat zien hoe tooutilize hello Azure File storage-service op een Linux-VM met behulp van SMB Hello Azure CLI 2.0 koppelen.</span><span class="sxs-lookup"><span data-stu-id="8ea56-104">This article shows you how tooutilize hello Azure File storage service on a Linux VM using an SMB mount with hello Azure CLI 2.0.</span></span> <span data-ttu-id="8ea56-105">Azure File storage biedt bestandsshares in de cloud van Hallo Hallo standaard SMB-protocol gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ea56-105">Azure File storage offers file shares in hello cloud using hello standard SMB protocol.</span></span> <span data-ttu-id="8ea56-106">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8ea56-106">You can also perform these steps with hello [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="8ea56-107">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="8ea56-107">hello requirements are:</span></span>

- [<span data-ttu-id="8ea56-108">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="8ea56-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="8ea56-109">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="8ea56-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="8ea56-110">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="8ea56-110">Quick Commands</span></span>

* <span data-ttu-id="8ea56-111">Een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="8ea56-111">A resource group</span></span>
* <span data-ttu-id="8ea56-112">Een Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="8ea56-112">An Azure virtual network</span></span>
* <span data-ttu-id="8ea56-113">Een netwerkbeveiligingsgroep met een SSH inkomende</span><span class="sxs-lookup"><span data-stu-id="8ea56-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="8ea56-114">Een subnet</span><span class="sxs-lookup"><span data-stu-id="8ea56-114">A subnet</span></span>
* <span data-ttu-id="8ea56-115">Een Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="8ea56-115">An Azure storage account</span></span>
* <span data-ttu-id="8ea56-116">Sleutels voor Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="8ea56-116">Azure storage account keys</span></span>
* <span data-ttu-id="8ea56-117">Een Azure File storage-share</span><span class="sxs-lookup"><span data-stu-id="8ea56-117">An Azure File storage share</span></span>
* <span data-ttu-id="8ea56-118">Een virtuele Linux-machine</span><span class="sxs-lookup"><span data-stu-id="8ea56-118">A Linux VM</span></span>

<span data-ttu-id="8ea56-119">Geen voorbeelden vervangen door uw eigen instellingen.</span><span class="sxs-lookup"><span data-stu-id="8ea56-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-hello-local-mount"></a><span data-ttu-id="8ea56-120">Maak een map voor lokale koppeling Hallo</span><span class="sxs-lookup"><span data-stu-id="8ea56-120">Create a directory for hello local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-hello-file-storage-smb-share-toohello-mount-point"></a><span data-ttu-id="8ea56-121">Hallo bestand opslag toohello koppelpunt wordt gehost SMB-share koppelen</span><span class="sxs-lookup"><span data-stu-id="8ea56-121">Mount hello File storage SMB share toohello mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-hello-mount-after-a-reboot"></a><span data-ttu-id="8ea56-122">Hallo koppelpunt behouden na opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="8ea56-122">Persist hello mount after a reboot</span></span>
<span data-ttu-id="8ea56-123">toodo toevoegen dus Hallo regel toohello na `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="8ea56-123">toodo so, add hello following line toohello `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="8ea56-124">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="8ea56-124">Detailed walkthrough</span></span>

<span data-ttu-id="8ea56-125">File storage biedt bestandsshares in de cloud Hallo Hallo standaard SMB-protocol gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ea56-125">File storage offers file shares in hello cloud that use hello standard SMB protocol.</span></span> <span data-ttu-id="8ea56-126">Met de meest recente release van File storage Hallo kunt u ook een bestandsshare koppelen vanuit elk besturingssysteem dat ondersteuning biedt voor SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="8ea56-126">With hello latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="8ea56-127">Als u een SMB-koppelen op Linux gebruikt, krijgt u eenvoudig back-ups tooa robuuste, permanente archiveren locatie voor de opslag die wordt ondersteund door een SLA.</span><span class="sxs-lookup"><span data-stu-id="8ea56-127">When you use an SMB mount on Linux, you get easy backups tooa robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="8ea56-128">Verplaatsen van bestanden in een VM tooan SMB koppelpunt wordt gehost op File storage is dat een uitstekende manier toodebug registreert.</span><span class="sxs-lookup"><span data-stu-id="8ea56-128">Moving files from a VM tooan SMB mount that's hosted on File storage is a great way toodebug logs.</span></span> <span data-ttu-id="8ea56-129">Dat komt doordat Hallo dezelfde SMB-share worden gekoppeld, lokaal tooyour Mac, Linux of Windows-werkstation.</span><span class="sxs-lookup"><span data-stu-id="8ea56-129">That's because hello same SMB share can be mounted locally tooyour Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="8ea56-130">SMB niet Hallo beste oplossing voor het streamen van Linux of toepassingslogboeken in real-time, omdat Hallo SMB-protocol niet is ingebouwd toohandle deze rechten zware logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="8ea56-130">SMB isn't hello best solution for streaming Linux or application logs in real time, because hello SMB protocol is not built toohandle such heavy logging duties.</span></span> <span data-ttu-id="8ea56-131">Een speciale, uniforme logboekregistratie laag hulpprogramma zoals Fluentd zou een betere keuze dan SMB zijn voor het verzamelen van Linux- en uitvoer logboekregistratie toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ea56-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="8ea56-132">Voor deze gedetailleerde procedure maken we Hallo vereisten nodig toofirst Hallo File storage-share maken en klik vervolgens op een Linux-VM via SMB koppelen.</span><span class="sxs-lookup"><span data-stu-id="8ea56-132">For this detailed walkthrough, we create hello prerequisites needed toofirst create hello File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="8ea56-133">Maak een resourcegroep met [az groep maken](/cli/azure/group#create) toohold Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="8ea56-133">Create a resource group with [az group create](/cli/azure/group#create) toohold hello file share.</span></span>

    <span data-ttu-id="8ea56-134">een resourcegroep met de naam toocreate `myResourceGroup` in Hallo 'VS-West' locatie, gebruikt u Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ea56-134">toocreate a resource group named `myResourceGroup` in hello "West US" location, use hello following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="8ea56-135">Maken van een Azure storage-account met [az storage-account maken](/cli/azure/storage/account#create) toostore Hallo bestanden.</span><span class="sxs-lookup"><span data-stu-id="8ea56-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) toostore hello actual files.</span></span>

    <span data-ttu-id="8ea56-136">toocreate een opslagaccount met de naam mystorageaccount hello Standard_LRS opslag SKU, gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ea56-136">toocreate a storage account named mystorageaccount by using hello Standard_LRS storage SKU, use hello following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="8ea56-137">Hallo-toegangscodes voor opslag weergeven.</span><span class="sxs-lookup"><span data-stu-id="8ea56-137">Show hello storage account keys.</span></span>

    <span data-ttu-id="8ea56-138">Wanneer u een opslagaccount maakt, worden de Hallo toegangscodes zodat ze kunnen worden gedraaid zonder onderbreking van de service in paren worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ea56-138">When you create a storage account, hello account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="8ea56-139">Wanneer u de tweede sleutel toohello Hallo paar overschakelt, maakt u een nieuw sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="8ea56-139">When you switch toohello second key in hello pair, you create a new key pair.</span></span> <span data-ttu-id="8ea56-140">Nieuwe toegangscodes voor opslag worden altijd paarsgewijs ervoor te zorgen dat u altijd ten minste één niet-gebruikte opslag account key gereed tooswitch te hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ea56-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready tooswitch to.</span></span>

    <span data-ttu-id="8ea56-141">Hallo opslagaccountsleutels Hello weergeven [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="8ea56-141">View hello storage account keys with hello [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="8ea56-142">Hallo toegangscodes voor opslag voor Hallo met de naam `mystorageaccount` worden vermeld in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ea56-142">hello storage account keys for hello named `mystorageaccount` are listed in hello following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="8ea56-143">tooextract één sleutel gebruiken Hallo `--query` vlag.</span><span class="sxs-lookup"><span data-stu-id="8ea56-143">tooextract a single key, use hello `--query` flag.</span></span> <span data-ttu-id="8ea56-144">Hallo volgende voorbeeld worden de eerste sleutel hello (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="8ea56-144">hello following example extracts hello first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="8ea56-145">Hallo File storage-share maken.</span><span class="sxs-lookup"><span data-stu-id="8ea56-145">Create hello File storage share.</span></span>

    <span data-ttu-id="8ea56-146">Hallo File storage-share bevat met de SMB-share Hallo [az storage-share maken](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="8ea56-146">hello File storage share contains hello SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="8ea56-147">Hallo quotum wordt altijd uitgedrukt in gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="8ea56-147">hello quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="8ea56-148">Doorgeven in een Hallo sleutels uit voorgaande Hallo `az storage account keys list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="8ea56-148">Pass in one of hello keys from hello preceding `az storage account keys list` command.</span></span> <span data-ttu-id="8ea56-149">Maak een share met de naam mystorageshare met een target 10 GB met behulp van Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ea56-149">Create a share named mystorageshare with a 10-GB quota by using hello following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="8ea56-150">Maak een map koppelpunt.</span><span class="sxs-lookup"><span data-stu-id="8ea56-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="8ea56-151">Een lokale map maken in Hallo Linux bestand system toomount Hallo naar de SMB-share.</span><span class="sxs-lookup"><span data-stu-id="8ea56-151">Create a local directory in hello Linux file system toomount hello SMB share to.</span></span> <span data-ttu-id="8ea56-152">Geschreven of gelezen uit de lokale Koppelmap Hallo wordt toohello SMB-share die wordt gehost op de opslag van bestanden doorgestuurd.</span><span class="sxs-lookup"><span data-stu-id="8ea56-152">Anything written or read from hello local mount directory is forwarded toohello SMB share that's hosted on File storage.</span></span> <span data-ttu-id="8ea56-153">toocreate een lokale map op/mnt/mymountdirectory, gebruik Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ea56-153">toocreate a local directory at /mnt/mymountdirectory, use hello following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="8ea56-154">Hallo SMB-share toohello lokale directory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="8ea56-154">Mount hello SMB share toohello local directory.</span></span>

    <span data-ttu-id="8ea56-155">Geef uw eigen storage account gebruikersnaam en het opslagaccountsleutel voor Hallo koppelpunt referenties als volgt:</span><span class="sxs-lookup"><span data-stu-id="8ea56-155">Provide your own storage account username and storage account key for hello mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="8ea56-156">Bewaren Hallo SMB koppelen via opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="8ea56-156">Persist hello SMB mount through reboots.</span></span>

    <span data-ttu-id="8ea56-157">Wanneer u de computer opnieuw Hallo Linux VM opstart, is hello gekoppelde SMB-share ontkoppeld tijdens het afsluiten.</span><span class="sxs-lookup"><span data-stu-id="8ea56-157">When you reboot hello Linux VM, hello mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="8ea56-158">tooremount hello SMB-share opstart, een regel toohello Linux /etc/fstab toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8ea56-158">tooremount hello SMB share on boot, add a line toohello Linux /etc/fstab.</span></span> <span data-ttu-id="8ea56-159">Hallo fstab-bestand toolist Hallo bestandssystemen toomount moet tijdens het opstartproces Hallo maakt gebruik van Linux.</span><span class="sxs-lookup"><span data-stu-id="8ea56-159">Linux uses hello fstab file toolist hello file systems that it needs toomount during hello boot process.</span></span> <span data-ttu-id="8ea56-160">Toe te voegen Hallo SMB-share zorgt ervoor dat Hallo File storage-share is een permanent gekoppelde bestandssysteem voor Hallo Linux VM.</span><span class="sxs-lookup"><span data-stu-id="8ea56-160">Adding hello SMB share ensures that hello File storage share is a permanently mounted file system for hello Linux VM.</span></span> <span data-ttu-id="8ea56-161">Hallo bestand opslag SMB-share tooa toe te voegen is nieuwe virtuele machine mogelijk wanneer u cloud-init gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ea56-161">Adding hello File storage SMB share tooa new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="8ea56-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ea56-162">Next steps</span></span>

- [<span data-ttu-id="8ea56-163">Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="8ea56-163">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="8ea56-164">Voeg een schijf tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="8ea56-164">Add a disk tooa Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="8ea56-165">Versleutelen van schijven op een Linux-VM met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8ea56-165">Encrypt disks on a Linux VM by using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
