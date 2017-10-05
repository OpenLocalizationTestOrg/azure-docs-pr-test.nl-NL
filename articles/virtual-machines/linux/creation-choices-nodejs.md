---
title: Verschillende manieren om te maken van een Linux-VM met Azure CLI 1.0 | Microsoft Docs
description: Informatie over de verschillende manieren om een virtuele Linux-machine te maken op Azure, waaronder koppelingen naar hulpprogramma's en zelfstudies voor elke methode.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 1eb90d44797d66f3e09811918ce5a7f4ad4287c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="different-ways-to-create-a-linux-virtual-machine-in-azure"></a>Verschillende manieren om een virtuele Linux-machine te maken in Azure
In Azure hebt u de flexibiliteit om een virtuele Linux-machine te maken met behulp van hulpprogramma's en werkstromen die u prettig vindt. Dit artikel bevat een overzicht van de verschillen en voorbeelden voor het maken van de Linux-VM's.

## <a name="azure-cli"></a>Azure CLI
Met een van de volgende CLI-versies kunt u virtuele machines maken in Azure:

- Azure CLI 1.0: onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel (dit artikel)
- [Azure CLI 2.0](../windows/creation-choices.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel

De Azure CLI 1.0 is op diverse platforms beschikbaar via een npm-pakket, door distributeurs geleverde pakketten of Docker-container. Meer informatie over het [installeren en configureren van de Azure CLI](../../cli-install-nodejs.md). In de volgende zelfstudies vindt u voorbeelden van het gebruik van de Azure CLI 1.0. Lees elk artikel voor meer informatie over de vermelde Quick Start-opdrachten voor CLI:

* [Een virtuele Linux-machine maken via Azure CLI voor ontwikkeling en tests](quick-create-cli-nodejs.md)
  
  * Het volgende voorbeeld wordt een CoreOS VM die gebruikmaakt van een openbare sleutel met de naam *azure_id_rsa.pub*:
    
    ```azurecli
    azure vm quick-create -ssh-publickey-file ~/.ssh/azure_id_rsa.pub \
      --image-urn CoreOS
    ```
* [Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon](create-ssh-secured-vm-from-template.md)
  
  * In het volgende voorbeeld wordt een VM gemaakt met behulp van een op GitHub opgeslagen sjabloon:
    
    ```azurecli
    azure group create --name myResourceGroup --location eastus 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
    ```
* [Een volledige Linux-omgeving maken met de Azure-CLI](create-cli-complete-nodejs.md)
  
  * Omvat het maken van een load balancer en meerdere VM’s in een beschikbaarheidsset.
* [Een schijf toevoegen aan een virtuele Linux-machine](add-disk.md)
  
  * Het volgende voorbeeld wordt een *5* Gb schijf naar een bestaande virtuele machine met de naam *myVM*:
    
    ```azurecli
    azure vm disk attach-new \
        --resource-group myResourceGroup \
        --vm-name myVM \
        --size-in-GB 5
    ```

## <a name="azure-portal"></a>Azure Portal
In [Azure Portal](https://portal.azure.com) kunt u snel een VM maken omdat u niets hoeft te installeren op uw systeem. Azure Portal gebruiken om een virtuele machine te maken:

* [Een virtuele Linux-machine maken met behulp van Azure Portal](quick-create-portal.md) 

## <a name="operating-system-and-image-choices"></a>Opties voor besturingssysteem en installatiekopieën
Bij het maken van een virtuele machine kiest u een installatiekopie op basis van het besturingssysteem dat u wilt uitvoeren. Azure en de diverse partners bieden een groot aantal installatiekopieën. Sommige hiervan bevatten toepassingen en hulpprogramma’s die vooraf zijn geïnstalleerd. U kunt ook een van uw eigen installatiekopieën uploaden (zie [het volgende gedeelte](#use-your-own-image)).

### <a name="azure-images"></a>Installatiekopieën van Azure
Gebruik de CLI-opdrachten van `azure vm image` om te zien wat er beschikbaar is per uitgever, distributierelease en build.

Vermeld beschikbare uitgevers als volgt:

```azurecli
azure vm image list-publishers --location eastus
```

Vermeld beschikbare producten (aanbiedingen) voor een bepaalde uitgever als volgt:

```azurecli
azure vm image list-offers --location eastus --publisher Canonical
```

Vermeld beschikbare SKU's (distributiereleases) van een bepaalde aanbieding als volgt:

```azurecli
azure vm image list-skus --location eastus --publisher Canonical --offer UbuntuServer
```

Vermeld alle beschikbare installatiekopieën voor een bepaalde release als volgt:

```azurecli
azure vm image list --location eastus --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS
```

De opdrachten `azure vm quick-create` en `azure vm create` hebben aliassen waarmee u snel toegang kunt krijgen tot de meest voorkomende distributies en hun meest recente versies. Het is gemakkelijker aliassen te gebruiken dan steeds weer de uitgever, aanbieding, SKU en versie op te geven wanneer u een VM maakt:

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
Als u specifieke aanpassingen nodig hebt, kunt u een installatiekopie gebruiken op basis van een bestaande VM in Azure door de betreffende VM *vast te leggen*. U kunt ook een installatiekopie uploaden die u on-premises hebt gemaakt. Raadpleeg de volgende artikelen voor meer informatie over ondersteunde distributies en over hoe u uw eigen installatiekopieën kunt gebruiken:

* [Door Azure goedgekeurde distributies](endorsed-distros.md)
* [Informatie over niet-goedgekeurde distributies](create-upload-generic.md)
* [Een virtuele Linux-machine uploaden en maken op basis van een aangepaste installatiekopie](upload-vhd.md)
* [Een virtuele Linux-machine vastleggen als Resource Manager-sjabloon](capture-image.md).
  
  * Voorbeelden van snelstartopdrachten voor het vastleggen van een bestaande VM:
    
    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --vm-name myVM
    azure vm generalize --resource-group myResourceGroup --vm-name myVM
    azure vm capture --resource-group myResourceGroup --vm-name myVM --vhd-name-prefix myCapturedVM
    ```

## <a name="next-steps"></a>Volgende stappen
* Maak een virtuele Linux-machine via de [portal](quick-create-portal.md), met de [CLI](quick-create-cli.md) of met behulp van een Azure Resource Manager-[sjabloon](../windows/cli-deploy-templates.md).
* Nadat u een Linux-VM hebt gemaakt, [voegt u een gegevensschijf toe](add-disk.md).
* Snelle stappen om [een wachtwoord of SSH-sleutels opnieuw in te stellen en gebruikers te beheren](using-vmaccess-extension.md)

