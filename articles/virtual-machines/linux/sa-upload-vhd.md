---
title: een aangepaste Linux-schijf met Azure CLI 2.0 aaaUpload | Microsoft Docs
description: Maken en uploaden van een virtuele harde schijf (VHD) tooAzure met Hallo Resource Manager-implementatiemodel en hello Azure CLI 2.0
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
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: cf8556ab4dfe6c4e5eff4e99fe1ddc44393f774c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-with-hello-azure-cli-20"></a>Uploaden en Linux-VM te maken van aangepaste schijf Hello Azure CLI 2.0
In dit artikel leest u hoe tooupload een virtuele harde schijf (VHD) tooan Azure storage-account met hello Azure CLI 2.0 en virtuele Linux-machines te maken van deze aangepaste schijf. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](upload-vhd-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Deze functionaliteit kunt u tooinstall en configureren van een Linux distro tooyour vereisten en gebruik vervolgens deze VHD tooquickly Azure virtuele machines (VM's) maken.

In dit onderwerp maakt gebruik van storage-accounts voor hello laatste VHD's, maar u kunt ook doen met behulp van deze stappen [schijven die worden beheerd](upload-vhd.md). 

## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, na de sectie details Hallo Hallo baseren opdrachten tooupload een tooAzure VHD. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#requirements).

Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `mydisks`.

Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUs` locatie:

```azurecli
az group create --name myResourceGroup --location westus
```

Uw virtuele schijven met een toohold storage-account maken [az storage-account maken](/cli/azure/storage/account#create). Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

Hallo toegangssleutels voor uw opslagaccount met lijst [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list). Maak een notitie van `key1`:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
```

Maken van een container in uw storage-account met behulp van de opslagsleutel Hallo u hebt verkregen met [az storage-container maken](/cli/azure/storage/container#create). Hallo volgende voorbeeld wordt een container met de naam `mydisks` met Hallo opslag sleutelwaarde van `key1`:

```azurecli
az storage container create --account-name mystorageaccount \
    --account-key key1 --name mydisks
```

Ten slotte uploaden uw VHD toohello-container die u hebt gemaakt met [uploaden van blob storage az](/cli/azure/storage/blob#upload). Geef Hallo lokaal pad tooyour VHD onder `/path/to/disk/mydisk.vhd`:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

Geef Hallo URI tooyour schijf (`--image`) met [az vm maken](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` gebruik van de virtuele schijf Hallo eerder hebt geüpload:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisk/myDisks.vhd \
    --use-unmanaged-disk
```

Hallo doelopslagaccount heeft toobe Hallo dezelfde als waar u de virtuele schijf geüpload. Of u kunt ook toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo **az vm maken** opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels. U kunt meer lezen over Hallo [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Vereisten
Hallo toocomplete volgende stappen die u nodig:

* **Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -installeren van een [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in VHD Hallo de indeling. Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:
  * Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling. Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.
  * U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure. Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling. Indien nodig, kunt u converteren VHDX schijven tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet. Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt. U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.
> 
> 

* Virtuele machines die zijn gemaakt op basis van uw aangepaste schijf moeten zich bevinden in Hallo hetzelfde opslagaccount als Hallo schijf zelf
  * Maken van een storage-account en de container toohold uw aangepaste schijf en de gemaakte virtuele machines
  * Nadat u uw virtuele machines hebt gemaakt, kunt u veilig de schijf verwijderen

Zorg ervoor dat er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `mydisks`.

<a id="prepimage"> </a>

## <a name="prepare-hello-disk-toobe-uploaded"></a>Hallo schijf toobe geüpload voorbereiden
Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund op Azure:

* **[Op basis van centOS distributies](create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Andere - niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

Zie ook Hallo  **[opmerkingen bij de installatie van Linux](create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.

> [!NOTE]
> Hallo [Azure-platform SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/) is van toepassing tooVMs met Linux alleen met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' wanneer een van de Hallo goedgekeurde distributies wordt gebruikt in [Linux op door Azure goedgekeurde Distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

## <a name="create-a-resource-group"></a>Een resourcegroep maken
Resourcegroepen samenbrengen logisch alle hello Azure-resources toosupport uw virtuele machines, zoals Hallo virtuele netwerken en opslag. Zie voor meer informatie resourcegroepen [resourcegroepen overzicht](../../azure-resource-manager/resource-group-overview.md). Voordat het uploaden van uw aangepaste schijf en het maken van virtuele machines, moet u eerst toocreate een resourcegroep met [az groep maken](/cli/azure/group#create).

Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-a-storage-account"></a>Een opslagaccount maken

Maken van een opslagaccount voor uw aangepaste schijf en virtuele machines met [az storage-account maken](/cli/azure/storage/account#create). Geen VM's met niet-beheerde schijven die u maakt van uw aangepaste schijf nodig toobe in Hallo hetzelfde opslagaccount als die schijf. 

Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount` in de resourcegroep Hallo eerder hebt gemaakt:

```azurecli
az storage account create --resource-group myResourceGroup --location westus \
  --name mystorageaccount --kind Storage --sku Standard_LRS
```

## <a name="list-storage-account-keys"></a>Lijst met sleutels voor opslagaccount
Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert. Deze toegangstoetsen worden gebruikt bij het verifiëren van toohello storage-account, zoals toocarry uit schrijfbewerkingen. Lees meer over [het beheren van toegang tot toostorage hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). U bekijkt hello toegangstoetsen met [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list).

Weergave Hallo toegangstoetsen voor Hallo storage-account die u hebt gemaakt:

```azurecli
az storage account keys list --resource-group myResourceGroup --account-name mystorageaccount
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
Maak een notitie van `key1` terwijl u met deze toointeract met uw opslagaccount in de volgende stappen Hallo.

## <a name="create-a-storage-container"></a>Een opslagcontainer maken
In Hallo dezelfde manier waarop u verschillende mappen toologically het lokale bestandssysteem organiseren, containers in een tooorganize storage-account maken van uw schijven. Een opslagaccount kan een onbeperkt aantal containers bevatten. Maken van een container met [az storage-container maken](/cli/azure/storage/container#create).

Hallo volgende voorbeeld wordt een container met de naam `mydisks`:

```azurecli
az storage container create \
    --account-name mystorageaccount \
    --name mydisks
```

## <a name="upload-vhd"></a>Virtuele harde schijf geüpload
Nu uw aangepaste schijf met uploaden [uploaden van blob storage az](/cli/azure/storage/blob#upload). U uploaden en de aangepaste schijf opslaan als een pagina-blob.

Geef uw toegangssleutel, Hallo-container die u hebt gemaakt in de vorige stap Hallo en vervolgens Hallo pad toohello aangepaste schijf op de lokale computer:

```azurecli
az storage blob upload --account-name mystorageaccount \
    --account-key key1 --container-name mydisks --type page \
    --file /path/to/disk/mydisk.vhd --name myDisk.vhd
```

## <a name="create-hello-vm"></a>Hallo VM maken
een virtuele machine met niet-beheerde schijven toocreate Hallo URI tooyour schijf opgeven (`--image`) met [az vm maken](/cli/azure/vm#create). Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` gebruik van de virtuele schijf Hallo eerder hebt geüpload:

Geef van Hallo `--image` parameter met [az vm maken](/cli/azure/vm#create) toopoint tooyour aangepaste schijf. Zorg ervoor dat `--storage-account` komt overeen met Hallo opslagaccount waarin de aangepaste schijf wordt opgeslagen. U beschikt niet over toouse Hallo dezelfde container als aangepaste schijf toostore Hallo uw virtuele machines. Zorg ervoor dat toocreate andere containers in Hallo dezelfde manier als Hallo eerdere stappen voordat u de aangepaste schijf uploadt.

Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` van uw aangepaste schijf:

```azurecli
az vm create --resource-group myResourceGroup --location westus \
    --name myVM --storage-account mystorageaccount --os-type linux \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --image https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd \
    --use-unmanaged-disk
```

Of u kunt nog steeds toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo **az vm maken** opdracht zoals gebruikersnaam en het SSH-sleutels.


## <a name="resource-manager-template"></a>Resource Manager-sjabloon
Azure Resource Manager-sjablonen zijn JSON JavaScript Object Notation ()-bestanden die u wenst dat toobuild Hallo-omgeving definiëren. Hallo-sjablonen zijn onderverdeeld in de resourceproviders toodifferent zoals compute of een netwerk. U kunt bestaande sjablonen gebruiken of uw eigen schrijven. Lees meer over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).

Binnen Hallo `Microsoft.Compute/virtualMachines` provider van de sjabloon die u hebt een `storageProfile` knooppunt met Hallo configuratiedetails voor uw virtuele machine. Hallo twee belangrijkste parameters tooedit zijn Hallo `image` en `vhd` URI's die verwijzen tooyour aangepaste en uw nieuwe VM virtuele schijf. Hallo hieronder toont een voorbeeld van Hallo JSON voor het gebruik van een aangepaste schijf:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/mydisks/myDisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

U kunt [deze bestaande sjabloon toocreate een virtuele machine van een aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) of lezen over [maken van uw eigen Azure Resource Manager-sjablonen](../../azure-resource-manager/resource-group-authoring-templates.md). 

Zodra u een sjabloon die is geconfigureerd hebt, gebruikt u [az implementatie maken](/cli/azure/group/deployment#create) toocreate uw virtuele machines. Hallo-URI van de JSON-sjabloon opgeven met Hallo `--template-uri` parameter:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-uri https://uri.to.template/mytemplate.json
```

Als u een JSON-bestand die lokaal zijn opgeslagen op uw computer hebt, kunt u Hallo `--template-file` parameter in plaats daarvan:

```azurecli
az group deployment create --resource-group myNewResourceGroup \
  --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Volgende stappen
Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md). U kunt ook te[een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nieuwe virtuele machines. Als u toepassingen die worden uitgevoerd op uw virtuele machines dat u tooaccess nodig hebt, moet u te[openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

