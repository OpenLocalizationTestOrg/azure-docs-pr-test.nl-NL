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
# <a name="how-toofind-linux-vm-images-in-hello-azure-marketplace-with-hello-azure-cli"></a><span data-ttu-id="e2efb-103">Hoe toofind Linux VM-installatiekopieën in Azure Marketplace Hallo Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2efb-103">How toofind Linux VM images in hello Azure Marketplace with hello Azure CLI</span></span>
<span data-ttu-id="e2efb-104">Dit onderwerp wordt beschreven hoe toouse hello Azure CLI 2.0 toofind VM-installatiekopieën in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e2efb-104">This topic describes how toouse hello Azure CLI 2.0 toofind VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="e2efb-105">Gebruik deze informatie toospecify een Marketplace-installatiekopie bij het maken van een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="e2efb-105">Use this information toospecify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="e2efb-106">Zorg ervoor dat u de Hallo meest recente geïnstalleerd [Azure CLI 2.0](/cli/azure/install-az-cli2) en worden vastgelegd in tooan Azure-account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="e2efb-106">Make sure that you installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in tooan Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="e2efb-107">Terminologie</span><span class="sxs-lookup"><span data-stu-id="e2efb-107">Terminology</span></span>

<span data-ttu-id="e2efb-108">Marketplace-installatiekopieën worden aangeduid in Hallo CLI en andere Azure-hulpprogramma's op basis van tooa hiërarchie:</span><span class="sxs-lookup"><span data-stu-id="e2efb-108">Marketplace images are identified in hello CLI and other Azure tools according tooa hierarchy:</span></span>

* <span data-ttu-id="e2efb-109">**Publisher** -Hallo organisatie die Hallo-installatiekopie heeft gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2efb-109">**Publisher** - hello organization that created hello image.</span></span> <span data-ttu-id="e2efb-110">Voorbeeld: canonieke</span><span class="sxs-lookup"><span data-stu-id="e2efb-110">Example: Canonical</span></span>
* <span data-ttu-id="e2efb-111">**Bieden** -een groep verwante afbeeldingen die zijn gemaakt door een uitgever.</span><span class="sxs-lookup"><span data-stu-id="e2efb-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="e2efb-112">Voorbeeld: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="e2efb-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="e2efb-113">**SKU** : een exemplaar van een aanbieding, zoals een grote release van een distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="e2efb-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="e2efb-114">Voorbeeld: 16.04-TNS</span><span class="sxs-lookup"><span data-stu-id="e2efb-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="e2efb-115">**Versie** -Hallo versienummer van een installatiekopie van het SKU.</span><span class="sxs-lookup"><span data-stu-id="e2efb-115">**Version** - hello version number of an image SKU.</span></span> <span data-ttu-id="e2efb-116">Wanneer u de installatiekopie van het Hallo opgeeft, kunt u Hallo versienummer met 'nieuwste' vervangen die Hallo meest recente versie van Hallo-distributiepunt selecteert.</span><span class="sxs-lookup"><span data-stu-id="e2efb-116">When specifying hello image, you can replace hello version number with "latest", which selects hello latest version of hello distribution.</span></span>

<span data-ttu-id="e2efb-117">toospecify een Marketplace-installatiekopie, doorgaans gebruikt u de installatiekopie van het Hallo *URN*.</span><span class="sxs-lookup"><span data-stu-id="e2efb-117">toospecify a Marketplace image, you typically use hello image *URN*.</span></span> <span data-ttu-id="e2efb-118">Hallo URN combineert deze waarden, gescheiden door een dubbele punt (:)-teken Hallo: *Publisher*:*bieden*:*Sku*:*versie*.</span><span class="sxs-lookup"><span data-stu-id="e2efb-118">hello URN combines these values, separated by hello colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="e2efb-119">Lijst met populaire installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="e2efb-119">List popular images</span></span>

