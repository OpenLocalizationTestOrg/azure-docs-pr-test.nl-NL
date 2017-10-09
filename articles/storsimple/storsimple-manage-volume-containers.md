---
title: aaaManage uw StorSimple-volumecontainers | Microsoft Docs
description: Legt uit hoe u Hallo StorSimple Manager service volumecontainers tooadd pagina, wijzigen of verwijderen van een volumecontainer kunt gebruiken.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="8b1dd-103">Hallo StorSimple Manager-service toomanage StorSimple volumecontainers gebruiken</span><span class="sxs-lookup"><span data-stu-id="8b1dd-103">Use hello StorSimple Manager service toomanage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="8b1dd-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8b1dd-104">Overview</span></span>
<span data-ttu-id="8b1dd-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Manager service toocreate Hallo en beheer containers voor StorSimple-volume.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-105">This tutorial explains how toouse hello StorSimple Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="8b1dd-106">Een volumecontainer in een Microsoft Azure StorSimple-apparaat bevat een of meer volumes die storage-account, versleuteling en verbruik van bandbreedte-instellingen delen.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="8b1dd-107">Een apparaat kan meerdere volumecontainers voor alle volumes hebben.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="8b1dd-108">Een volumecontainer heeft Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="8b1dd-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="8b1dd-109">**Volumes** – Hallo lagen of lokaal vastgemaakt StorSimple-volumes die zijn opgenomen in de volumecontainer Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> <span data-ttu-id="8b1dd-110">Een volumecontainer kan up too256 StorSimple-volumes bevatten.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-110">A volume container may contain up too256 StorSimple volumes.</span></span>
* <span data-ttu-id="8b1dd-111">**Versleuteling** – een versleutelingssleutel die kan worden gedefinieerd voor elke volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="8b1dd-112">Deze sleutel wordt gebruikt voor het versleutelen van Hallo-gegevens die worden verzonden vanuit uw StorSimple-apparaat toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-112">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="8b1dd-113">Een defensie hoogwaardige AES-256-bitssleutel wordt gebruikt met de gebruiker ingevoerde Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-113">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="8b1dd-114">toosecure uw gegevens, het is raadzaam dat u altijd versleuteling van cloudopslag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-114">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="8b1dd-115">**Storage-account** – Hallo storage-account dat is gekoppeld tooyour cloud-opslag-serviceprovider.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-115">**Storage account** – hello storage account that is linked tooyour cloud storage service provider.</span></span> <span data-ttu-id="8b1dd-116">Alle Hallo volumes die zich in een volumecontainer delen dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-116">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="8b1dd-117">U kunt een opslagaccount kiezen uit een bestaande lijst of maak een nieuw account als u Hallo volumecontainer maken en geef vervolgens Hallo-referenties voor dat account.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-117">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="8b1dd-118">**Cloud bandbreedte** – Hallo netwerkbandbreedte verbruikt door Hallo apparaat wanneer het Hallo-gegevens van het Hallo-apparaat toohello cloud worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-118">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="8b1dd-119">U kunt een bandbreedteregeling afdwingen door een waarde tussen 1 en 1000 Mbps bij het definiëren van deze container.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="8b1dd-120">Als u Hallo apparaat tooconsume alle beschikbare bandbreedte wilt, stelt u dit veld tooUnlimited.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-120">If you want hello device tooconsume all available bandwidth, set this field tooUnlimited.</span></span> <span data-ttu-id="8b1dd-121">U kunt ook maken en toepassen van een bandbreedte tooallocate bandbreedte van het sjabloon op basis van de planning.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-121">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

![Volume containers pagina](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="8b1dd-123">Deze volgende procedures wordt uitgelegd hoe toouse StorSimple Hallo **volumecontainers** pagina toocomplete Hallo algemene bewerkingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b1dd-123">This following procedures explain how toouse hello StorSimple **Volume containers** page toocomplete hello following common operations:</span></span>

* <span data-ttu-id="8b1dd-124">Een volumecontainer toevoegen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-124">Add a volume container</span></span> 
* <span data-ttu-id="8b1dd-125">Een volumecontainer wijzigen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-125">Modify a volume container</span></span> 
* <span data-ttu-id="8b1dd-126">Een volumecontainer verwijderen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="8b1dd-127">Een volumecontainer toevoegen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-127">Add a volume container</span></span>
<span data-ttu-id="8b1dd-128">Volgende stappen tooadd een volumecontainer Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-128">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="8b1dd-129">Een volumecontainer wijzigen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-129">Modify a volume container</span></span>
<span data-ttu-id="8b1dd-130">Volgende stappen toomodify een volumecontainer Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-130">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="8b1dd-131">Een volumecontainer verwijderen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-131">Delete a volume container</span></span>
<span data-ttu-id="8b1dd-132">Een volumecontainer heeft volumes in het.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-132">A volume container has volumes within it.</span></span> <span data-ttu-id="8b1dd-133">Deze kan alleen als alle Hallo volumes die dit eerst worden verwijderd, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-133">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="8b1dd-134">Volgende stappen toodelete een volumecontainer Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8b1dd-134">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="8b1dd-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b1dd-135">Next steps</span></span>
* <span data-ttu-id="8b1dd-136">Meer informatie over [StorSimple-volumes beheren](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="8b1dd-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="8b1dd-137">Meer informatie over [StorSimple Manager service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8b1dd-137">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

