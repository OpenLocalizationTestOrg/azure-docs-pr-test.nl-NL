---
title: aaaIntroduction tooAzure Queue storage | Microsoft Docs
description: Inleiding tooAzure Queue storage
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
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="1b123-103">Inleiding tooQueues</span><span class="sxs-lookup"><span data-stu-id="1b123-103">Introduction tooQueues</span></span>

<span data-ttu-id="1b123-104">Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1b123-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="1b123-105">Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.</span><span class="sxs-lookup"><span data-stu-id="1b123-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="1b123-106">Veelvoorkomende toepassingen</span><span class="sxs-lookup"><span data-stu-id="1b123-106">Common uses</span></span>

<span data-ttu-id="1b123-107">Veelvoorkomende toepassingen van Queue Storage zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="1b123-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="1b123-108">Een achterstand van werk tooprocess maken asynchroon</span><span class="sxs-lookup"><span data-stu-id="1b123-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="1b123-109">Doorgeven van berichten van een Azure-web-rol tooan Azure-werkrol</span><span class="sxs-lookup"><span data-stu-id="1b123-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="1b123-110">Concepten van Queue-service</span><span class="sxs-lookup"><span data-stu-id="1b123-110">Queue service concepts</span></span>

<span data-ttu-id="1b123-111">Hallo Queue-service bevat Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="1b123-111">hello Queue service contains hello following components:</span></span>

![Wachtrij-concepten](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="1b123-113">**URL-indeling:** wachtrijen worden opgevraagd met Hallo URL-indeling te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b123-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="1b123-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="1b123-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="1b123-115">URL na Hello wordt een wachtrij in Hallo diagram:</span><span class="sxs-lookup"><span data-stu-id="1b123-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="1b123-116">**Storage-account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1b123-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="1b123-117">Zie [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (Schaalbaarheids- en prestatiedoelen in Azure Storage) voor meer informatie over opslagaccountcapaciteit.</span><span class="sxs-lookup"><span data-stu-id="1b123-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="1b123-118">**Wachtrij:** Een wachtrij bevat een set berichten.</span><span class="sxs-lookup"><span data-stu-id="1b123-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="1b123-119">Alle berichten moeten zich in een wachtrij bevinden.</span><span class="sxs-lookup"><span data-stu-id="1b123-119">All messages must be in a queue.</span></span> <span data-ttu-id="1b123-120">Houd er rekening mee dat Hallo wachtrijnaam moet alleen kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="1b123-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="1b123-121">Zie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Wachtrijen en metagegevens een naam geven) voor informatie over de naamgeving van wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="1b123-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="1b123-122">**Bericht:** A-bericht, in een willekeurige indeling van up too64 KB.</span><span class="sxs-lookup"><span data-stu-id="1b123-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="1b123-123">Hallo maximale tijd aan dat een bericht in de wachtrij Hallo blijven kan is zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="1b123-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b123-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b123-124">Next steps</span></span>

* [<span data-ttu-id="1b123-125">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="1b123-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="1b123-126">Aan de slag met wachtrijen met .NET</span><span class="sxs-lookup"><span data-stu-id="1b123-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
