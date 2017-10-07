---
title: aaaCreate en het uploaden van een OpenBSD VM image tooAzure | Microsoft Docs
description: Meer informatie over hoe toocreate en het uploaden van een virtuele harde schijf (VHD) die bevat Hallo OpenBSD besturingssysteem toocreate een virtuele machine van Azure via Azure CLI
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="336aa-103">Maken en een tooAzure OpenBSD schijf installatiekopie uploaden</span><span class="sxs-lookup"><span data-stu-id="336aa-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="336aa-104">Dit artikel laat zien hoe Hallo besturingssysteem OpenBSD toocreate en het uploaden van een virtuele harde schijf (VHD) die bevat.</span><span class="sxs-lookup"><span data-stu-id="336aa-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="336aa-105">Nadat u deze uploaden, kunt u deze kunt gebruiken als uw eigen toocreate installatiekopie van een virtuele machine (VM) in Azure via Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="336aa-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="336aa-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="336aa-106">Prerequisites</span></span>
<span data-ttu-id="336aa-107">In dit artikel wordt ervan uitgegaan dat u hebt Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="336aa-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="336aa-108">**Een Azure-abonnement** -als u geen account hebt, kunt u een in een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="336aa-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="336aa-109">Als u een MSDN-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="336aa-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="336aa-110">Anders wordt informatie over hoe te[maken van een gratis proefaccount](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="336aa-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="336aa-111">**Azure CLI 2.0** -Controleer of er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-azure-cli) geïnstalleerd en geregistreerd in tooyour Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="336aa-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="336aa-112">**OpenBSD-besturingssysteem is geïnstalleerd in een .vhd-bestand** -een ondersteund besturingssysteem van OpenBSD (versie 6.1) moet geïnstalleerde tooa virtuele hardeschijf.</span><span class="sxs-lookup"><span data-stu-id="336aa-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="336aa-113">Meerdere hulpprogramma's bestaan toocreate VHD-bestanden.</span><span class="sxs-lookup"><span data-stu-id="336aa-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="336aa-114">U kunt bijvoorbeeld een oplossing voor netwerkvirtualisatie gebruiken zoals Hyper-V toocreate Hallo .vhd-bestand en Hallo-besturingssysteem installeren.</span><span class="sxs-lookup"><span data-stu-id="336aa-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="336aa-115">Voor instructies over hoe tooinstall en het gebruik van Hyper-V, Zie [Hyper-V installeren en een virtuele machine maken](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="336aa-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="336aa-116">De installatiekopie van het OpenBSD voorbereiden voor Azure</span><span class="sxs-lookup"><span data-stu-id="336aa-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="336aa-117">Voer op Hallo VM waar u Hallo OpenBSD besturingssysteem geïnstalleerd 6,1, Hyper-V-ondersteuning wordt toegevoegd en Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="336aa-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="336aa-118">Als DHCP niet is ingeschakeld tijdens de installatie, het Hallo-service als volgt inschakelen:</span><span class="sxs-lookup"><span data-stu-id="336aa-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="336aa-119">Stel een seriële console als volgt in:</span><span class="sxs-lookup"><span data-stu-id="336aa-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="336aa-120">De installatie van pakket als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="336aa-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="336aa-121">Standaard Hallo `root` gebruiker is uitgeschakeld op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="336aa-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="336aa-122">Gebruikers kunnen opdrachten uitvoeren met verhoogde bevoegdheden via Hallo `doas` opdracht op OpenBSD VM.</span><span class="sxs-lookup"><span data-stu-id="336aa-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="336aa-123">Doas is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="336aa-123">Doas is enabled by default.</span></span> <span data-ttu-id="336aa-124">Zie voor meer informatie [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="336aa-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="336aa-125">Installeren en configureren van vereisten voor hello Azure Agent als volgt:</span><span class="sxs-lookup"><span data-stu-id="336aa-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="336aa-126">meest recente versie van de Hallo Hallo Azure-agent altijd vindt u op [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="336aa-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="336aa-127">Hallo-agent als volgt installeren:</span><span class="sxs-lookup"><span data-stu-id="336aa-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="336aa-128">Nadat u Azure-Agent hebt geïnstalleerd, is het een goed idee tooverify dat deze wordt als volgt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="336aa-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="336aa-129">Identiteitsgegevens Hallo system tooclean deze en maak deze geschikt is voor reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="336aa-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="336aa-130">Hallo volgende opdracht ook verwijderd Hallo laatste ingerichte gebruiker serviceaccount en Hallo die zijn gekoppeld:</span><span class="sxs-lookup"><span data-stu-id="336aa-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="336aa-131">U kunt nu uw virtuele machine afsluiten.</span><span class="sxs-lookup"><span data-stu-id="336aa-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="336aa-132">Hallo VHD voorbereiden</span><span class="sxs-lookup"><span data-stu-id="336aa-132">Prepare hello VHD</span></span>
<span data-ttu-id="336aa-133">Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**.</span><span class="sxs-lookup"><span data-stu-id="336aa-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="336aa-134">U kunt converteren Hallo schijf toofixed VHD-indeling met behulp van Hyper-V-beheer of Powershell Hallo [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="336aa-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="336aa-135">Een voorbeeld is als volgende.</span><span class="sxs-lookup"><span data-stu-id="336aa-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="336aa-136">Storage-resources maken en uploaden</span><span class="sxs-lookup"><span data-stu-id="336aa-136">Create storage resources and upload</span></span>
<span data-ttu-id="336aa-137">Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="336aa-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="336aa-138">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:</span><span class="sxs-lookup"><span data-stu-id="336aa-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="336aa-139">tooupload uw VHD maken van een opslagaccount met [az storage-account maken](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="336aa-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="336aa-140">Namen van opslagaccounts moeten uniek zijn, zodat uw eigen naam opgeven.</span><span class="sxs-lookup"><span data-stu-id="336aa-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="336aa-141">Hallo volgende voorbeeld wordt een opslagaccount met de naam *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="336aa-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="336aa-142">toocontrol toegang tot het opslagaccount toohello, krijgen Hallo-opslagsleutel met [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list) als volgt:</span><span class="sxs-lookup"><span data-stu-id="336aa-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="336aa-143">toologically afzonderlijke Hallo VHD's die u uploadt, maak een container in Hallo storage-account met [az storage-container maken](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="336aa-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="336aa-144">Ten slotte uw VHD met uploaden [uploaden van blob storage az](/cli/azure/storage/blob#upload) als volgt:</span><span class="sxs-lookup"><span data-stu-id="336aa-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="336aa-145">Virtuele machine van de VHD maken</span><span class="sxs-lookup"><span data-stu-id="336aa-145">Create VM from your VHD</span></span>
<span data-ttu-id="336aa-146">U kunt maken met een virtuele machine een [voorbeeldscript](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) of rechtstreeks met [az vm maken](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="336aa-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="336aa-147">toospecify OpenBSD VHD u hebt geüpload, gebruik Hallo Hallo `--image` parameter als volgt:</span><span class="sxs-lookup"><span data-stu-id="336aa-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="336aa-148">Hallo IP-adres verkrijgen voor uw VM OpenBSD met [az vm lijst-ip-adressen](/cli/azure/vm#list-ip-addresses) als volgt:</span><span class="sxs-lookup"><span data-stu-id="336aa-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="336aa-149">U kunt nu SSH tooyour OpenBSD VM als normale:</span><span class="sxs-lookup"><span data-stu-id="336aa-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="336aa-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="336aa-150">Next steps</span></span>
<span data-ttu-id="336aa-151">Desgewenst kunt u meer informatie over Hyper-V op OpenBSD6.1 ondersteunen tooknow lezen [OpenBSD 6.1](https://www.openbsd.org/61.html) en [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="336aa-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="336aa-152">Desgewenst kunt u een virtuele machine van de beheerde schijf toocreate lezen [az schijf](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="336aa-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
