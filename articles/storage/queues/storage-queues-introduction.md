---
title: Inleiding tot Azure Queue storage | Microsoft Docs
description: Inleiding tot Azure Queue storage
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
ms.openlocfilehash: 4db7552a1b76c89151405c55c8682abbb5326bb6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-queues"></a><span data-ttu-id="01387-103">Inleiding tot wachtrijen</span><span class="sxs-lookup"><span data-stu-id="01387-103">Introduction to Queues</span></span>

<span data-ttu-id="01387-104">Azure Queue Storage is een service voor de opslag van grote aantallen berichten die via HTTP of HTTPS overal vandaan kunnen worden opgevraagd met geverifieerde aanroepen.</span><span class="sxs-lookup"><span data-stu-id="01387-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="01387-105">Een enkel wachtrijbericht mag maximaal 64 KB groot zijn en een wachtrij kan miljoenen berichten bevatten, tot de totale capaciteitslimiet van een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="01387-105">A single queue message can be up to 64 KB in size, and a queue can contain millions of messages, up to the total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="01387-106">Veelvoorkomende toepassingen</span><span class="sxs-lookup"><span data-stu-id="01387-106">Common uses</span></span>

<span data-ttu-id="01387-107">Veelvoorkomende toepassingen van Queue Storage zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="01387-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="01387-108">Het maken van een voorraad werk dat asynchroon moet worden verwerkt</span><span class="sxs-lookup"><span data-stu-id="01387-108">Creating a backlog of work to process asynchronously</span></span>
* <span data-ttu-id="01387-109">Het doorgeven van berichten van een Azure-webrol aan een Azure-werkrol</span><span class="sxs-lookup"><span data-stu-id="01387-109">Passing messages from an Azure web role to an Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="01387-110">Concepten van Queue-service</span><span class="sxs-lookup"><span data-stu-id="01387-110">Queue service concepts</span></span>

<span data-ttu-id="01387-111">De Queue-service bevat de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="01387-111">The Queue service contains the following components:</span></span>

![Wachtrij-concepten](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="01387-113">**URL-indeling:** Wachtrijen kunnen worden opgevraagd met de volgende URL-indeling:</span><span class="sxs-lookup"><span data-stu-id="01387-113">**URL format:** Queues are addressable using the following URL format:</span></span>   
    <span data-ttu-id="01387-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="01387-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="01387-115">Met de volgende URL wordt een wachtrij in het diagram opgevraagd:</span><span class="sxs-lookup"><span data-stu-id="01387-115">The following URL addresses a queue in the diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="01387-116">**Storage-account:** alle toegang tot Azure Storage vindt plaats via een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="01387-116">**Storage account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="01387-117">Zie [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (Schaalbaarheids- en prestatiedoelen in Azure Storage) voor meer informatie over opslagaccountcapaciteit.</span><span class="sxs-lookup"><span data-stu-id="01387-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="01387-118">**Wachtrij:** Een wachtrij bevat een set berichten.</span><span class="sxs-lookup"><span data-stu-id="01387-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="01387-119">Alle berichten moeten zich in een wachtrij bevinden.</span><span class="sxs-lookup"><span data-stu-id="01387-119">All messages must be in a queue.</span></span> <span data-ttu-id="01387-120">De naam van een wachtrij mag alleen kleine letters bevatten.</span><span class="sxs-lookup"><span data-stu-id="01387-120">Note that the queue name must be all lowercase.</span></span> <span data-ttu-id="01387-121">Zie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Wachtrijen en metagegevens een naam geven) voor informatie over de naamgeving van wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="01387-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="01387-122">**Bericht:** Een bericht in een willekeurige indeling, van maximaal 64 KB.</span><span class="sxs-lookup"><span data-stu-id="01387-122">**Message:** A message, in any format, of up to 64 KB.</span></span> <span data-ttu-id="01387-123">De maximale tijdsduur dat een bericht in de wachtrij blijven kan is zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="01387-123">The maximum time that a message can remain in the queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01387-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01387-124">Next steps</span></span>

* [<span data-ttu-id="01387-125">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="01387-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="01387-126">Aan de slag met wachtrijen met .NET</span><span class="sxs-lookup"><span data-stu-id="01387-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
