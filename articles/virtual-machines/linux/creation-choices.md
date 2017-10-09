---
title: aaaDifferent manieren toocreate een Linux VM in Azure | Microsoft Azure
description: Meer informatie over Hallo verschillende manieren toocreate virtuele Linux-machine in Azure, met inbegrip van koppelingen tootools en zelfstudies voor elke methode.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Verschillende manieren toocreate een Linux-VM
Hebt u Hallo flexibiliteit in Azure toocreate virtuele Linux-machine (VM) met behulp van hulpprogramma's en werkstromen vertrouwd tooyou. In dit artikel bevat een overzicht van deze verschillen en voorbeelden voor het maken van uw virtuele Linux-machines, met inbegrip van hello Azure CLI 2.0. U kunt ook het maken van keuzen inclusief Hallo weergeven [Azure CLI 1.0](creation-choices-nodejs.md).

Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2) is beschikbaar in verschillende platforms via een pakket npm, geleverde distro pakketten of Docker-container. Installeer de meest geschikte build Hallo voor uw omgeving en meld u aan tooan Azure-account met [az aanmelding](/cli/azure/#login)

* [Maak een Linux-VM met hello Azure CLI 2.0](quick-create-cli.md)
  
  * Maak een resourcegroep met [az group create](/cli/azure/group#create) met de naam *myResourceGroup*: 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Maak een VM met [az vm maken](/cli/azure/vm#create) met de naam *myVM* met behulp van recente Hallo *UbuntuLTS* installatiekopie en SSH-sleutels genereren als deze niet al bestaan *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Een virtuele Linux-machine maken met een Azure-sjabloon](create-ssh-secured-vm-from-template.md)
  
  * Hallo volgende voorbeeld wordt [az implementatie maken](/cli/azure/group/deployment#create) toocreate een virtuele machine uit een sjabloon die is opgeslagen op GitHub:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Een virtuele Linux-machine maken en aanpassen met cloud-init](tutorial-automate-vm-deployment.md)

* [Een maximaal beschikbare toepassing met gelijke taakverdeling maken op meerdere virtuele Linux-machines](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Azure Portal
Hallo [Azure-portal](https://portal.azure.com) kunt u tooquickly een virtuele machine maken omdat er is niets tooinstall op uw systeem. Gebruik hello Azure portal toocreate Hallo VM:

* [Maak een Linux-VM met hello Azure-portal](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Opties voor besturingssysteem en installatiekopieën
Wanneer u een virtuele machine maakt, kiest u een installatiekopie die op basis van het besturingssysteem die u wilt dat toorun Hallo. Azure en de diverse partners bieden een groot aantal installatiekopieën. Sommige hiervan bevatten toepassingen en hulpprogramma’s die vooraf zijn geïnstalleerd. Of een van uw eigen installatiekopieën uploaden (Zie [Hallo volgende sectie](#use-your-own-image)).

### <a name="azure-images"></a>Installatiekopieën van Azure
Gebruik Hallo [az vm-installatiekopie](/cli/azure/vm/image) toosee-opdrachten door de uitgever, distro release en builds beschikbaar is.

Beschikbare uitgevers vermelden:

```azurecli
az vm image list-publishers --location eastus
```

Beschikbare producten (aanbiedingen) voor een bepaalde uitgever vermelden:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Beschikbare SKU's (distributiereleases) van een bepaalde aanbieding vermelden:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Alle beschikbare installatiekopieën voor een bepaalde release vermelden:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Zie voor meer voorbeelden op Bladeren en het gebruik van de beschikbare installatiekopieën [navigeren door en selecteren van installatiekopieën van virtuele machine van Azure met Azure CLI Hallo](cli-ps-findimage.md).

Hallo [az vm maken](/cli/azure/vm#create) opdracht beschikt over aliassen kunt u tooquickly toegang Hallo veelvoorkomende distributies en hun meest recente versies. Het gebruik van aliassen is vaak sneller dan het Hallo-uitgever, aanbieding, SKU en versie geven telkens wanneer die u een virtuele machine maken:

| Alias | Uitgever | Aanbieding | SKU | Versie |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7.2 |meest recente |
| CoreOS |CoreOS |CoreOS |Stabiel |meest recente |
| Debian |credativ |Debian |8 |meest recente |
| openSUSE |SUSE |openSUSE |13.2 |meest recente |
| RHEL |RedHat |RHEL |7.2 |meest recente |
| SLES |SLES |SLES |12-SP1 |meest recente |
| UbuntuLTS |Canonical |UbuntuServer |14.04.4-LTS |meest recente |

### <a name="use-your-own-image"></a>Uw eigen installatiekopie gebruiken
Als u specifieke aanpassingen nodig hebt, kunt u een installatiekopie gebruiken op basis van een bestaande VM in Azure door de betreffende VM vast te leggen. U kunt ook een installatiekopie uploaden die u on-premises hebt gemaakt. Voor meer informatie over ondersteunde distributies en hoe toouse uw eigen installatiekopieën zien Hallo volgende artikelen:

* [Door Azure goedgekeurde distributies](endorsed-distros.md)
* [Informatie over niet-goedgekeurde distributies](create-upload-generic.md)
* [Hoe een installatiekopie van een bestaande virtuele machine van Azure toocreate](tutorial-custom-images.md).
  
  * Snel starten voorbeeld opdrachten toocreate een installatiekopie van een bestaande virtuele machine van Azure:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Volgende stappen
* Maak een Linux-VM met Hallo [CLI](quick-create-cli.md), van Hallo [portal](quick-create-portal.md), of met behulp van een [Azure Resource Manager-sjabloon](../windows/cli-deploy-templates.md).
* Lees na het maken van een virtuele Linux-machine [meer informatie over Azure-schijven en opslag](tutorial-manage-disks.md).
* Snelle stappen te[opnieuw instellen van een wachtwoord of SSH-sleutels en gebruikers beheren](using-vmaccess-extension.md).
