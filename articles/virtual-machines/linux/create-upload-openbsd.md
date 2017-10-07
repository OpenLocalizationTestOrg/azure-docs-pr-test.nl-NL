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
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Maken en een tooAzure OpenBSD schijf installatiekopie uploaden
Dit artikel laat zien hoe Hallo besturingssysteem OpenBSD toocreate en het uploaden van een virtuele harde schijf (VHD) die bevat. Nadat u deze uploaden, kunt u deze kunt gebruiken als uw eigen toocreate installatiekopie van een virtuele machine (VM) in Azure via Azure CLI.


## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt Hallo volgende items:

* **Een Azure-abonnement** -als u geen account hebt, kunt u een in een paar minuten. Als u een MSDN-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Anders wordt informatie over hoe te[maken van een gratis proefaccount](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure CLI 2.0** -Controleer of er Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-azure-cli) geïnstalleerd en geregistreerd in tooyour Azure-account met [az aanmelding](/cli/azure/#login).
* **OpenBSD-besturingssysteem is geïnstalleerd in een .vhd-bestand** -een ondersteund besturingssysteem van OpenBSD (versie 6.1) moet geïnstalleerde tooa virtuele hardeschijf. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden. U kunt bijvoorbeeld een oplossing voor netwerkvirtualisatie gebruiken zoals Hyper-V toocreate Hallo .vhd-bestand en Hallo-besturingssysteem installeren. Voor instructies over hoe tooinstall en het gebruik van Hyper-V, Zie [Hyper-V installeren en een virtuele machine maken](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>De installatiekopie van het OpenBSD voorbereiden voor Azure
Voer op Hallo VM waar u Hallo OpenBSD besturingssysteem geïnstalleerd 6,1, Hyper-V-ondersteuning wordt toegevoegd en Hallo procedures te volgen:

1. Als DHCP niet is ingeschakeld tijdens de installatie, het Hallo-service als volgt inschakelen:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Stel een seriële console als volgt in:

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. De installatie van pakket als volgt configureren:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. Standaard Hallo `root` gebruiker is uitgeschakeld op virtuele machines in Azure. Gebruikers kunnen opdrachten uitvoeren met verhoogde bevoegdheden via Hallo `doas` opdracht op OpenBSD VM. Doas is standaard ingeschakeld. Zie voor meer informatie [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Installeren en configureren van vereisten voor hello Azure Agent als volgt:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. meest recente versie van de Hallo Hallo Azure-agent altijd vindt u op [Github](https://github.com/Azure/WALinuxAgent/releases). Hallo-agent als volgt installeren:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Nadat u Azure-Agent hebt geïnstalleerd, is het een goed idee tooverify dat deze wordt als volgt uitgevoerd:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Identiteitsgegevens Hallo system tooclean deze en maak deze geschikt is voor reprovisioning. Hallo volgende opdracht ook verwijderd Hallo laatste ingerichte gebruiker serviceaccount en Hallo die zijn gekoppeld:

    ```sh
    waagent -deprovision+user -force
    ```

U kunt nu uw virtuele machine afsluiten.


## <a name="prepare-hello-vhd"></a>Hallo VHD voorbereiden
Hallo VHDX-indeling wordt niet ondersteund in Azure, alleen **vaste VHD**. U kunt converteren Hallo schijf toofixed VHD-indeling met behulp van Hyper-V-beheer of Powershell Hallo [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet. Een voorbeeld is als volgende.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Storage-resources maken en uploaden
Maak eerst een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload uw VHD maken van een opslagaccount met [az storage-account maken](/cli/azure/storage/account#create). Namen van opslagaccounts moeten uniek zijn, zodat uw eigen naam opgeven. Hallo volgende voorbeeld wordt een opslagaccount met de naam *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol toegang tot het opslagaccount toohello, krijgen Hallo-opslagsleutel met [lijst met opslagaccounts die sleutels az](/cli/azure/storage/account/keys#list) als volgt:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

toologically afzonderlijke Hallo VHD's die u uploadt, maak een container in Hallo storage-account met [az storage-container maken](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Ten slotte uw VHD met uploaden [uploaden van blob storage az](/cli/azure/storage/blob#upload) als volgt:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Virtuele machine van de VHD maken
U kunt maken met een virtuele machine een [voorbeeldscript](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) of rechtstreeks met [az vm maken](/cli/azure/vm#create). toospecify OpenBSD VHD u hebt geüpload, gebruik Hallo Hallo `--image` parameter als volgt:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Hallo IP-adres verkrijgen voor uw VM OpenBSD met [az vm lijst-ip-adressen](/cli/azure/vm#list-ip-addresses) als volgt:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

U kunt nu SSH tooyour OpenBSD VM als normale:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Volgende stappen
Desgewenst kunt u meer informatie over Hyper-V op OpenBSD6.1 ondersteunen tooknow lezen [OpenBSD 6.1](https://www.openbsd.org/61.html) en [hyperv.4](http://man.openbsd.org/hyperv.4).

Desgewenst kunt u een virtuele machine van de beheerde schijf toocreate lezen [az schijf](/cli/azure/disk). 
