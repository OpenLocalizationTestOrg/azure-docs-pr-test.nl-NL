---
title: aaaIntroduction tooAzure Blob storage | Microsoft Docs
description: Inleiding tooAzure Blob-opslag
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="eb03e-103">Inleiding tooBlob opslag</span><span class="sxs-lookup"><span data-stu-id="eb03e-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="eb03e-104">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde objectgegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eb03e-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="eb03e-105">U kunt Blob storage-tooexpose gegevens openbaar toohello world of toostore toepassingsgegevens privé.</span><span class="sxs-lookup"><span data-stu-id="eb03e-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="eb03e-106">Veelvoorkomende toepassingen van Blob Storage zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="eb03e-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="eb03e-107">Voor afbeeldingen of documenten rechtstreeks tooa browser</span><span class="sxs-lookup"><span data-stu-id="eb03e-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="eb03e-108">De opslag van bestanden voor gedistribueerde toegang</span><span class="sxs-lookup"><span data-stu-id="eb03e-108">Storing files for distributed access</span></span>
* <span data-ttu-id="eb03e-109">Streaming van video en audio</span><span class="sxs-lookup"><span data-stu-id="eb03e-109">Streaming video and audio</span></span>
* <span data-ttu-id="eb03e-110">De opslag van gegevens voor back-up en herstel, herstel na noodgevallen en archivering</span><span class="sxs-lookup"><span data-stu-id="eb03e-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="eb03e-111">De opslag van gegevens voor analyse door een on-premises in Azure gehoste service</span><span class="sxs-lookup"><span data-stu-id="eb03e-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="eb03e-112">Concepten van Blob service</span><span class="sxs-lookup"><span data-stu-id="eb03e-112">Blob service concepts</span></span>

<span data-ttu-id="eb03e-113">Hallo Blob-service bevat Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="eb03e-113">hello Blob service contains hello following components:</span></span>

![Blobarchitectuur](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="eb03e-115">**Storage-Account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="eb03e-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="eb03e-116">Dit opslagaccount mag een **algemeen opslagaccount** of een **Blob-opslagaccount** die speciaal is bedoeld voor het opslaan van objecten/blobs.</span><span class="sxs-lookup"><span data-stu-id="eb03e-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="eb03e-117">Zie [Over Azure Storage-accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="eb03e-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="eb03e-118">**Container:** Een container is een groepering van een reeks blobs.</span><span class="sxs-lookup"><span data-stu-id="eb03e-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="eb03e-119">Alle blobs moeten zich in een container bevinden.</span><span class="sxs-lookup"><span data-stu-id="eb03e-119">All blobs must be in a container.</span></span> <span data-ttu-id="eb03e-120">Een account kan een onbeperkt aantal containers bevatten.</span><span class="sxs-lookup"><span data-stu-id="eb03e-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="eb03e-121">Een container kan een onbeperkt aantal blobs bevatten.</span><span class="sxs-lookup"><span data-stu-id="eb03e-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="eb03e-122">Houd er rekening mee dat Hallo containernaam moet een kleine letter.</span><span class="sxs-lookup"><span data-stu-id="eb03e-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="eb03e-123">**Blob:** Een bestand van willekeurig type en willekeurige grootte.</span><span class="sxs-lookup"><span data-stu-id="eb03e-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="eb03e-124">Azure Storage biedt drie typen blobs: blok-blobs, pagina-blobs en toevoeg-blobs.</span><span class="sxs-lookup"><span data-stu-id="eb03e-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="eb03e-125">*Blok-blobs* zijn ideaal voor de opslag van tekst- of binaire bestanden, zoals documenten en mediabestanden.</span><span class="sxs-lookup"><span data-stu-id="eb03e-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="eb03e-126">*Toevoeg-blobs* zijn vergelijkbaar tooblock blobs in dat ze bestaan uit blokken, maar ze zijn geoptimaliseerd voor toevoegbewerkingen; ze zijn daarom nuttig voor logboekscenario's.</span><span class="sxs-lookup"><span data-stu-id="eb03e-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="eb03e-127">Een enkel blok-blob kan bevatten up too50, 000 blokken van too100 MB, voor een totale grootte van iets meer dan 4.75 TB (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="eb03e-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="eb03e-128">Een enkele toevoeg-blob kan bevatten up too50, 000 blokken van too4 MB, voor een totale grootte van iets meer dan 195 GB (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="eb03e-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="eb03e-129">*Pagina-blobs* kan up too1 TB groot zijn en zijn efficiënter voor regelmatige lees-en schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="eb03e-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="eb03e-130">Virtuele Machines in Azure maakt gebruik van pagina-blobs als besturingssysteem en gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="eb03e-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="eb03e-131">Zie [Containers, blobs en metagegevens een naam geven en hiernaar verwijderen](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata) voor meer informatie over de naamgeving van containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="eb03e-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb03e-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eb03e-132">Next steps</span></span>

* [<span data-ttu-id="eb03e-133">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="eb03e-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="eb03e-134">Aan de slag met Blob storage met .NET</span><span class="sxs-lookup"><span data-stu-id="eb03e-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)