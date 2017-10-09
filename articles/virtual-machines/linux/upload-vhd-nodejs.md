---
title: een aangepaste installatiekopie Linux met Azure CLI 1.0 aaaUpload | Microsoft Docs
description: Maken en uploaden van een virtuele harde schijf (VHD) tooAzure met een aangepaste Linux-installatiekopie met Hallo Resource Manager-implementatiemodel en hello Azure CLI 1.0.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a8c7818f-eb65-409e-aa91-ce5ae975c564
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/10/2016
ms.author: iainfou
ms.openlocfilehash: 0bbd232debee1e632233d1c010e388dbc1548bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-and-create-a-linux-vm-from-custom-disk-image-by-using-hello-azure-cli-10"></a>Uploaden en Linux-VM maken van aangepaste installatiekopie met behulp van hello Azure CLI 1.0
Dit artikel ziet u hoe een virtuele harde schijf (VHD) tooAzure met tooupload Hallo Resource Manager-implementatiemodel en virtuele Linux-machines van deze aangepaste installatiekopie maken. Deze functionaliteit kunt u tooinstall en configureren van een Linux distro tooyour vereisten en gebruik vervolgens deze VHD tooquickly Azure virtuele machines (VM's) maken.


## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel


## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, na de sectie details Hallo Hallo baseren opdrachten tooupload een tooAzure VM. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#requirements).

Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `myimages`.

Maak eerst een resourcegroep. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUs` locatie:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

Een toohold storage-account van uw virtuele schijven maken. Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount`:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

Lijst Hallo toegangssleutels voor uw opslagaccount. Maak een notitie van `key1`:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
```

Maak een container in uw storage-account met behulp van Hallo-opslagsleutel die u hebt verkregen. Hallo volgende voorbeeld wordt een container met de naam `myimages` met Hallo opslag sleutelwaarde van `key1`:

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

Ten slotte upload uw VHD toohello-container die u hebt gemaakt. Geef Hallo lokaal pad tooyour VHD onder `/path/to/disk/mydisk.vhd`:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

U kunt nu een virtuele machine maken van de geüploade virtuele schijf [met een Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd). U kunt ook Hallo CLI door Hallo URI tooyour schijf opgeven (`--image-urn`). Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` gebruik van de virtuele schijf Hallo eerder hebt geüpload:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
```

Hallo doelopslagaccount heeft toobe Hallo dezelfde als waar u de virtuele schijf geüpload. Of u kunt ook toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo `azure vm create` opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels. U kunt meer lezen over Hallo [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

## <a name="requirements"></a>Vereisten
Hallo toocomplete volgende stappen die u nodig:

* **Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -installeren van een [door Azure goedgekeurde Linux-distributie](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in VHD Hallo de indeling. Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:
  * Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling. Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.
  * U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure. Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling. Indien nodig, kunt u converteren VHDX schijven tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet. Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt. U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.
> 
> 

* Virtuele machines die zijn gemaakt op basis van uw aangepaste installatiekopie moeten zich bevinden in Hallo hetzelfde opslagaccount als Hallo installatiekopie zelf
  * Maken van een storage-account en de container toohold uw aangepaste installatiekopie en de gemaakte virtuele machines
  * Nadat u uw virtuele machines hebt gemaakt, kunt u veilig uw installatiekopie verwijderen

Zorg ervoor dat u hebt [hello Azure CLI 1.0](../../cli-install-nodejs.md) aangemeld en het gebruik van Resource Manager-modus:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. Voorbeeld parameternamen opgenomen `myResourceGroup`, `mystorageaccount`, en `myimages`.

<a id="prepimage"> </a>

## <a name="prepare-hello-image-toobe-uploaded"></a>Hallo installatiekopie toobe geüpload voorbereiden
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


## <a name="create-a-resource-group"></a>Een resourcegroep maken
Resourcegroepen samenbrengen logisch alle hello Azure-resources toosupport uw virtuele machines, zoals Hallo virtuele netwerken en opslag. Lees meer over [Azure resourcegroepen hier](../../azure-resource-manager/resource-group-overview.md). Voordat u uw aangepaste schijfimage uploaden en het maken van virtuele machines, moet u eerst toocreate een resourcegroep. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUS` locatie:

```azurecli
azure group create myResourceGroup --location "WestUS"
```

## <a name="create-a-storage-account"></a>Een opslagaccount maken
Virtuele machines worden opgeslagen als pagina-blobs binnen een opslagaccount. Lees meer over [hier Azure blob-opslag](../../storage/common/storage-introduction.md#blob-storage). U maken een opslagaccount voor uw aangepaste schijfimage en virtuele machines. Alle virtuele machines die u maakt van uw aangepaste schijf installatiekopie moeten toobe in Hallo hetzelfde opslagaccount als installatiekopie.

Hallo volgende voorbeeld wordt een opslagaccount met de naam `mystorageaccount` in de resourcegroep Hallo eerder hebt gemaakt:

```azurecli
azure storage account create mystorageaccount --resource-group myResourceGroup \
    --location "WestUS" --kind Storage --sku-name PLRS
```

## <a name="list-storage-account-keys"></a>Lijst met sleutels voor opslagaccount
Azure twee 512-bits toegangstoetsen voor elk opslagaccount genereert. Deze toegangstoetsen worden gebruikt bij het verifiëren van toohello storage-account, zoals toocarry uit schrijfbewerkingen. Lees meer over [het beheren van toegang tot toostorage hier](../../storage/common/storage-create-storage-account.md#manage-your-storage-account). U kunt toegangstoetsen Hello weergeven `azure storage account keys list` opdracht.

Weergave Hallo toegangstoetsen voor Hallo storage-account die u hebt gemaakt:

```azurecli
azure storage account keys list mystorageaccount --resource-group myResourceGroup
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
In Hallo indelen dezelfde manier waarop u verschillende mappen toologically het lokale bestandssysteem, maakt u containers in een storage account tooorganize uw virtuele schijven en afbeeldingen. Een opslagaccount kan een onbeperkt aantal containers bevatten. 

Hallo volgende voorbeeld wordt een container met de naam `myimages`, in de vorige stap Hallo Hallo toegangssleutel geven verkregen (`key1`):

```azurecli
azure storage container create --account-name mystorageaccount \
    --account-key key1 --container myimages
```

## <a name="upload-vhd"></a>Virtuele harde schijf geüpload
Nu kunt u uw aangepaste schijfimage daadwerkelijk uploaden. Als met alle virtuele schijven die door virtuele machines, gebruikt u uploaden en uw aangepaste schijfimage opslaan als een pagina-blob.

Geef uw toegangssleutel, Hallo-container die u hebt gemaakt in de vorige stap Hallo en vervolgens Hallo pad toohello aangepaste schijfimage op uw lokale computer:

```azurecli
azure storage blob upload --blobtype page --account-name mystorageaccount \
    --account-key key1 --container myimages /path/to/disk/mydisk.vhd
```

## <a name="create-vm-from-custom-image"></a>Virtuele machine van de aangepaste installatiekopie maken
Wanneer u virtuele machines van de installatiekopie van uw aangepaste schijf maakt, geef Hallo URI toohello schijfimage. Zorg ervoor dat Hallo bestemming storage-account komt overeen met waar de installatiekopie van uw aangepaste schijf wordt opgeslagen. U kunt uw virtuele machine met behulp van hello Azure CLI of Resource Manager JSON-sjabloon maken.

### <a name="create-a-vm-using-hello-azure-cli"></a>Een virtuele machine maken met hello Azure CLI
Geef van Hallo `--image-urn` parameter Hello `azure vm create` opdracht toopoint tooyour aangepaste schijfimage. Zorg ervoor dat `--storage-account-name` komt overeen met Hallo opslagaccount waarin de installatiekopie van uw aangepaste schijf wordt opgeslagen. U beschikt niet over toouse Hallo dezelfde container als aangepaste schijf installatiekopie toostore Hallo uw virtuele machines. Zorg ervoor dat toocreate andere containers in Hallo dezelfde manier als Hallo eerdere stappen voordat u uw aangepaste schijfkopieën uploadt.

Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` van uw aangepaste schijfimage:

```azurecli
azure vm create myVM -l "WestUS" --resource-group myResourceGroup \
    --image-urn https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd
    --storage-account-name mystorageaccount
```

Of u kunt nog steeds toospecify, wordt u gevraagd om te beantwoorden, alle extra parameters die zijn vereist voor Hallo Hallo `azure vm create` opdracht zoals virtueel netwerk, openbare IP-adres, gebruikersnaam en een SSH-sleutels. Lees meer over Hallo [beschikbare parameters van de CLI Resource Manager](../azure-cli-arm-commands.md#azure-vm-commands-to-manage-your-azure-virtual-machines).

### <a name="create-a-vm-using-a-json-template"></a>Een virtuele machine met een JSON-sjabloon maken
Azure Resource Manager-sjablonen zijn JSON JavaScript Object Notation ()-bestanden die u wenst dat toobuild Hallo-omgeving definiëren. Hallo-sjablonen zijn onderverdeeld in de resourceproviders toodifferent zoals compute of een netwerk. U kunt bestaande sjablonen gebruiken of uw eigen schrijven. Lees meer over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md).

Binnen Hallo `Microsoft.Compute/virtualMachines` provider van de sjabloon die u hebt een `storageProfile` knooppunt met Hallo configuratiedetails voor uw virtuele machine. Hallo twee belangrijkste parameters tooedit zijn Hallo `image` en `vhd` URI's die verwijzen tooyour aangepaste installatiekopie en de virtuele schijf van de nieuwe VM. Hallo hieronder toont een voorbeeld van Hallo JSON voor het gebruik van een aangepaste installatiekopie:

```json
"storageProfile": {
          "osDisk": {
            "name": "myVM",
            "osType": "Linux",
            "caching": "ReadWrite",
            "createOption": "FromImage",
            "image": {
              "uri": "https://mystorageaccount.blob.core.windows.net/myimages/mydisk.vhd"
            },
            "vhd": {
              "uri": "https://mystorageaccount.blob.core.windows.net/vhds/newvmname.vhd"
            }
          }
```

U kunt [deze bestaande sjabloon toocreate een virtuele machine van een aangepaste installatiekopie](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) of lezen over [maken van uw eigen Azure Resource Manager-sjablonen](../../azure-resource-manager/resource-group-authoring-templates.md). 

Zodra u een sjabloon die is geconfigureerd hebt, hebt u uw virtuele machines met behulp van Hallo `azure group deployment create` opdracht. Hallo-URI van de JSON-sjabloon opgeven met Hallo `--template-uri` parameter:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-uri https://uri.to.template/mytemplate.json
```

Als u een JSON-bestand die lokaal zijn opgeslagen op uw computer hebt, kunt u Hallo `--template-file` parameter in plaats daarvan:

```azurecli
azure group deployment create --resource-group myResourceGroup
    --template-file /path/to/mytemplate.json
```


## <a name="next-steps"></a>Volgende stappen
Nadat u hebt voorbereid en uw aangepaste virtuele schijf wordt geüpload, kunt u meer lezen over [met Resource Manager en sjablonen](../../azure-resource-manager/resource-group-overview.md). U kunt ook te[een gegevensschijf toevoegen](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooyour nieuwe virtuele machines. Als u toepassingen die worden uitgevoerd op uw virtuele machines dat u tooaccess nodig hebt, moet u te[openen van poorten en eindpunten](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

