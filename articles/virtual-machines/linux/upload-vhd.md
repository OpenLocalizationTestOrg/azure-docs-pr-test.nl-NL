---
title: aaaUpload of een kopie van een aangepaste Linux-VM met Azure CLI 2.0 | Microsoft Docs
description: "Upload of een aangepaste virtuele machine met behulp van Hallo Resource Manager-implementatiemodel en Azure CLI 2.0 Hallo kopiëren"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/06/2017
ms.author: cynthn
ms.openlocfilehash: 79af897120a6ba7f4a427ba6c7d0c31b7b870bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Linux-VM te maken van aangepaste schijf Hello Azure CLI 2.0

<!-- rename toocreate-vm-specialized -->

Dit artikel ziet u hoe tooupload een aangepaste virtuele harde schijf (VHD) of kopieer een een bestaande VHD in Azure en nieuwe virtuele Linux-machines (VM's) maken van aangepaste Hallo-schijf. U kunt installeren en configureren van een Linux distro tooyour vereisten en gebruik vervolgens deze VHD tooquickly maakt een nieuwe virtuele machine van Azure.

Als u wilt dat toocreate meerdere virtuele machines van de aangepaste schijf, maakt u een installatiekopie van een van de virtuele machine of de VHD. Zie voor meer informatie [maken van een aangepaste installatiekopie van een virtuele machine van Azure CLI Hallo met](tutorial-custom-images.md).

U hebt hiervoor twee opties:
* [Een VHD uploaden](#option-1-upload-a-specialized-vhd)
* [Kopiëren van een bestaande virtuele machine in Azure](#option-2-copy-an-existing-azure-vm)

## <a name="quick-commands"></a>Snelle opdrachten

Bij het maken van een nieuwe virtuele machine met [az vm maken](/cli/azure/vm#create) van een aangepaste of gespecialiseerde schijf u **koppelen** Hallo schijf (--koppelen-os-schijf) in plaats van een aangepaste of marketplace-installatiekopie (--afbeelding). Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* Hallo met beheerde-schijf met de naam *myManagedDisk* gemaakt op basis van uw aangepaste VHD:

```azurecli
az vm create --resource-group myResourceGroup --location eastus --name myVM \
   --os-type linux --attach-os-disk myManagedDisk
```

## <a name="requirements"></a>Vereisten
Hallo toocomplete volgende stappen die u nodig:

* Een virtuele Linux-machine die is voorbereid voor gebruik in Azure. Hallo [voorbereiden Hallo VM](#prepare-the-vm) sectie van dit artikel bevat informatie over hoe toofind distro specifieke informatie over het installeren van Azure Linux Agent (waagent) is vereist voor Hallo VM toowork correct in Azure en u toobe kunnen tooconnect Hallo tooit via SSH.
* Hallo VHD-bestand van een bestaand [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in VHD-indeling Hallo. Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:
  * Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling. Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met **qemu img converteren**.
  * U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure. Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling. Indien nodig, kunt u converteren VHDX schijven tooVHD [qemu img converteren](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [Convert-VHD](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet. Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt. U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.
> 
> 


* Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen *myResourceGroup*, *mystorageaccount*, en *mydisks*.

<a id="prepimage"> </a>

## <a name="prepare-hello-vm"></a>Hallo VM voorbereiden

Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund op Azure:

* [Op basis van centOS distributies](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Andere - niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Zie ook Hallo [opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes) voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.

> [!NOTE]
> Hallo [Azure-platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) is van toepassing tooVMs met Linux alleen met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' wanneer een van de Hallo goedgekeurde distributies wordt gebruikt in [Linux op door Azure goedgekeurde Distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="option-1-upload-a-vhd"></a>Optie 1: Een VHD uploaden

U kunt een aangepaste VHD die u hebt uitgevoerd op een lokale computer of die u hebt geëxporteerd uit een andere cloud uploaden. toouse hello VHD toocreate een nieuwe virtuele machine in Azure, moet u tooupload Hallo VHD tooa storage-account en een beheerde schijf van Hallo VHD te maken. 

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Voordat het uploaden van uw aangepaste schijf en het maken van virtuele machines, moet u eerst toocreate een resourcegroep met [az groep maken](/cli/azure/group#create).

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie: [overzicht van beheerde Azure-schijven](../windows/managed-disks-overview.md)
```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

### <a name="create-a-storage-account"></a>Een opslagaccount maken

Maken van een opslagaccount voor uw aangepaste schijf en virtuele machines met [az storage-account maken](/cli/azure/storage/account#create). 

Hallo volgende voorbeeld wordt een opslagaccount met de naam *mystorageaccount* in de resourcegroep Hallo eerder hebt gemaakt:

```azurecli
az storage account create \
    --resource-group myResourceGroup \
    --location eastus \
    --name mystorageaccount \
    --kind Storage \
    --sku Standard_LRS
```

### <a name="list-storage-account-keys"></a>Lijst met sleutels voor opslagaccount
Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert. Deze toegangstoetsen worden gebruikt bij het verifiëren van toohello storage-account, zoals de uitvoering van schrijfbewerkingen. Lees meer over [het beheren van toegang tot toostorage hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). U bekijkt hello toegangstoetsen met [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list).

Weergave Hallo toegangstoetsen voor Hallo storage-account die u hebt gemaakt:

```azurecli
az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount
```

Hallo-uitvoer is vergelijkbaar met:

```azurecli
info:    Executing command storage account keys list
+ Getting storage account keys
data:    Name  Key                                                                                       Permissions
data:    ----  ----------------------------------------------------------------------------------------  -----------
data:    key1  d4XAvZzlGAgWdvhlWfkZ9q4k9bYZkXkuPCJ15NTsQOeDeowCDAdB80r9zA/tUINApdSGQ94H9zkszYyxpe8erw==  Full
data:    key2  Ww0T7g4UyYLaBnLYcxIOTVziGAAHvU+wpwuPvK4ZG0CDFwu/mAxS/YYvAQGHocq1w7/3HcalbnfxtFdqoXOw8g==  Full
info:    storage account keys list command OK
```
Maak een notitie van **key1** terwijl u met deze toointeract met uw opslagaccount in de volgende stappen Hallo.

### <a name="create-a-storage-container"></a>Een opslagcontainer maken
In Hallo dezelfde manier waarop u verschillende mappen toologically het lokale bestandssysteem organiseren, containers in een tooorganize storage-account maken van uw schijven. Een opslagaccount kan een onbeperkt aantal containers bevatten. Maken van een container met [az storage-container maken](/cli/azure/storage/container#create).

Hallo volgende voorbeeld wordt een container met de naam *mydisks*:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

### <a name="upload-hello-vhd"></a>Hallo VHD uploaden
Nu uw aangepaste schijf met uploaden [uploaden van blob storage az](/cli/azure/storage/blob#upload). U uploaden en de aangepaste schijf opslaan als een pagina-blob.

Geef uw toegangssleutel, Hallo-container die u hebt gemaakt in de vorige stap Hallo en vervolgens Hallo pad toohello aangepaste schijf op de lokale computer:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 \
    --container-name mydisks \
    --type page \
    --file /path/to/disk/mydisk.vhd \
    --name myDisk.vhd
```
Bezig met uploaden Hallo VHD kan even duren.

### <a name="create-a-managed-disk"></a>Een beheerde schijf maken


Maak een beheerde schijf vanuit Hallo VHD met [az schijf maken](/cli/azure/disk#create). Hallo volgende voorbeeld wordt een beheerde schijf met de naam *myManagedDisk* van Hallo VHD die u hebt geüpload tooyour opslagaccount en container met de naam:

```azurecli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
  --source https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd
```
## <a name="option-2-copy-an-existing-vm"></a>Optie 2: Een bestaande virtuele machine kopiëren

U kunt ook maken Hallo aangepaste virtuele machine in Azure en vervolgens Hallo OS-schijf kopiëren en deze te koppelen tooa nieuwe VM toocreate een ander exemplaar. Dit is goed voor het testen, maar als u toouse een bestaande virtuele machine van Azure als het Hallo-model voor meerdere nieuwe virtuele machines wilt, kunt u echt maken een **installatiekopie** in plaats daarvan. Zie voor meer informatie over het maken van een installatiekopie van een bestaande virtuele machine van Azure [maken van een aangepaste installatiekopie van een virtuele machine in Azure met behulp van Hallo CLI](tutorial-custom-images.md)

### <a name="create-a-snapshot"></a>Een momentopname maken

In dit voorbeeld wordt een momentopname van een virtuele machine met de naam *myVM* in de resourcegroep *myResourceGroup* en maakt een momentopname met de naam *osDiskSnapshot*.

```azure-cli
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create \
    -g myResourceGroup \
    --source "$osDiskId" \
    --name osDiskSnapshot
```
###  <a name="create-hello-managed-disk"></a>Hallo-beheerde schijven maken

Een nieuwe beheerde schijf van Hallo momentopname maken.

Hallo-ID van de momentopname Hallo ophalen. In dit voorbeeld Hallo momentopname heet *osDiskSnapshot* en is in Hallo *myResourceGroup* resourcegroep.

```azure-cli
snapshotId=$(az snapshot show --name osDiskSnapshot --resource-group myResourceGroup --query [id] -o tsv)
```

Hallo-beheerde schijven maken. In dit voorbeeld wordt een beheerde schijf met de naam maakt *myManagedDisk* van onze momentopname die is 128 GB groot in standard-opslag.

```azure-cli
az disk create \
    --resource-group myResourceGroup \
    --name myManagedDisk \
    --sku Standard_LRS \
    --size-gb 128 \
    --source $snapshotId
```

## <a name="create-hello-vm"></a>Hallo VM maken

Maak nu uw virtuele machine met [az vm maken](/cli/azure/vm#create) en koppelt (--koppelen-os-schijf) Hallo beheerd schijf als Hallo OS-schijf. Hallo volgende voorbeeld wordt een virtuele machine met de naam *myNewVM* Hallo met beheerde-schijf gemaakt op basis van uw geüploade VHD:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNewVM \
    --os-type linux \
    --attach-os-disk myManagedDisk
```

U moet kunnen tooSSH in Hallo VM met Hallo referenties van Hallo bron-VM. 

## <a name="next-steps"></a>Volgende stappen
Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md). U kunt ook te[een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nieuwe virtuele machines. Als u toepassingen die worden uitgevoerd op uw virtuele machines dat u tooaccess nodig hebt, moet u te[openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

