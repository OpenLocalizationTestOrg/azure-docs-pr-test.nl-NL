---
title: prestatieniveaus aaaDocumentDB API | Microsoft Docs
description: Meer informatie over hoe prestatieniveaus DocumentDB API u tooreserve doorvoer op basis van de per-container kunnen.
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a>Hallo S1, S2 en S3 prestatieniveaus buiten gebruik stellen

> [!IMPORTANT] 
> Hallo te S1, S2 en S3 prestatieniveaus, besproken in dit artikel worden buiten gebruik gesteld en zijn niet meer beschikbaar voor nieuwe DocumentDB-API-accounts.
>

Dit artikel biedt een overzicht van S1, S2 en S3 prestatieniveaus en wordt beschreven hoe Hallo verzamelingen die gebruikmaken van deze prestatieniveaus gemigreerde toosingle partitie verzamelingen op 1e augustus 2017 zijn. Na het lezen van dit artikel, moet u kunnen tooanswer Hallo vragen te volgen:

- [Waarom worden Hallo S1, S2 en S3 prestaties niveaus buiten gebruik gesteld?](#why-retired)
- [Hoe verzamelingen met één partitie en gepartitioneerde verzamelingen Vergelijk toohello S1, S2 S3 prestatieniveaus?](#compare)
- [Wat kan ik moet toodo tooensure ononderbroken toegangsgegevens toomy?](#uninterrupted-access)
- [Hoe wordt mijn verzameling wijzigen na de migratie Hallo?](#collection-change)
- [Hoe wordt mijn facturering wijzigen nadat ik gemigreerde toosingle partitie verzamelingen?](#billing-change)
- [Wat gebeurt er als ik meer dan 10 GB aan opslagruimte nodig?](#more-storage-needed)
- [Kan ik tussen Hallo S1, S2 en S3 prestatieniveaus vóór 1 augustus 2017 wijzigen?](#change-before)
- [Hoe weet ik wanneer de verzameling is gemigreerd?](#when-migrated)
- [Hoe Migreer ik van Hallo S1, S2, S3 prestaties niveaus toosingle verzamelingen partitie zelf?](#migrate-diy)
- [Hoe ben ik als ik een klant EA beïnvloed?](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a>Waarom worden Hallo S1, S2 en S3 prestaties niveaus buiten gebruik gesteld?

Hallo S1, S2 en S3 prestatieniveaus doen niet aanbieding Hallo flexibiliteit die verzamelingen van DocumentDB API biedt. Hello S1, S2, S3 prestatieniveaus, beide Hallo doorvoer en de opslagcapaciteit vooraf zijn ingesteld en is niet aangeboden elasticiteit. Azure Cosmos DB biedt nu Hallo mogelijkheid toocustomize uw doorvoer en opslag, biedt veel meer flexibiliteit in uw tooscale mogelijkheid naar behoefte.

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a>Hoe verzamelingen met één partitie en gepartitioneerde verzamelingen Vergelijk toohello S1, S2 S3 prestatieniveaus?

Hallo volgende tabel vergelijkt Hallo doorvoer en opslag beschikbare opties in verzamelingen met één partitie, gepartitioneerde verzamelingen en S1, S2, S3 prestatieniveaus. Hier volgt een voorbeeld voor de regio VS Oost 2:

|   |Gepartitioneerde verzameling|Verzameling van één partitie|S1|S2|S3|
|---|---|---|---|---|---|
|Maximale doorvoer|Onbeperkt|10 K RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Minimaal doorvoer|2.5 K RU/s|400 RU/s|250 RU/s|1 K RU/s|2.5 K RU/s|
|Maximale opslag|Onbeperkt|10 GB|10 GB|10 GB|10 GB|
|Prijs (maandelijks)|Doorvoer: $6 / 100 RU/s<br><br>Opslag: $ 0,25/GB|Doorvoer: $6 / 100 RU/s<br><br>Opslag: $ 0,25/GB|25 USD $|50 USD $|100 USD $|

Weet u een klant EA? Zo ja, Zie [hoe ben ik beïnvloed als ik een klant EA?](#ea-customer)

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a>Wat kan ik moet toodo tooensure ononderbroken toegangsgegevens toomy?

Er is niets, Cosmos DB Hallo migratie voor u verwerkt. Als u een verzameling S1, S2 of S3 hebt, worden uw huidige verzameling gemigreerde tooa één partitie verzameling op 31 juli 2017. 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a>Hoe wordt mijn verzameling wijzigen na de migratie Hallo?

Als u een verzameling S1 hebt, kunt u zich gemigreerde tooa één partitie verzameling met 400 RU/s-doorvoer. 400 RU/s is Hallo laagste doorvoer beschikbaar met verzamelingen met één partitie. Hallo-kosten voor 400 RU/s in een verzameling één partitie is ongeveer Hallo gelijk zijn aan u zijn betaling met uw verzameling S1 Hallo en 250 RU/s – zodat u niet betalen Hallo echter extra 150 RU/s beschikbaar tooyou.

Als u een verzameling S2 hebt, kunt u zich gemigreerde tooa één partitie verzameling met 1 K RU/s. Hier ziet u geen wijziging tooyour doorvoerniveau.

Als u een verzameling S3 hebt, kunt u zich gemigreerde tooa één partitie verzameling met 2,5 K RU/s. Hier ziet u geen wijziging tooyour doorvoerniveau.

In elk van deze gevallen, nadat uw verzameling wordt gemigreerd, u worden kunnen toocustomize uw doorvoerniveau of het omhoog en omlaag schalen als benodigde tooprovide lage latentie toegang tooyour gebruikers. toochange hello doorvoerniveau nadat uw verzameling is gemigreerd, gewoon uw account Cosmos DB in hello Azure-portal openen, klikt u op schaal, kies uw verzameling en pas Hallo doorvoerniveau, zoals wordt weergegeven in de volgende schermafbeelding Hallo:

![Hoe tooscale doorvoer in hello Azure-portal](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a>Hoe wordt mijn facturering wijzigen nadat ik verzamelingen met één partitie gemigreerde toohello?

Ervan uitgaande dat u 10 S1 verzamelingen, 1 GB aan opslagruimte voor elk in de regio VS-Oost Hallo hebt en u deze 10 S1 verzamelingen too10 verzamelingen met één partitie op 400 RU per seconde (minimaal niveau hebben Hallo) migreert. Uw factuur wordt er als volgt uitzien als u verzamelingen met Hallo 10 één partitie voor een volledige maand behouden:

![Hoe too10 verzamelingen S1 prijzen voor 10 verzamelingen vergelijkt met prijzen voor een verzameling van één partitie](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a>Wat gebeurt er als ik meer dan 10 GB aan opslagruimte nodig?

Of u een verzameling met een prestatieniveau S1, S2 of S3 of een verzameling van één partitie, die allemaal 10 GB aan opslagruimte hebt, kunt u Hallo Cosmos DB Data Migration tool toomigrate uw gegevens tooa gepartitioneerd verzameling met vrijwel onbeperkte opslag. Zie voor meer informatie over Hallo voordelen van een gepartitioneerde verzameling [partitionering en schalen in Azure Cosmos DB](documentdb-partition-data.md). Voor informatie over het toomigrate uw S1, S2, S3 of één partitie verzameling tooa gepartitioneerd verzameling, Zie [migreren van één partitie toopartitioned verzamelingen](documentdb-partition-data.md#migrating-from-single-partition). 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a>Kan ik tussen Hallo S1, S2 en S3 prestatieniveaus vóór 1 augustus 2017 wijzigen?

Alleen bestaande accounts met S1, S2 en S3 prestaties wordt kunnen toochange en alter niveau prestatielagen via Hallo portal of programmatisch. 1 augustus 2017 Hallo S1, S2 en prestatieniveaus S3 niet langer beschikbaar. Als u uit S1, S3 of S3 tooa één partitie verzameling wijzigt, kunt niet u teruggaan toohello S1, S2 of S3 prestatieniveaus.

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a>Hoe weet ik wanneer de verzameling is gemigreerd?

Hallo migratie wordt uitgevoerd op 31 juli 2017. Als u een verzameling hebt die gebruikmaakt van Hallo S1, S2 of S3 prestatieniveaus, Hallo Cosmos-DB-team neemt contact met u per e-mail voordat Hallo migratie plaatsvindt. Wanneer Hallo migratie voltooid, op 1 augustus 2017 is weergegeven hello Azure-portal dat gebruikmaakt van uw verzameling standaardprijzen.

![Hoe tooconfirm uw verzameling is gemigreerd toohello standaardcategorie prijzen](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a>Hoe Migreer ik van Hallo S1, S2, S3 prestaties niveaus toosingle verzamelingen partitie zelf?

U kunt migreren vanaf Hallo S1, S2 en S3 prestaties niveaus toosingle partitie verzamelingen met hello Azure-portal of programmatisch. U kunt dit doen op uw eigen vóór 1 augustus toobenefit uit Hallo doorvoer flexibele opties beschikbaar met verzamelingen met één partitie of we uw verzamelingen die u wilt migreren op 31 juli 2017.

**verzamelingen toomigrate toosingle partitie met hello Azure-portal**

1. In Hallo [ **Azure-portal**](https://portal.azure.com), klikt u op **Azure Cosmos DB**, selecteer vervolgens Hallo Cosmos DB account toomodify. 
 
    Als **Azure Cosmos DB** is niet op Hallo van Snelbalk, klikt u op >, te schuiven**Databases**, selecteer **Azure Cosmos DB**, en selecteer vervolgens Hallo DocumentDB-account.  

2. Hallo resource menu onder **Containers**, klikt u op **Scale**Hallo verzameling toomodify selecteert in de vervolgkeuzelijst Hallo en klik vervolgens op **prijscategorie**. Accounts met behulp van vooraf gedefinieerde doorvoer hebben een prijscategorie S1, S2 of S3.  In Hallo **Kies uw prijscategorie** blade, klikt u op **standaard** toochange toouser gedefinieerde doorvoer en klik vervolgens op **Selecteer** toosave uw wijziging.

    ![Schermopname van de blade instellingen Hallo weergegeven waar toochange doorvoercapaciteit Hallo](./media/performance-levels/change-performance-set-thoughput.png)

3. Terug in Hallo **Scale** blade, Hallo **prijscategorie** wordt gewijzigd te**standaard** en Hallo **doorvoer (RU/s)** wordt weergegeven met een de standaardwaarde van 400. Set Hallo doorvoer tussen 400 en 10.000 [Aanvraageenheden](request-units.md)/second (RU/s). Hallo **maandelijkse factuur geschatte** onderin Hallo Hallo pagina wordt automatisch bijgewerkt tooprovide een schatting maken van Hallo maandelijkse kosten. 

    >[!IMPORTANT] 
    > Nadat u uw wijzigingen hebt opgeslagen en de Standard-prijscategorie toohello verplaatsen, terugdraaien u niet toohello S1, S2 of S3 prestatieniveaus.

4. Klik op **opslaan** toosave uw wijzigingen.

    Als u vaststelt dat u meer doorvoer (groter dan 10.000 RU/s) of meer opslagruimte moet (groter dan 10GB), kunt u een gepartitioneerde verzameling kunt maken. Zie voor een verzameling van één partitie verzameling tooa gepartitioneerd, toomigrate [migreren van één partitie toopartitioned verzamelingen](documentdb-partition-data.md#migrating-from-single-partition).

    > [!NOTE]
    > Het wijzigen van S1, S2 of S3 tooStandard kan up too2 minuten duren.
    > 
    > 

**verzamelingen toomigrate toosingle partitie met Hallo .NET SDK**

Er is een andere optie voor het wijzigen van de uw verzamelingen prestatieniveaus via onze SDK's. Deze sectie bevat alleen de prestaties van een verzameling wijzigen met behulp van het serviceniveau onze [DocumentDB .NET API](documentdb-sdk-dotnet.md), maar het Hallo-proces is vergelijkbaar voor onze andere SDK.

Hier volgt een codefragment voor het wijzigen van Hallo verzameling doorvoer too5 000 aanvraageenheden per seconde:
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

Ga naar [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview aanvullende voorbeelden en meer informatie over onze aanbieding methoden:

* [**ReadOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [**ReadOffersFeedAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [**ReplaceOfferAsync**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [**CreateOfferQuery**](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a>Hoe ben ik als ik een klant EA beïnvloed?

EA klanten worden beveiligd tot einde van het huidige contract Hallo prijs.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over prijzen en het beheren van gegevens met Azure Cosmos DB, bekijk deze resources:

1.  [Partitioneren van gegevens in Cosmos DB](documentdb-partition-data.md). Hallo verschil tussen één partitie container en gepartitioneerde containers, evenals tips voor het implementeren van een partitionering strategie tooscale naadloos.
2.  [Prijzen voor cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). Meer informatie over Hallo kosten van de inrichting van de doorvoer en opslag gebruiken.
3.  [Aanvraageenheden](request-units.md). Hallo-verbruik van doorvoer voor een andere bewerkingstypen, bijvoorbeeld lezen, schrijven, Query begrijpen.
