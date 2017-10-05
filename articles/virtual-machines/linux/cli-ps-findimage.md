---
title: "Selecteer de installatiekopieën van het Linux-VM met de Azure CLI | Microsoft Docs"
description: "Informatie over het gebruik van de Azure CLI om te bepalen van de uitgever, aanbieding, SKU en versie voor installatiekopieën van Marketplace VM."
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
ms.openlocfilehash: e0c27a7ee9e9a7ab1a3b004e070fa556b56a36a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-find-linux-vm-images-in-the-azure-marketplace-with-the-azure-cli"></a><span data-ttu-id="175ec-103">Linux-VM-installatiekopieën zoeken in Azure Marketplace met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="175ec-103">How to find Linux VM images in the Azure Marketplace with the Azure CLI</span></span>
<span data-ttu-id="175ec-104">Dit onderwerp wordt beschreven hoe u met de Azure CLI 2.0 VM-installatiekopieën vinden in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="175ec-104">This topic describes how to use the Azure CLI 2.0 to find VM images in the Azure Marketplace.</span></span> <span data-ttu-id="175ec-105">Deze informatie gebruiken om op te geven van een Marketplace-installatiekopie bij het maken van een Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="175ec-105">Use this information to specify a Marketplace image when you create a Linux VM.</span></span>

<span data-ttu-id="175ec-106">Zorg ervoor dat u de meest recente geïnstalleerd [Azure CLI 2.0](/cli/azure/install-az-cli2) en u bent aangemeld bij een Azure-account (`az login`).</span><span class="sxs-lookup"><span data-stu-id="175ec-106">Make sure that you installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and are logged in to an Azure account (`az login`).</span></span>

## <a name="terminology"></a><span data-ttu-id="175ec-107">Terminologie</span><span class="sxs-lookup"><span data-stu-id="175ec-107">Terminology</span></span>

<span data-ttu-id="175ec-108">Marketplace-installatiekopieën worden geïdentificeerd in de CLI en andere Azure-hulpprogramma's volgens een hiërarchie:</span><span class="sxs-lookup"><span data-stu-id="175ec-108">Marketplace images are identified in the CLI and other Azure tools according to a hierarchy:</span></span>

* <span data-ttu-id="175ec-109">**Publisher** -de organisatie die de installatiekopie heeft gemaakt.</span><span class="sxs-lookup"><span data-stu-id="175ec-109">**Publisher** - The organization that created the image.</span></span> <span data-ttu-id="175ec-110">Voorbeeld: canonieke</span><span class="sxs-lookup"><span data-stu-id="175ec-110">Example: Canonical</span></span>
* <span data-ttu-id="175ec-111">**Bieden** -een groep verwante afbeeldingen die zijn gemaakt door een uitgever.</span><span class="sxs-lookup"><span data-stu-id="175ec-111">**Offer** - A group of related images created by a publisher.</span></span> <span data-ttu-id="175ec-112">Voorbeeld: Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="175ec-112">Example: Ubuntu Server</span></span>
* <span data-ttu-id="175ec-113">**SKU** : een exemplaar van een aanbieding, zoals een grote release van een distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="175ec-113">**SKU** - An instance of an offer, such as a major release of a distribution.</span></span> <span data-ttu-id="175ec-114">Voorbeeld: 16.04-TNS</span><span class="sxs-lookup"><span data-stu-id="175ec-114">Example: 16.04-LTS</span></span>
* <span data-ttu-id="175ec-115">**Versie** -het versienummer van een installatiekopie van het SKU.</span><span class="sxs-lookup"><span data-stu-id="175ec-115">**Version** - The version number of an image SKU.</span></span> <span data-ttu-id="175ec-116">Bij het opgeven van de installatiekopie, kunt u het versienummer met 'nieuwste' vervangen die de meest recente versie van de verdeling selecteert.</span><span class="sxs-lookup"><span data-stu-id="175ec-116">When specifying the image, you can replace the version number with "latest", which selects the latest version of the distribution.</span></span>

