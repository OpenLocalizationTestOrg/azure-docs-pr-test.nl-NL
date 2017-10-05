---
title: Beheren van uw StorSimple-volumecontainers | Microsoft Docs
description: Legt uit hoe u kunt de pagina van de volume-containers voor de StorSimple Manager-service toevoegen, wijzigen of verwijderen van een volumecontainer.
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
ms.openlocfilehash: bb55a7a4bff0fd4319de6f6ce958686ad8a4142b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-storsimple-volume-containers"></a><span data-ttu-id="8e574-103">De StorSimple Manager-service gebruiken voor het beheren van StorSimple volumecontainers</span><span class="sxs-lookup"><span data-stu-id="8e574-103">Use the StorSimple Manager service to manage StorSimple volume containers</span></span>
## <a name="overview"></a><span data-ttu-id="8e574-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8e574-104">Overview</span></span>
<span data-ttu-id="8e574-105">Deze zelfstudie wordt uitgelegd hoe de StorSimple Manager-service maken en beheren van StorSimple volumecontainers gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8e574-105">This tutorial explains how to use the StorSimple Manager service to create and manage StorSimple volume containers.</span></span>

<span data-ttu-id="8e574-106">Een volumecontainer in een Microsoft Azure StorSimple-apparaat bevat een of meer volumes die storage-account, versleuteling en verbruik van bandbreedte-instellingen delen.</span><span class="sxs-lookup"><span data-stu-id="8e574-106">A volume container in a Microsoft Azure StorSimple device contains one or more volumes that share storage account, encryption, and bandwidth consumption settings.</span></span> <span data-ttu-id="8e574-107">Een apparaat kan meerdere volumecontainers voor alle volumes hebben.</span><span class="sxs-lookup"><span data-stu-id="8e574-107">A device can have multiple volume containers for all its volumes.</span></span> 

<span data-ttu-id="8e574-108">Een volumecontainer heeft de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="8e574-108">A volume container has the following attributes:</span></span>

* <span data-ttu-id="8e574-109">**Volumes** – de lagen of lokaal vastgemaakt StorSimple-volumes die zijn opgenomen in de volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="8e574-109">**Volumes** – The tiered or locally pinned StorSimple volumes that are contained within the volume container.</span></span> <span data-ttu-id="8e574-110">Een volumecontainer mag maximaal 256 StorSimple-volumes bevatten.</span><span class="sxs-lookup"><span data-stu-id="8e574-110">A volume container may contain up to 256 StorSimple volumes.</span></span>
* <span data-ttu-id="8e574-111">**Versleuteling** – een versleutelingssleutel die kan worden gedefinieerd voor elke volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="8e574-111">**Encryption** – An encryption key that can be defined for each volume container.</span></span> <span data-ttu-id="8e574-112">Deze sleutel wordt gebruikt voor het versleutelen van de gegevens die door uw StorSimple-apparaat wordt verzonden naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="8e574-112">This key is used for encrypting the data that is sent from your StorSimple device to the cloud.</span></span> <span data-ttu-id="8e574-113">Een defensie hoogwaardige AES-256-bitssleutel wordt gebruikt door de gebruiker ingevoerde sleutel.</span><span class="sxs-lookup"><span data-stu-id="8e574-113">A military-grade AES-256 bit key is used with the user-entered key.</span></span> <span data-ttu-id="8e574-114">Uw gegevens wilt beveiligen, is het raadzaam dat u altijd versleuteling van cloudopslag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="8e574-114">To secure your data, we recommend that you always enable cloud storage encryption.</span></span>
* <span data-ttu-id="8e574-115">**Storage-account** – het opslagaccount dat is gekoppeld aan uw serviceprovider voor cloud-opslag.</span><span class="sxs-lookup"><span data-stu-id="8e574-115">**Storage account** – The storage account that is linked to your cloud storage service provider.</span></span> <span data-ttu-id="8e574-116">Alle volumes die zich in een volumecontainer delen dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8e574-116">All the volumes residing in a volume container share this storage account.</span></span> <span data-ttu-id="8e574-117">U kunt een opslagaccount kiezen uit een bestaande lijst of maak een nieuw account als u de volumecontainer maken en geef vervolgens de referenties voor toegang voor dat account.</span><span class="sxs-lookup"><span data-stu-id="8e574-117">You can choose a storage account from an existing list, or create a new account when you create the volume container and then specify the access credentials for that account.</span></span>
* <span data-ttu-id="8e574-118">**Cloud bandbreedte** – de bandbreedte die door het apparaat worden gebruikt wanneer de gegevens van het apparaat worden verzonden naar de cloud.</span><span class="sxs-lookup"><span data-stu-id="8e574-118">**Cloud bandwidth** – The bandwidth consumed by the device when the data from the device is being sent to the cloud.</span></span> <span data-ttu-id="8e574-119">U kunt een bandbreedteregeling afdwingen door een waarde tussen 1 en 1000 Mbps bij het definiëren van deze container.</span><span class="sxs-lookup"><span data-stu-id="8e574-119">You can enforce a bandwidth control by specifying a value between 1 and 1000 Mbps when you define this container.</span></span> <span data-ttu-id="8e574-120">Als u het apparaat voor gebruik van alle beschikbare bandbreedte wilt, moet u dit veld ingesteld op onbeperkt.</span><span class="sxs-lookup"><span data-stu-id="8e574-120">If you want the device to consume all available bandwidth, set this field to Unlimited.</span></span> <span data-ttu-id="8e574-121">U kunt ook maken en toepassen van een bandbreedtesjabloon op basis van schema-bandbreedte toewijzen.</span><span class="sxs-lookup"><span data-stu-id="8e574-121">You can also create and apply a bandwidth template to allocate bandwidth based on schedule.</span></span>