<span data-ttu-id="e2efb-120">Hallo uitvoeren [az vm afbeeldingenlijst](/cli/azure/vm/image#list) opdracht zonder Hallo `--all` optie, toosee installatiekopieën van een lijst met populaire VM in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e2efb-120">Run hello [az vm image list](/cli/azure/vm/image#list) command, without hello `--all` option, toosee a list of popular VM images in hello Azure Marketplace.</span></span> <span data-ttu-id="e2efb-121">Bijvoorbeeld uitvoeren Hallo opdracht toodisplay na een in cache opgeslagen lijst van populaire afbeeldingen in tabelindeling:</span><span class="sxs-lookup"><span data-stu-id="e2efb-121">For example, run hello following command toodisplay a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="e2efb-122">Hallo uitvoer bevat Hallo URN (waarde in Hallo Hallo *Urn* kolom), waardoor u toospecify Hallo installatiekopie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e2efb-122">hello output includes hello URN (hello value in hello *Urn* column), which you use toospecify hello image.</span></span> <span data-ttu-id="e2efb-123">Wanneer u een virtuele machine maakt met een van deze populaire Marketplace-installatiekopieën, kunt u ook opgeven Hallo URN alias, zoals *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="e2efb-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify hello URN alias, such as *UbuntuLTS*.</span></span>

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

## <a name="find-specific-images"></a><span data-ttu-id="e2efb-124">Specifieke installatiekopieën zoeken</span><span class="sxs-lookup"><span data-stu-id="e2efb-124">Find specific images</span></span>

<span data-ttu-id="e2efb-125">een specifieke VM-installatiekopie in Marketplace, Hallo toofind gebruiken Hallo `az vm image list` opdracht Hello `--all` optie.</span><span class="sxs-lookup"><span data-stu-id="e2efb-125">toofind a specific VM image in hello Marketplace, use hello `az vm image list` command with hello `--all` option.</span></span> <span data-ttu-id="e2efb-126">Deze versie van de opdracht Hallo neemt enige tijd toocomplete en kunnen langdurige uitvoer geretourneerd zodat u meestal Hallo lijst filteren op `--publisher` of een andere parameter.</span><span class="sxs-lookup"><span data-stu-id="e2efb-126">This version of hello command takes some time toocomplete and can return lengthy output, so you usually filter hello list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="e2efb-127">Hallo volgende opdracht geeft bijvoorbeeld alle Debian-aanbiedingen (Vergeet niet dat zonder Hallo `--all` overschakelen, zoekt alleen lokale cache Hallo van algemene installatiekopieën):</span><span class="sxs-lookup"><span data-stu-id="e2efb-127">For example, hello following command displays all Debian offers (remember that without hello `--all` switch, it only searches hello local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="e2efb-128">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e2efb-128">Partial output:</span></span> 
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

<span data-ttu-id="e2efb-129">Toepassen van vergelijkbare filters Hello `--location`, `--publisher`, en `--sku` opties.</span><span class="sxs-lookup"><span data-stu-id="e2efb-129">Apply similar filters with hello `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="e2efb-130">U kunt zelfs gedeeltelijke overeenkomsten uitvoeren op een filter, zoals het zoeken naar `--offer Deb` toofind alle Debian installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="e2efb-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` toofind all Debian images.</span></span>

<span data-ttu-id="e2efb-131">Als u niet een bepaalde locatie met de Hallo opgeeft `--location` optie, Hallo waarden voor `westus` standaard worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e2efb-131">If you don't specify a particular location with hello `--location` option, hello values for `westus` are returned by default.</span></span> <span data-ttu-id="e2efb-132">(Een andere standaardlocatie ingesteld door `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="e2efb-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="e2efb-133">Bijvoorbeeld, Hallo volgende opdracht geeft een lijst van alle Debian 8 SKU's in `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="e2efb-133">For example, hello following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="e2efb-134">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e2efb-134">Partial output:</span></span>

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

## <a name="navigate-hello-images"></a><span data-ttu-id="e2efb-135">Navigeer Hallo installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="e2efb-135">Navigate hello images</span></span> 
<span data-ttu-id="e2efb-136">Een andere manier toofind een installatiekopie op een locatie wordt toorun hello [az vm image lijst-uitgevers](/cli/azure/vm/image#list-publishers), [az vm image lijst-aanbiedingen](/cli/azure/vm/image#list-offers), en [az vm image lijst-SKU's](/cli/azure/vm/image#list-skus) opdrachten in de reeks.</span><span class="sxs-lookup"><span data-stu-id="e2efb-136">Another way toofind an image in a location is toorun hello [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="e2efb-137">Met deze opdrachten moet u deze waarden bepalen:</span><span class="sxs-lookup"><span data-stu-id="e2efb-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="e2efb-138">Lijst Hallo installatiekopie uitgevers.</span><span class="sxs-lookup"><span data-stu-id="e2efb-138">List hello image publishers.</span></span>
2. <span data-ttu-id="e2efb-139">Geef de aanbiedingen voor een bepaalde uitgever weer.</span><span class="sxs-lookup"><span data-stu-id="e2efb-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="e2efb-140">Geef de SKU's voor een bepaalde aanbieding weer.</span><span class="sxs-lookup"><span data-stu-id="e2efb-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="e2efb-141">Bijvoorbeeld: hello volgende opdracht worden Hallo installatiekopie uitgevers in Hallo VS-West locatie:</span><span class="sxs-lookup"><span data-stu-id="e2efb-141">For example, hello following command lists hello image publishers in hello West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="e2efb-142">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e2efb-142">Partial output:</span></span>

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
<span data-ttu-id="e2efb-143">Gebruik die deze informatie toofind van een bepaalde uitgever biedt.</span><span class="sxs-lookup"><span data-stu-id="e2efb-143">Use this information toofind offers from a specific publisher.</span></span> <span data-ttu-id="e2efb-144">Bijvoorbeeld, als Canonical een installatiekopie-uitgever in Hallo locatie VS-West is, hun aanbiedingen vinden door te voeren `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="e2efb-144">For example, if Canonical is an image publisher in hello West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="e2efb-145">Hallo locatie en uitgever zoals in het volgende voorbeeld Hallo Hallo doorgeven:</span><span class="sxs-lookup"><span data-stu-id="e2efb-145">Pass hello location and hello publisher as in hello following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="e2efb-146">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e2efb-146">Output:</span></span>

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
<span data-ttu-id="e2efb-147">U ziet dat de Canonical in de regio VS-West Hallo Hallo publiceert **UbuntuServer** bieden op Azure.</span><span class="sxs-lookup"><span data-stu-id="e2efb-147">You see that in hello West US region, Canonical publishes hello **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="e2efb-148">Maar wat SKU's? tooget uitvoeren van deze waarden `azure vm image list-skus` en stel Hallo locatie, de uitgever en de aanbieding die u gedetecteerd:</span><span class="sxs-lookup"><span data-stu-id="e2efb-148">But what SKUs? tooget those values, run `azure vm image list-skus` and set hello location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="e2efb-149">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e2efb-149">Output:</span></span>

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

<span data-ttu-id="e2efb-150">Gebruik tot slot Hallo `az vm image list` opdracht toofind een specifieke versie van Hallo SKU die u bijvoorbeeld wilt **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="e2efb-150">Finally, use hello `az vm image list` command toofind a specific version of hello SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="e2efb-151">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e2efb-151">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="e2efb-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2efb-152">Next steps</span></span>
<span data-ttu-id="e2efb-153">Nu kunt u precies Hallo installatiekopie u toouse door duurt Opmerking Hallo URN waarde.</span><span class="sxs-lookup"><span data-stu-id="e2efb-153">Now you can choose precisely hello image you want toouse by taking note of hello URN value.</span></span> <span data-ttu-id="e2efb-154">Deze waarde Hello doorgeven `--image` parameter wanneer u een virtuele machine met de Hallo maakt [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e2efb-154">Pass this value with hello `--image` parameter when you create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="e2efb-155">Houd er rekening mee dat u eventueel Hallo-versienummer in Hallo URN door 'nieuwste vervangen kunt'.</span><span class="sxs-lookup"><span data-stu-id="e2efb-155">Remember that you can optionally replace hello version number in hello URN with "latest".</span></span> <span data-ttu-id="e2efb-156">Deze versie is altijd de nieuwste versie Hallo Hallo-verdeling.</span><span class="sxs-lookup"><span data-stu-id="e2efb-156">This version is always hello latest version of hello distribution.</span></span> <span data-ttu-id="e2efb-157">toocreate een virtuele machine snel met behulp van Hallo URN informatie, Zie [maken en beheren van virtuele Linux-machines Hello Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e2efb-157">toocreate a virtual machine quickly by using hello URN information, see [Create and Manage Linux VMs with hello Azure CLI](tutorial-manage-vm.md).</span></span>
