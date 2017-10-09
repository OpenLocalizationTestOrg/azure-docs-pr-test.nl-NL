---
title: "aaaSelect Linux VM-installatiekopieën Hello Azure CLI | Microsoft Docs"
description: "Meer informatie over hoe toouse hello Azure CLI toodetermine Hallo uitgever, aanbieding, SKU en versie voor Marketplace-VM-installatiekopieën."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7a858e38-4f17-4e8e-a28a-c7f801101721
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/24/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b115b8654bc156b5bfadba53a6b002a105acb68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a>Hoe toofind Linux VM-installatiekopieën in Azure Marketplace Hallo Hello Azure CLI
Dit onderwerp wordt beschreven hoe toouse hello Azure CLI 2.0 toofind VM-installatiekopieën in hello Azure Marketplace. Gebruik deze informatie toospecify een Marketplace-installatiekopie bij het maken van een Linux-VM.

Zorg ervoor dat u de Hallo meest recente geïnstalleerd [Azure CLI 2.0](/cli/azure/install-az-cli2) en worden vastgelegd in tooan Azure-account (`az login`).

## <a name="terminology"></a>Terminologie

Marketplace-installatiekopieën worden aangeduid in Hallo CLI en andere Azure-hulpprogramma's op basis van tooa hiërarchie:

* **Publisher** -Hallo organisatie die Hallo-installatiekopie heeft gemaakt. Voorbeeld: canonieke
* **Bieden** -een groep verwante afbeeldingen die zijn gemaakt door een uitgever. Voorbeeld: Ubuntu Server
* **SKU** : een exemplaar van een aanbieding, zoals een grote release van een distributiepunt. Voorbeeld: 16.04-TNS
* **Versie** -Hallo versienummer van een installatiekopie van het SKU. Wanneer u de installatiekopie van het Hallo opgeeft, kunt u Hallo versienummer met 'nieuwste' vervangen die Hallo meest recente versie van Hallo-distributiepunt selecteert.

toospecify een Marketplace-installatiekopie, doorgaans gebruikt u de installatiekopie van het Hallo *URN*. Hallo URN combineert deze waarden, gescheiden door een dubbele punt (:)-teken Hallo: *Publisher*:*bieden*:*Sku*:*versie*. 


## <a name="list-popular-images"></a>Lijst met populaire installatiekopieën

