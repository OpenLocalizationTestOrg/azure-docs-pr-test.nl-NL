---
title: aaaCreate en een tooAzure Linux VHD uploaden | Microsoft Docs
description: Maken en uploaden van een Azure virtuele harde schijf (VHD) die Hallo Linux-besturingssysteem met behulp van Hallo klassieke implementatiemodel bevat
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Maakt en uploadt u een virtuele harde schijf met Hallo Linux-besturingssysteem
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. U kunt ook [uploaden van een aangepaste installatiekopie met Azure Resource Manager](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Dit artikel laat zien hoe toocreate en het uploaden van een virtuele harde schijf (VHD) zodat u deze als uw eigen gebruiken kunt installatiekopie toocreate virtuele machines in Azure. Meer informatie over hoe tooprepare Hallo besturingssysteem zodat u deze, kunt u toocreate gebruiken kunt meerdere virtuele machines op basis van die installatiekopie. 


## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt Hallo volgende items:

* **Linux-besturingssysteem is geïnstalleerd in een .vhd-bestand** -u hebt geïnstalleerd een [door Azure goedgekeurde Linux-distributie](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (of Raadpleeg [informatie voor niet-goedgekeurde distributies](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa virtuele schijf in Hallo VHD-indeling. Er bestaan meerdere hulpprogramma's toocreate een virtuele machine en de VHD:
  * Installeer en configureer [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) of [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse wordt gelet op de VHD in uw installatiekopie-indeling. Indien nodig, kunt u [converteren van een installatiekopie van een](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) met `qemu-img convert`.
  * U kunt ook de Hyper-V [op Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) of [op Windows Server 2012/2012 R2](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure. Wanneer u een virtuele machine maakt, geeft u de VHD als Hallo-indeling. Indien nodig, kunt u converteren VHDX schijven tooVHD [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) of Hallo [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell-cmdlet. Bovendien wordt biedt Azure geen ondersteuning dynamische VHD's uploaden, zodat u tooconvert moet dergelijke schijven toostatic VHD's voordat u uploadt. U kunt hulpprogramma's gebruiken zoals [Azure VHD-hulpprogramma's voor Ga](https://github.com/Microsoft/azure-vhd-utils-for-go) tooconvert dynamische schijven tijdens Hallo van tooAzure uploaden.

* **Azure-opdrachtregelinterface** -meest recente installatie Hallo [Azure-opdrachtregelinterface](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload Hallo VHD.

<a id="prepimage"> </a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>Stap 1: Voorbereiden Hallo installatiekopie toobe geüpload
Azure biedt ondersteuning voor verschillende Linux-distributies (Zie [goedgekeurde distributies](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Hallo artikelen te volgen helpt u bij hoe tooprepare Hallo verschillende Linux-distributies die worden ondersteund in Azure. Nadat u de stappen in de volgende handleidingen Hallo Hallo hebt voltooid, kun je hier als u een VHD-bestand dat is gereed tooupload tooAzure hebt:

* **[Op basis van centOS distributies](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Andere - niet-goedgekeurde distributies](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Hello Azure-platform SLA van toepassing is toovirtual machines met Linux-besturingssysteem alleen als een van de Hallo distributies goedgekeurde wordt gebruikt met Hallo configuratiedetails zoals opgegeven in de ondersteunde versies' hello in [Linux op Azure-Endorsed distributies ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Alle Linux-distributies in de afbeelding voor Azure-galerie Hallo zijn aangebracht distributies met Hallo vereiste configuratie.
> 
> 

Zie ook Hallo  **[opmerkingen bij de installatie van Linux](../create-upload-generic.md#general-linux-installation-notes)**  voor meer algemene tips voor het Linux-installatiekopieën voorbereiden voor Azure.

<a id="connect"> </a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>Stap 2: Hallo verbinding tooAzure voorbereiden
Zorg ervoor dat u gebruikmaakt van hello Azure CLI in het klassieke implementatiemodel hello (`azure config mode asm`), meld u daarna tooyour account:

```azurecli
azure login
```


<a id="upload"> </a>

## <a name="step-3-upload-hello-image-tooazure"></a>Stap 3: Hallo installatiekopie tooAzure uploaden
U moet uw VHD-bestand naar een tooupload storage-account. Kunt u een bestaand opslagaccount kiezen of [Maak een nieuwe](../../../storage/common/storage-create-storage-account.md).

Hello Azure CLI tooupload Hallo installatiekopie door Hallo volgende opdracht gebruiken:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

In het vorige voorbeeld Hallo:

* **BlobStorageURL** Hallo-URL voor Hallo u van plan bent toouse storage-account
* **YourImagesFolder** Hallo-container in blob-opslag is waar u toostore uw installatiekopieën
* **VHDName** Hallo-label die wordt weergegeven in de portal tooidentify Hallo virtuele harde schijf.
* **PathToVHDFile** Hallo volledig pad en naam van Hallo .vhd-bestand op uw computer.

Hallo na de opdracht ziet u een compleet voorbeeld:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>Stap 4: Een virtuele machine uit Hallo installatiekopie maken
U maakt een virtuele machine met `azure vm create` in Hallo dezelfde manier als een gewone virtuele machine. Hebt u uw installatiekopie gegeven in de vorige stap Hallo Hallo-naam opgeven. In de Hallo voorbeeld te volgen, gebruiken we Hallo **myImage** de naam van de installatiekopie is opgegeven in de vorige stap Hallo:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate uw eigen virtuele machines, Geef uw eigen gebruikersnaam en wachtwoord, locatie, DNS-naam en installatiekopie met de naam.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie [Azure CLI-verwijzing voor hello Azure klassieke implementatiemodel](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
