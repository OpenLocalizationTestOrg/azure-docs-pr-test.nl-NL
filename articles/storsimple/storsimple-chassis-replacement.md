---
title: aaaReplace chassis op StorSimple 8000 series apparaat | Microsoft Docs
description: Hierin wordt beschreven hoe Hallo chassis voor uw StorSimple-primaire behuizing of EBOD behuizing tooremove en vervangen.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a><span data-ttu-id="5a9bc-103">Vervang Hallo chassis op uw StorSimple-apparaat</span><span class="sxs-lookup"><span data-stu-id="5a9bc-103">Replace hello chassis on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="5a9bc-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5a9bc-104">Overview</span></span>
<span data-ttu-id="5a9bc-105">Deze zelfstudie wordt uitgelegd hoe tooremove en een chassis in een serie StorSimple 8000 apparaat vervangen.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-105">This tutorial explains how tooremove and replace a chassis in a StorSimple 8000 series device.</span></span> <span data-ttu-id="5a9bc-106">Hallo StorSimple 8100-model is een apparaat met één behuizing (één chassis), terwijl Hallo 8600 een dubbele behuizing-apparaat (twee chassis is).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-106">hello StorSimple 8100 model is a single enclosure device (one chassis), whereas hello 8600 is a dual enclosure device (two chassis).</span></span> <span data-ttu-id="5a9bc-107">Voor een model 8600 zijn mogelijk twee chassis dat op het apparaat van de Hallo kan mislukken: Hallo chassis voor primaire behuizing Hallo of Hallo chassis voor Hallo EBOD behuizing.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-107">For an 8600 model, there are potentially two chassis that could fail in hello device: hello chassis for hello primary enclosure or hello chassis for hello EBOD enclosure.</span></span>

<span data-ttu-id="5a9bc-108">In beide gevallen is Hallo vervanging chassis dat wordt geleverd door Microsoft leeg.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-108">In either case, hello replacement chassis that is shipped by Microsoft is empty.</span></span> <span data-ttu-id="5a9bc-109">Er is geen stroom en koeling Modules (PCMs), controller-modules Solid-State harde schijven (SSD's), harde schijven (HDD's) of EBOD modules worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-109">No Power and Cooling Modules (PCMs), controller modules, solid state disk drives (SSDs), hard disk drives (HDDs), or EBOD modules will be included.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a9bc-110">Voordat u verwijdert en vervangt chassis Hallo, bekijk de informatie van de Hallo veiligheid in [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-110">Before removing and replacing hello chassis, review hello safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-chassis"></a><span data-ttu-id="5a9bc-111">Hallo chassis verwijderen</span><span class="sxs-lookup"><span data-stu-id="5a9bc-111">Remove hello chassis</span></span>
<span data-ttu-id="5a9bc-112">Volg stappen tooremove Hallo chassis op uw StorSimple-apparaat Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-112">Perform hello following steps tooremove hello chassis on your StorSimple device.</span></span>