<span data-ttu-id="175ec-117">Als u een Marketplace-installatiekopie, doorgaans gebruikt u de installatiekopie van het *URN*.</span><span class="sxs-lookup"><span data-stu-id="175ec-117">To specify a Marketplace image, you typically use the image *URN*.</span></span> <span data-ttu-id="175ec-118">Deze waarden, gescheiden door het teken van de dubbele punt (:) worden gecombineerd voor de URN: *Publisher*:*bieden*:*Sku*:*versie*.</span><span class="sxs-lookup"><span data-stu-id="175ec-118">The URN combines these values, separated by the colon (:) character: *Publisher*:*Offer*:*Sku*:*Version*.</span></span> 


## <a name="list-popular-images"></a><span data-ttu-id="175ec-119">Lijst met populaire installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="175ec-119">List popular images</span></span>

<span data-ttu-id="175ec-120">Voer de [az vm afbeeldingenlijst](/cli/azure/vm/image#list) opdracht, zonder de `--all` optie voor een overzicht van populaire VM-installatiekopieën in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="175ec-120">Run the [az vm image list](/cli/azure/vm/image#list) command, without the `--all` option, to see a list of popular VM images in the Azure Marketplace.</span></span> <span data-ttu-id="175ec-121">Voer bijvoorbeeld de volgende opdracht een lijst wilt weergeven in de cache van populaire afbeeldingen in tabelindeling:</span><span class="sxs-lookup"><span data-stu-id="175ec-121">For example, run the following command to display a cached list of popular images in table format:</span></span>

```azurecli
az vm image list --output table
```

<span data-ttu-id="175ec-122">De uitvoer bevat de URN (de waarde in de *Urn* kolom), waarmee u de installatiekopie opgeven.</span><span class="sxs-lookup"><span data-stu-id="175ec-122">The output includes the URN (the value in the *Urn* column), which you use to specify the image.</span></span> <span data-ttu-id="175ec-123">Wanneer u een virtuele machine maakt met een van deze populaire Marketplace-installatiekopieën, kunt u ook opgeven de alias URN zoals *UbuntuLTS*.</span><span class="sxs-lookup"><span data-stu-id="175ec-123">When creating a VM with one of these popular Marketplace images, you can alternatively specify the URN alias, such as *UbuntuLTS*.</span></span>

```
You are viewing an offline list of images, use --all to retrieve an up-to-date list
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

## <a name="find-specific-images"></a><span data-ttu-id="175ec-124">Specifieke installatiekopieën zoeken</span><span class="sxs-lookup"><span data-stu-id="175ec-124">Find specific images</span></span>

<span data-ttu-id="175ec-125">Ga voor een specifieke VM-installatiekopie in de Marketplace, gebruiken de `az vm image list` opdracht met de `--all` optie.</span><span class="sxs-lookup"><span data-stu-id="175ec-125">To find a specific VM image in the Marketplace, use the `az vm image list` command with the `--all` option.</span></span> <span data-ttu-id="175ec-126">Deze versie van de opdracht neemt enige tijd voltooid en kan langdurige uitvoer geretourneerd zodat u doorgaans de lijst filteren op `--publisher` of een andere parameter.</span><span class="sxs-lookup"><span data-stu-id="175ec-126">This version of the command takes some time to complete and can return lengthy output, so you usually filter the list by `--publisher` or another parameter.</span></span> 

<span data-ttu-id="175ec-127">De volgende opdracht geeft bijvoorbeeld alle Debian-aanbiedingen (Vergeet niet dat zonder de `--all` overschakelen, zoekt alleen de lokale cache van algemene installatiekopieën):</span><span class="sxs-lookup"><span data-stu-id="175ec-127">For example, the following command displays all Debian offers (remember that without the `--all` switch, it only searches the local cache of common images):</span></span>

```azurecli
az vm image list --offer Debian --all --output table 

```

<span data-ttu-id="175ec-128">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="175ec-128">Partial output:</span></span> 
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

<span data-ttu-id="175ec-129">Toepassen van filters voor soortgelijke de `--location`, `--publisher`, en `--sku` opties.</span><span class="sxs-lookup"><span data-stu-id="175ec-129">Apply similar filters with the `--location`, `--publisher`, and `--sku` options.</span></span> <span data-ttu-id="175ec-130">U kunt zelfs gedeeltelijke overeenkomsten uitvoeren op een filter, zoals het zoeken naar `--offer Deb` alle Debian installatiekopieën vinden.</span><span class="sxs-lookup"><span data-stu-id="175ec-130">You can even perform partial matches on a filter, such as searching for `--offer Deb` to find all Debian images.</span></span>

<span data-ttu-id="175ec-131">Als u geen dat een bepaalde locatie met opgeeft de `--location` optie, de waarden voor `westus` standaard worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="175ec-131">If you don't specify a particular location with the `--location` option, the values for `westus` are returned by default.</span></span> <span data-ttu-id="175ec-132">(Een andere standaardlocatie ingesteld door `az configure --defaults location=<location>`.)</span><span class="sxs-lookup"><span data-stu-id="175ec-132">(Set a different default location by running `az configure --defaults location=<location>`.)</span></span>

<span data-ttu-id="175ec-133">Bijvoorbeeld de volgende opdracht worden alle Debian 8 SKU's in `westeurope`:</span><span class="sxs-lookup"><span data-stu-id="175ec-133">For example, the following command lists all Debian 8 SKUs in `westeurope`:</span></span>

```azurecli
az vm image list --location westeurope --offer Deb --publisher credativ --sku 8 --all --output table
```

<span data-ttu-id="175ec-134">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="175ec-134">Partial output:</span></span>

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

## <a name="navigate-the-images"></a><span data-ttu-id="175ec-135">Installatiekopieën van het navigeren</span><span class="sxs-lookup"><span data-stu-id="175ec-135">Navigate the images</span></span> 
<span data-ttu-id="175ec-136">Een installatiekopie niet vinden in een locatie op een andere manier is om uit te voeren de [az vm image lijst-uitgevers](/cli/azure/vm/image#list-publishers), [az vm image lijst-aanbiedingen](/cli/azure/vm/image#list-offers), en [az vm image lijst-SKU's](/cli/azure/vm/image#list-skus) opdrachten in de reeks.</span><span class="sxs-lookup"><span data-stu-id="175ec-136">Another way to find an image in a location is to run the [az vm image list-publishers](/cli/azure/vm/image#list-publishers), [az vm image list-offers](/cli/azure/vm/image#list-offers), and [az vm image list-skus](/cli/azure/vm/image#list-skus) commands in sequence.</span></span> <span data-ttu-id="175ec-137">Met deze opdrachten moet u deze waarden bepalen:</span><span class="sxs-lookup"><span data-stu-id="175ec-137">With these commands, you determine these values:</span></span>

1. <span data-ttu-id="175ec-138">Geef de uitgevers van installatiekopieën weer.</span><span class="sxs-lookup"><span data-stu-id="175ec-138">List the image publishers.</span></span>
2. <span data-ttu-id="175ec-139">Geef de aanbiedingen voor een bepaalde uitgever weer.</span><span class="sxs-lookup"><span data-stu-id="175ec-139">For a given publisher, list their offers.</span></span>
3. <span data-ttu-id="175ec-140">Geef de SKU's voor een bepaalde aanbieding weer.</span><span class="sxs-lookup"><span data-stu-id="175ec-140">For a given offer, list their SKUs.</span></span>


<span data-ttu-id="175ec-141">De volgende opdracht worden bijvoorbeeld de uitgevers van de installatiekopie op de locatie VS-West:</span><span class="sxs-lookup"><span data-stu-id="175ec-141">For example, the following command lists the image publishers in the West US location:</span></span>

```azurecli
az vm image list-publishers --location westus --output table
```

<span data-ttu-id="175ec-142">Gedeeltelijke uitvoer:</span><span class="sxs-lookup"><span data-stu-id="175ec-142">Partial output:</span></span>

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
<span data-ttu-id="175ec-143">Gebruik deze informatie om te zoeken aanbiedingen van een bepaalde uitgever.</span><span class="sxs-lookup"><span data-stu-id="175ec-143">Use this information to find offers from a specific publisher.</span></span> <span data-ttu-id="175ec-144">Bijvoorbeeld, als Canonical een installatiekopie-uitgever op de locatie VS-West is, hun aanbiedingen vinden door te voeren `azure vm image list-offers`.</span><span class="sxs-lookup"><span data-stu-id="175ec-144">For example, if Canonical is an image publisher in the West US location, find their offers by running `azure vm image list-offers`.</span></span> <span data-ttu-id="175ec-145">Geef de locatie en de uitgever zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="175ec-145">Pass the location and the publisher as in the following example:</span></span>

```azurecli
az vm image list-offers --location westus --publisher Canonical --output table
```

<span data-ttu-id="175ec-146">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="175ec-146">Output:</span></span>

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
<span data-ttu-id="175ec-147">U ziet dat in de regio VS-West Canonical publiceert de **UbuntuServer** bieden op Azure.</span><span class="sxs-lookup"><span data-stu-id="175ec-147">You see that in the West US region, Canonical publishes the **UbuntuServer** offer on Azure.</span></span> <span data-ttu-id="175ec-148">Maar welke SKU's?</span><span class="sxs-lookup"><span data-stu-id="175ec-148">But what SKUs?</span></span> <span data-ttu-id="175ec-149">Uitvoeren als u deze waarden, `azure vm image list-skus` en stel de locatie, de uitgever en de aanbieding die u gedetecteerd:</span><span class="sxs-lookup"><span data-stu-id="175ec-149">To get those values, run `azure vm image list-skus` and set the location, publisher, and offer that you have discovered:</span></span>

```azurecli
az vm image list-skus --location westus --publisher Canonical --offer UbuntuServer --output table
```

<span data-ttu-id="175ec-150">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="175ec-150">Output:</span></span>

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

<span data-ttu-id="175ec-151">Gebruik tot slot de `az vm image list` opdracht om te bepalen van een specifieke versie van de SKU die u wilt bijvoorbeeld **16.04 LTS**:</span><span class="sxs-lookup"><span data-stu-id="175ec-151">Finally, use the `az vm image list` command to find a specific version of the SKU you want, for example, **16.04-LTS**:</span></span>

```azurecli
az vm image list --location westus --publisher Canonical --offer UbuntuServer --sku 16.04-LTS --all --output table
```

<span data-ttu-id="175ec-152">Uitvoer:</span><span class="sxs-lookup"><span data-stu-id="175ec-152">Output:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="175ec-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="175ec-153">Next steps</span></span>
<span data-ttu-id="175ec-154">U kunt nu nauwkeurig de installatiekopie die u gebruiken wilt door de URN-waarde.</span><span class="sxs-lookup"><span data-stu-id="175ec-154">Now you can choose precisely the image you want to use by taking note of the URN value.</span></span> <span data-ttu-id="175ec-155">Deze waarde met de `--image` parameter bij het maken van een virtuele machine met de [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="175ec-155">Pass this value with the `--image` parameter when you create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="175ec-156">Houd er rekening mee dat u eventueel het versienummer in de URN door 'nieuwste vervangen kunt'.</span><span class="sxs-lookup"><span data-stu-id="175ec-156">Remember that you can optionally replace the version number in the URN with "latest".</span></span> <span data-ttu-id="175ec-157">Deze versie is altijd de nieuwste versie van het distributiepunt.</span><span class="sxs-lookup"><span data-stu-id="175ec-157">This version is always the latest version of the distribution.</span></span> <span data-ttu-id="175ec-158">Om snel een virtuele machine maken met behulp van de URN informatie, Zie [maken en beheren van virtuele Linux-machines met de Azure CLI](tutorial-manage-vm.md).</span><span class="sxs-lookup"><span data-stu-id="175ec-158">To create a virtual machine quickly by using the URN information, see [Create and Manage Linux VMs with the Azure CLI](tutorial-manage-vm.md).</span></span>
