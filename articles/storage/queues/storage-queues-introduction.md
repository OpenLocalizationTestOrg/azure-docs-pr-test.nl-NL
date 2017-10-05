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
# <a name="introduction-to-queues"></a>Inleiding tot wachtrijen

Azure Queue Storage is een service voor de opslag van grote aantallen berichten die via HTTP of HTTPS overal vandaan kunnen worden opgevraagd met geverifieerde aanroepen. Een enkel wachtrijbericht mag maximaal 64 KB groot zijn en een wachtrij kan miljoenen berichten bevatten, tot de totale capaciteitslimiet van een opslagaccount.

## <a name="common-uses"></a>Veelvoorkomende toepassingen

Veelvoorkomende toepassingen van Queue Storage zijn onder andere:

* Het maken van een voorraad werk dat asynchroon moet worden verwerkt
* Het doorgeven van berichten van een Azure-webrol aan een Azure-werkrol

## <a name="queue-service-concepts"></a>Concepten van Queue-service

De Queue-service bevat de volgende onderdelen:

![Wachtrij-concepten](./media/storage-queues-introduction/queue1.png)

* **URL-indeling:** Wachtrijen kunnen worden opgevraagd met de volgende URL-indeling:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Met de volgende URL wordt een wachtrij in het diagram opgevraagd:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Storage-account:** alle toegang tot Azure Storage vindt plaats via een opslagaccount. Zie [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (Schaalbaarheids- en prestatiedoelen in Azure Storage) voor meer informatie over opslagaccountcapaciteit.

* **Wachtrij:** Een wachtrij bevat een set berichten. Alle berichten moeten zich in een wachtrij bevinden. De naam van een wachtrij mag alleen kleine letters bevatten. Zie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Wachtrijen en metagegevens een naam geven) voor informatie over de naamgeving van wachtrijen.

* **Bericht:** Een bericht in een willekeurige indeling, van maximaal 64 KB. De maximale tijdsduur dat een bericht in de wachtrij blijven kan is zeven dagen.

## <a name="next-steps"></a>Volgende stappen

* [Een opslagaccount maken](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Aan de slag met wachtrijen met .NET](storage-dotnet-how-to-use-queues.md)