Hallo uitvoeren [az vm afbeeldingenlijst](/cli/azure/vm/image#list) opdracht zonder Hallo `--all` optie, toosee installatiekopieën van een lijst met populaire VM in hello Azure Marketplace. Bijvoorbeeld uitvoeren Hallo opdracht toodisplay na een in cache opgeslagen lijst van populaire afbeeldingen in tabelindeling:

```azurecli
az vm image list --output table
```

Hallo uitvoer bevat Hallo URN (waarde in Hallo Hallo *Urn* kolom), waardoor u toospecify Hallo installatiekopie gebruiken. Wanneer u een virtuele machine maakt met een van deze populaire Marketplace-installatiekopieën, kunt u ook opgeven Hallo URN alias, zoals *UbuntuLTS*.

```
You are viewing an offline list of images, use --all tooretrieve an up-to-date list
Offer          Publisher               Sku                 Urn                                                             UrnAlias             Version
-------------  ----------------------  ------------------  --------------------------------------------------------------  -------------------  ---------
CentOS         OpenLogic               7.3                 OpenLogic:CentOS:7.3:latest                                     CentOS               latest
CoreOS         CoreOS                  Stable              CoreOS:CoreOS:Stable:latest                                     CoreOS               latest
Debian         credativ                8                   credativ:Debian:8:latest                                        Debian               latest
openSUSE-Leap  SUSE                    42.2                SUSE:openSUSE-Leap:42.2:latest                                  openSUSE-Leap        latest
RHEL           RedHat                  7.3                 RedHat:RHEL:7.3:latest                                          RHEL                 latest
SLES           SUSE                    12-SP2              SUSE:SLES:12-SP2:latest                                         SLES                 latest
UbuntuServer   Canonical               16.04-LTS           Canonical:UbuntuServer:16.04-LTS:latest                         UbuntuLTS            latest
...
```

## <a name="find-specific-images"></a>Specifieke installatiekopieën zoeken

een specifieke VM-installatiekopie in Marketplace, Hallo toofind gebruiken Hallo `az vm image list` opdracht Hello `--all` optie. Deze versie van de opdracht Hallo neemt enige tijd toocomplete en kunnen langdurige uitvoer geretourneerd zodat u meestal Hallo lijst filteren op `--publisher` of een andere parameter. 

Hallo volgende opdracht geeft bijvoorbeeld alle Debian-aanbiedingen (Vergeet niet dat zonder Hallo `--all` overschakelen, zoekt alleen lokale cache Hallo van algemene installatiekopieën):

```azurecli
az vm image list --offer Debian --all --output table 

```

Gedeeltelijke uitvoer: 
```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  --------------
Debian   credativ     7                  credativ:Debian:7:7.0.201602010                  7.0.201602010
Debian   credativ     7                  credativ:Debian:7:7.0.201603020                  7.0.201603020
Debian   credativ     7                  credativ:Debian:7:7.0.201604050                  7.0.201604050
Debian   credativ     7                  credativ:Debian:7:7.0.201604200                  7.0.201604200
Debian   credativ     7                  credativ:Debian:7:7.0.201606280                  7.0.201606280
Debian   credativ     7                  credativ:Debian:7:7.0.201609120                  7.0.201609120
Debian   credativ     7                  credativ:Debian:7:7.0.201611020                  7.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
Debian   credativ     8                  credativ:Debian:8:8.0.201708040                  8.0.201708040
...
```

Toepassen van vergelijkbare filters Hello `--location`, `--publisher`, en `--sku` opties. U kunt zelfs gedeeltelijke overeenkomsten uitvoeren op een filter, zoals het zoeken naar `--offer Deb` toofind alle Debian installatiekopieën.

Als u niet een bepaalde locatie met de Hallo opgeeft `--location` optie, Hallo waarden voor `westus` standaard worden geretourneerd. (Een andere standaardlocatie ingesteld door `az configure --defaults location=<location>`.)

Bijvoorbeeld, Hallo volgende opdracht geeft een lijst van alle Debian 8 SKU's in `westeurope`:

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

Gedeeltelijke uitvoer:

```
Offer    Publisher    Sku                Urn                                              Version
-------  -----------  -----------------  -----------------------------------------------  -------------
Debian   credativ     8                  credativ:Debian:8:8.0.201602010                  8.0.201602010
Debian   credativ     8                  credativ:Debian:8:8.0.201603020                  8.0.201603020
Debian   credativ     8                  credativ:Debian:8:8.0.201604050                  8.0.201604050
Debian   credativ     8                  credativ:Debian:8:8.0.201604200                  8.0.201604200
Debian   credativ     8                  credativ:Debian:8:8.0.201606280                  8.0.201606280
Debian   credativ     8                  credativ:Debian:8:8.0.201609120                  8.0.201609120
Debian   credativ     8                  credativ:Debian:8:8.0.201611020                  8.0.201611020
Debian   credativ     8                  credativ:Debian:8:8.0.201701180                  8.0.201701180
Debian   credativ     8                  credativ:Debian:8:8.0.201703150                  8.0.201703150
Debian   credativ     8                  credativ:Debian:8:8.0.201704110                  8.0.201704110
Debian   credativ     8                  credativ:Debian:8:8.0.201704180                  8.0.201704180
Debian   credativ     8                  credativ:Debian:8:8.0.201706190                  8.0.201706190
Debian   credativ     8                  credativ:Debian:8:8.0.201706210                  8.0.201706210
...
```

## <a name="navigate-hello-images"></a>Navigeer Hallo installatiekopieën 
Een andere manier toofind een installatiekopie op een locatie wordt toorun hello [az vm image lijst-uitgevers](/cli/azure/vm/image#list-publishers), [az vm image lijst-aanbiedingen](/cli/azure/vm/image#list-offers), en [az vm image lijst-SKU's](/cli/azure/vm/image#list-skus) opdrachten in de reeks. Met deze opdrachten moet u deze waarden bepalen:

1. Lijst Hallo installatiekopie uitgevers.
2. Geef de aanbiedingen voor een bepaalde uitgever weer.
3. Geef de SKU's voor een bepaalde aanbieding weer.


Bijvoorbeeld: hello volgende opdracht worden Hallo installatiekopie uitgevers in Hallo VS-West locatie:

```azurecli
az vm image list-publishers --location westus --output table
```

Gedeeltelijke uitvoer:

```
Location    Name
----------  ----------------------------------------------------
westus      1e
westus      4psa
westus      7isolutions
westus      a10networks
westus      abiquo
westus      accellion
westus      Acronis
westus      Acronis.Backup
westus      actian_matrix
westus      actifio
westus      activeeon
westus      adatao
...
```
Gebruik die deze informatie toofind van een bepaalde uitgever biedt. Bijvoorbeeld, als Canonical een installatiekopie-uitgever in Hallo locatie VS-West is, hun aanbiedingen vinden door te voeren `azure vm image list-offers`. Hallo locatie en uitgever zoals in het volgende voorbeeld Hallo Hallo doorgeven:

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

Uitvoer:

```
Location    Name
----------  -------------------------
westus      Ubuntu15.04Snappy
westus      Ubuntu15.04SnappyDocker
westus      UbunturollingSnappy
westus      UbuntuServer
westus      Ubuntu_Core
westus      Ubuntu_Snappy_Core
westus      Ubuntu_Snappy_Core_Docker
```
U ziet dat de Canonical in de regio VS-West Hallo Hallo publiceert **UbuntuServer** bieden op Azure. Maar wat SKU's? tooget uitvoeren van deze waarden `azure vm image list-skus` en stel Hallo locatie, de uitgever en de aanbieding die u gedetecteerd:

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

Uitvoer:

```
Location    Name
----------  -----------------
westus      12.04.3-LTS
westus      12.04.4-LTS
westus      12.04.5-DAILY-LTS
westus      12.04.5-LTS
westus      12.10
westus      14.04.0-LTS
westus      14.04.1-LTS
westus      14.04.2-LTS
westus      14.04.3-LTS
westus      14.04.4-LTS
westus      14.04.5-DAILY-LTS
westus      14.04.5-LTS
westus      16.04-beta
westus      16.04-DAILY-LTS
westus      16.04-LTS
westus      16.04.0-LTS
westus      16.10
westus      16.10-DAILY
westus      17.04
westus      17.04-DAILY
westus      17.10-DAILY
```

Gebruik tot slot Hallo `az vm image list` opdracht toofind een specifieke versie van Hallo SKU die u bijvoorbeeld wilt **16.04 LTS**:

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

Uitvoer:

```
Offer         Publisher    Sku        Urn                                               Version
------------  -----------  ---------  ------------------------------------------------  ---------------
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611220  16.04.201611220
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201611300  16.04.201611300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612050  16.04.201612050
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612140  16.04.201612140
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201612210  16.04.201612210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201701130  16.04.201701130
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702020  16.04.201702020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702200  16.04.201702200
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702210  16.04.201702210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201702240  16.04.201702240
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703020  16.04.201703020
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703030  16.04.201703030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703070  16.04.201703070
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703270  16.04.201703270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703280  16.04.201703280
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201703300  16.04.201703300
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705080  16.04.201705080
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201705160  16.04.201705160
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706100  16.04.201706100
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201706191  16.04.201706191
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707210  16.04.201707210
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201707270  16.04.201707270
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708030  16.04.201708030
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708110  16.04.201708110
UbuntuServer  Canonical    16.04-LTS  Canonical:UbuntuServer:16.04-LTS:16.04.201708151  16.04.201708151
```
## <a name="next-steps"></a>Volgende stappen
Nu kunt u precies Hallo installatiekopie u toouse door duurt Opmerking Hallo URN waarde. Deze waarde Hello doorgeven `--image` parameter wanneer u een virtuele machine met de Hallo maakt [az vm maken](/cli/azure/vm#create) opdracht. Houd er rekening mee dat u eventueel Hallo-versienummer in Hallo URN door 'nieuwste vervangen kunt'. Deze versie is altijd de nieuwste versie Hallo Hallo-verdeling. toocreate een virtuele machine snel met behulp van Hallo URN informatie, Zie [maken en beheren van virtuele Linux-machines Hello Azure CLI](tutorial-manage-vm.md).
