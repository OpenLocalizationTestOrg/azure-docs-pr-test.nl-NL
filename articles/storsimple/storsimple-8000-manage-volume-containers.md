---
title: aaaManage uw StorSimple-volumecontainers op Hallo StorSimple 8000 series apparaat | Microsoft Docs
description: Legt uit hoe u Hallo StorSimple Apparaatbeheer service volumecontainers tooadd pagina, wijzigen of verwijderen van een volumecontainer kunt gebruiken.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a><span data-ttu-id="57752-103">Hallo Apparaatbeheer StorSimple-service toomanage StorSimple volumecontainers gebruiken</span><span class="sxs-lookup"><span data-stu-id="57752-103">Use hello StorSimple Device Manager service toomanage StorSimple volume containers</span></span>

## <a name="overview"></a><span data-ttu-id="57752-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="57752-104">Overview</span></span>
<span data-ttu-id="57752-105">Deze zelfstudie wordt uitgelegd hoe toouse StorSimple Apparaatbeheer service toocreate Hallo en beheer containers voor StorSimple-volume.</span><span class="sxs-lookup"><span data-stu-id="57752-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage StorSimple volume containers.</span></span>

<span data-ttu-id="57752-106">Een volumecontainer in een Microsoft Azure StorSimple-apparaat bevat een of meer volumes die storage-account, versleuteling en verbruik van bandbreedte-instellingen delen.</span><span class="sxs-lookup"><span data-stu-id="57752-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="57752-107">Een apparaat kan meerdere volumecontainers voor alle volumes hebben.</span><span class="sxs-lookup"><span data-stu-id="57752-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="57752-108">Een volumecontainer heeft Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="57752-108">A volume container has hello following attributes:</span></span>

* <span data-ttu-id="57752-109">**Volumes** – Hallo lagen of lokaal vastgemaakt StorSimple-volumes die zijn opgenomen in de volumecontainer Hallo.</span><span class="sxs-lookup"><span data-stu-id="57752-109">**Volumes** – hello tiered or locally pinned StorSimple volumes that are contained within hello volume container.</span></span> 
* <span data-ttu-id="57752-110">**Versleuteling** – een versleutelingssleutel die kan worden gedefinieerd voor elke volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="57752-110">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="57752-111">Deze sleutel wordt gebruikt voor het versleutelen van Hallo-gegevens die worden verzonden vanuit uw StorSimple-apparaat toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="57752-111">This key is used for encrypting hello data that is sent from your StorSimple device toohello cloud.</span></span> <span data-ttu-id="57752-112">Een defensie hoogwaardige AES-256-bitssleutel wordt gebruikt met de gebruiker ingevoerde Hallo-sleutel.</span><span class="sxs-lookup"><span data-stu-id="57752-112">A military-grade AES-256 bit key is used with hello user-entered key.</span></span> <span data-ttu-id="57752-113">toosecure uw gegevens, het is raadzaam dat u altijd versleuteling van cloudopslag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="57752-113">toosecure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="57752-114">**Storage-account** – hello Azure storage-account is gebruikte toostore Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="57752-114">**Storage account** – hello Azure storage account that is used toostore hello data.</span></span> <span data-ttu-id="57752-115">Alle Hallo volumes die zich in een volumecontainer delen dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="57752-115">All hello volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="57752-116">U kunt een opslagaccount kiezen uit een bestaande lijst of maak een nieuw account als u Hallo volumecontainer maken en geef vervolgens Hallo-referenties voor dat account.</span><span class="sxs-lookup"><span data-stu-id="57752-116">You can choose a storage account from an existing list, or create a new account when you create hello volume container and then specify hello access credentials for that account.</span></span>
* <span data-ttu-id="57752-117">**Cloud bandbreedte** – Hallo netwerkbandbreedte verbruikt door Hallo apparaat wanneer het Hallo-gegevens van het Hallo-apparaat toohello cloud worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="57752-117">**Cloud bandwidth** – hello bandwidth consumed by hello device when hello data from hello device is being sent toohello cloud.</span></span> <span data-ttu-id="57752-118">U kunt een bandbreedteregeling afdwingen door een waarde tussen 1 en 1000 Mbps op te geven wanneer u deze container maken.</span><span class="sxs-lookup"><span data-stu-id="57752-118">You can enforce a bandwidth control by specifying a value between 1 Mbps and 1,000 Mbps when you create this container.</span></span> <span data-ttu-id="57752-119">Als u Hallo apparaat tooconsume alle beschikbare bandbreedte wilt, stelt u dit veld te**onbeperkt**.</span><span class="sxs-lookup"><span data-stu-id="57752-119">If you want hello device tooconsume all available bandwidth, set this field too**Unlimited**.</span></span> <span data-ttu-id="57752-120">U kunt ook maken en toepassen van een bandbreedte tooallocate bandbreedte van het sjabloon op basis van de planning.</span><span class="sxs-lookup"><span data-stu-id="57752-120">You can also create and apply a bandwidth template tooallocate bandwidth based on schedule.</span></span>

<span data-ttu-id="57752-121">Hallo volgende procedures wordt uitgelegd hoe toouse StorSimple Hallo **volumecontainers** blade toocomplete Hallo algemene bewerkingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="57752-121">hello following procedures explain how toouse hello StorSimple **Volume containers** blade toocomplete hello following common operations:</span></span>

* <span data-ttu-id="57752-122">Een volumecontainer toevoegen</span><span class="sxs-lookup"><span data-stu-id="57752-122">Add a volume container</span></span>
* <span data-ttu-id="57752-123">Een volumecontainer wijzigen</span><span class="sxs-lookup"><span data-stu-id="57752-123">Modify a volume container</span></span>
* <span data-ttu-id="57752-124">Een volumecontainer verwijderen</span><span class="sxs-lookup"><span data-stu-id="57752-124">Delete a volume container</span></span>

## <a name="add-a-volume-container"></a><span data-ttu-id="57752-125">Een volumecontainer toevoegen</span><span class="sxs-lookup"><span data-stu-id="57752-125">Add a volume container</span></span>
<span data-ttu-id="57752-126">Volgende stappen tooadd een volumecontainer Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="57752-126">Perform hello following steps tooadd a volume container.</span></span>

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="57752-127">Een volumecontainer wijzigen</span><span class="sxs-lookup"><span data-stu-id="57752-127">Modify a volume container</span></span>
<span data-ttu-id="57752-128">Volgende stappen toomodify een volumecontainer Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="57752-128">Perform hello following steps toomodify a volume container.</span></span>

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="57752-129">Een volumecontainer verwijderen</span><span class="sxs-lookup"><span data-stu-id="57752-129">Delete a volume container</span></span>
<span data-ttu-id="57752-130">Een volumecontainer heeft volumes in het.</span><span class="sxs-lookup"><span data-stu-id="57752-130">A volume container has volumes within it.</span></span> <span data-ttu-id="57752-131">Deze kan alleen als alle Hallo volumes die dit eerst worden verwijderd, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="57752-131">It can be deleted only if all hello volumes contained in it are first deleted.</span></span> <span data-ttu-id="57752-132">Volgende stappen toodelete een volumecontainer Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="57752-132">Perform hello following steps toodelete a volume container.</span></span>

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="57752-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="57752-133">Next steps</span></span>
* <span data-ttu-id="57752-134">Meer informatie over [StorSimple-volumes beheren](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="57752-134">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span> 
* <span data-ttu-id="57752-135">Meer informatie over [StorSimple Apparaatbeheer service tooadminister uw StorSimple-apparaat met behulp van Hallo](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="57752-135">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

