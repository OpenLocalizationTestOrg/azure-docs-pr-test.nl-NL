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
# <a name="introduction-tooqueues"></a>Inleiding tooQueues

Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS. Een enkel wachtrijbericht mag up too64 KB groot en een wachtrij kan miljoenen berichten up toohello totale capaciteitslimiet van een opslagaccount bevatten.

## <a name="common-uses"></a>Veelvoorkomende toepassingen

Veelvoorkomende toepassingen van Queue Storage zijn onder andere:

* Een achterstand van werk tooprocess maken asynchroon
* Doorgeven van berichten van een Azure-web-rol tooan Azure-werkrol

## <a name="queue-service-concepts"></a>Concepten van Queue-service

Hallo Queue-service bevat Hallo volgende onderdelen:

![Wachtrij-concepten](./media/storage-queues-introduction/queue1.png)

* **URL-indeling:** wachtrijen worden opgevraagd met Hallo URL-indeling te volgen:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    URL na Hello wordt een wachtrij in Hallo diagram:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Storage-account:** alle toegang tot tooAzure opslag wordt gedaan via een opslagaccount. Zie [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) (Schaalbaarheids- en prestatiedoelen in Azure Storage) voor meer informatie over opslagaccountcapaciteit.

* **Wachtrij:** Een wachtrij bevat een set berichten. Alle berichten moeten zich in een wachtrij bevinden. Houd er rekening mee dat Hallo wachtrijnaam moet alleen kleine letters bevatten. Zie [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx) (Wachtrijen en metagegevens een naam geven) voor informatie over de naamgeving van wachtrijen.

* **Bericht:** A-bericht, in een willekeurige indeling van up too64 KB. Hallo maximale tijd aan dat een bericht in de wachtrij Hallo blijven kan is zeven dagen.

## <a name="next-steps"></a>Volgende stappen

* [Een opslagaccount maken](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Aan de slag met wachtrijen met .NET](storage-dotnet-how-to-use-queues.md)
