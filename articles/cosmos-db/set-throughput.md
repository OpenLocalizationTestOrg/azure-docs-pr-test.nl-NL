---
title: aaaProvision doorvoer voor Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe tooset ingerichte doorvoer voor uw Azure Cosmos DB containsers, verzamelingen, grafieken en tabellen.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Doorvoer instellen voor Azure DB die Cosmos-containers

U kunt doorvoer instellen voor uw Azure DB die Cosmos-containers in hello Azure-portal of met behulp van Hallo client-SDK's. 

Hallo volgende tabel geeft een lijst van Hallo doorvoer beschikbaar voor containers:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Container één partitie</strong></p></td>
            <td valign="top"><p><strong>Gepartitioneerde Container</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Minimaal doorvoer</p></td>
            <td valign="top"><p>400 aanvraageenheden per seconde</p></td>
            <td valign="top"><p>2500 aanvraageenheden per seconde</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Maximale doorvoer</p></td>
            <td valign="top"><p>10.000 aanvraageenheden per seconde</p></td>
            <td valign="top"><p>Onbeperkt</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>tooset hello doorvoer via hello Azure-portal

1. In een nieuw venster openen Hallo [Azure-portal](https://portal.azure.com).
2. Klik op Hallo linkerbalk op **Azure Cosmos DB**, of klik op **meer Services** onderin Hallo Schuif vervolgens te**Databases**, en klik vervolgens op **Azure Cosmos DB**.
3. Selecteer uw account Cosmos DB.
4. Op het nieuwe venster Hallo **Data Explorer (Preview)** in het navigatiemenu Hallo.
5. In nieuw venster hello, vouw uw database en de container en klik op **schaal & instellingen**.
6. In nieuw venster hello, typt u nieuwe doorvoercapaciteit in Hallo Hallo **doorvoer** vak en klik vervolgens op **opslaan**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>tooset hello doorvoer via Hallo DocumentDB-API voor .NET

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Veelgestelde vragen over doorvoer

**Kan ik mijn tooless doorvoer dan 400 RU/s instellen?**

400 RU/s is minimaal doorvoer Hallo beschikbaar zijn op verzamelingen met één partitie Cosmos-DB (2500 RU/s is Hallo minimale voor gepartitioneerde verzamelingen). Aanvraag eenheden worden ingesteld met intervallen van 100 RU/s, maar doorvoer kan niet worden ingesteld too100 RU/s of een willekeurige waarde kleiner is dan 400 RU/s. Als u op zoek bent naar een voordelige methode toodevelop en Cosmos DB testen, kunt u gratis Hallo [Azure Cosmos DB Emulator](local-emulator.md), die u lokaal kunt implementeren zonder kosten. 

**Hoe stel ik througput hello MongoDB-API gebruiken?**

Er is geen MongoDB-API-extensie tooset doorvoer. Hallo aanbeveling is toouse hello DocumentDB API, zoals wordt weergegeven [tooset Hallo doorvoer via Hallo DocumentDB-API voor .NET](#set-throughput-sdk).

## <a name="next-steps"></a>Volgende stappen

Zie toolearn meer informatie over het inrichten en gaat wereld-schaal met Cosmos-DB [partitionering en schalen met Cosmos DB](partition-data.md).