#### <a name="tooremove-a-chassis"></a><span data-ttu-id="5a9bc-113">tooremove een chassis</span><span class="sxs-lookup"><span data-stu-id="5a9bc-113">tooremove a chassis</span></span>
1. <span data-ttu-id="5a9bc-114">Zorg ervoor dat Hallo StorSimple-apparaat is afgesloten en alle Hallo stroomvoorziening is verbroken.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-114">Make sure that hello StorSimple device is shut down and disconnected from all hello power sources.</span></span>
2. <span data-ttu-id="5a9bc-115">Verwijder alle Hallo netwerk- en SAS-kabels, indien van toepassing.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-115">Remove all hello network and SAS cables, if applicable.</span></span>
3. <span data-ttu-id="5a9bc-116">Verwijder Hallo eenheid uit Hallo rack.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-116">Remove hello unit from hello rack.</span></span>
4. <span data-ttu-id="5a9bc-117">Verwijderen van Hallo schijven en noteer Hallo sleuven waaruit ze dan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-117">Remove each of hello drives and note hello slots from which they are removed.</span></span> <span data-ttu-id="5a9bc-118">Zie voor meer informatie [Hallo schijfstation verwijderen](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-118">For more information, see [Remove hello disk drive](storsimple-disk-drive-replacement.md#remove-the-disk-drive).</span></span>
5. <span data-ttu-id="5a9bc-119">Op Hallo EBOD behuizing (indien dit Hallo chassis dat is mislukt is), Hallo EBOD controller modules te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-119">On hello EBOD enclosure (if this is hello chassis that failed), remove hello EBOD controller modules.</span></span> <span data-ttu-id="5a9bc-120">Zie voor meer informatie [verwijderen van een domeincontroller EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-120">For more information, see [Remove an EBOD controller](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller).</span></span> 
   
    <span data-ttu-id="5a9bc-121">Primaire behuizing (indien dit is Hallo chassis dat is mislukt) Verwijder Hallo controllers op Hallo en houd er rekening mee Hallo sleuven waaruit ze dan worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-121">On hello primary enclosure (if this is hello chassis that failed), remove hello controllers and note hello slots from which they are removed.</span></span> <span data-ttu-id="5a9bc-122">Zie voor meer informatie [verwijderen van een domeincontroller](storsimple-controller-replacement.md#remove-a-controller).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-122">For more information, see [Remove a controller](storsimple-controller-replacement.md#remove-a-controller).</span></span>

## <a name="install-hello-chassis"></a><span data-ttu-id="5a9bc-123">Hallo chassis installeren</span><span class="sxs-lookup"><span data-stu-id="5a9bc-123">Install hello chassis</span></span>
<span data-ttu-id="5a9bc-124">Volg stappen tooinstall Hallo chassis op uw StorSimple-apparaat Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-124">Perform hello following steps tooinstall hello chassis on your StorSimple device.</span></span>

#### <a name="tooinstall-a-chassis"></a><span data-ttu-id="5a9bc-125">tooinstall een chassis</span><span class="sxs-lookup"><span data-stu-id="5a9bc-125">tooinstall a chassis</span></span>
1. <span data-ttu-id="5a9bc-126">Hallo chassis in Hallo rek koppelen.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-126">Mount hello chassis in hello rack.</span></span> <span data-ttu-id="5a9bc-127">Zie voor meer informatie [Rack koppelen uw StorSimple-8100-apparaat](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) of [Rack koppelen 8600 StorSimple-apparaat](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-127">For more information, see [Rack-mount your StorSimple 8100 device](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) or [Rack-mount your StorSimple 8600 device](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).</span></span>
2. <span data-ttu-id="5a9bc-128">Nadat het Hallo chassis is gekoppeld in Hallo rack, installeert u Hallo controller modules in Hallo die dezelfde geplaatst dat ze eerder zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-128">After hello chassis is mounted in hello rack, install hello controller modules in hello same positions that they were previously installed in.</span></span>
3. <span data-ttu-id="5a9bc-129">Installatie Hallo schijven in Hallo dezelfde plaatsen en sleuven ze eerder zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-129">Install hello drives in hello same positions and slots that they were previously installed in.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5a9bc-130">U wordt aangeraden dat u eerst Hallo SSD's in Hallo sleuven installeren en vervolgens Hallo HDD's installeren.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-130">We recommend that you install hello SSDs in hello slots first, and then install hello HDDs.</span></span>
   > 
   > 
4. <span data-ttu-id="5a9bc-131">Uw apparaat toohello gewenste bronnen verbinding maken met Hallo-apparaat is gekoppeld in Hallo rack en Hallo componenten zijn geïnstalleerd, en Hallo apparaat inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5a9bc-131">With hello device mounted in hello rack and hello components installed, connect your device toohello appropriate power sources, and turn on hello device.</span></span> <span data-ttu-id="5a9bc-132">Zie voor meer informatie [uw StorSimple 8100-apparaat bekabelen](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) of [uw StorSimple 8600-apparaat bekabelen](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-132">For details, see [Cable your StorSimple 8100 device](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) or [Cable your StorSimple 8600 device](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a9bc-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a9bc-133">Next steps</span></span>
<span data-ttu-id="5a9bc-134">Meer informatie over [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="5a9bc-134">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