![Volume containers pagina](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

<span data-ttu-id="8e574-123">Deze volgende procedures wordt uitgelegd hoe u de StorSimple **volumecontainers** pagina om de volgende algemene bewerkingen uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="8e574-123">This following procedures explain how to use the StorSimple **Volume containers** page to complete the following common operations:</span></span>

* <span data-ttu-id="8e574-124">Een volumecontainer toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e574-124">Add a volume container</span></span> 
* <span data-ttu-id="8e574-125">Een volumecontainer wijzigen</span><span class="sxs-lookup"><span data-stu-id="8e574-125">Modify a volume container</span></span> 
* <span data-ttu-id="8e574-126">Een volumecontainer verwijderen</span><span class="sxs-lookup"><span data-stu-id="8e574-126">Delete a volume container</span></span> 

## <a name="add-a-volume-container"></a><span data-ttu-id="8e574-127">Een volumecontainer toevoegen</span><span class="sxs-lookup"><span data-stu-id="8e574-127">Add a volume container</span></span>
<span data-ttu-id="8e574-128">Voer de volgende stappen uit om een volumecontainer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8e574-128">Perform the following steps to add a volume container.</span></span>

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a><span data-ttu-id="8e574-129">Een volumecontainer wijzigen</span><span class="sxs-lookup"><span data-stu-id="8e574-129">Modify a volume container</span></span>
<span data-ttu-id="8e574-130">Voer de volgende stappen uit voor het wijzigen van een volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="8e574-130">Perform the following steps to modify a volume container.</span></span>

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a><span data-ttu-id="8e574-131">Een volumecontainer verwijderen</span><span class="sxs-lookup"><span data-stu-id="8e574-131">Delete a volume container</span></span>
<span data-ttu-id="8e574-132">Een volumecontainer heeft volumes in het.</span><span class="sxs-lookup"><span data-stu-id="8e574-132">A volume container has volumes within it.</span></span> <span data-ttu-id="8e574-133">Worden kan verwijderd als de volumes die zijn opgenomen in het eerst worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8e574-133">It can be deleted only if all the volumes contained in it are first deleted.</span></span> <span data-ttu-id="8e574-134">Voer de volgende stappen uit voor het verwijderen van een volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="8e574-134">Perform the following steps to delete a volume container.</span></span>

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a><span data-ttu-id="8e574-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e574-135">Next steps</span></span>
* <span data-ttu-id="8e574-136">Meer informatie over [StorSimple-volumes beheren](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="8e574-136">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span> 
* <span data-ttu-id="8e574-137">Meer informatie over [de StorSimple Manager-service gebruiken voor het beheer van uw StorSimple-apparaat](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="8e574-137">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

