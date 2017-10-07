---
title: de uitvoer aaaJSON voor Stream Analytics | Microsoft Docs
description: Meer informatie over hoe Stream Analytics doel Azure Cosmos DB voor de JSON-uitvoer, voor het archiveren van gegevens en lage latentie query's op niet-gestructureerde JSON-gegevens.
keywords: JSON-uitvoer
documentationcenter: 
services: stream-analytics,documentdb
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 5d2a61a6-0dbf-4f1b-80af-60a80eb25dd1
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: fa717818c839ecd7a60fcee33d22011990fd5878
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="target-azure-cosmos-db-for-json-output-from-stream-analytics"></a>Azure Cosmos Doeldatabase voor JSON-uitvoer van de Stream Analytics
Stream Analytics kunt richten [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) inschakelen voor JSON-uitvoer, lage latentie en archiveren gegevensquery op niet-gestructureerde JSON-gegevens. Dit document bevat informatie over enkele aanbevolen procedures voor het implementeren van deze configuratie.

Voor gebruikers die niet bekend met Cosmos DB bent, Bekijk [leertraject voor Azure Cosmos DB](https://azure.microsoft.com/documentation/learning-paths/documentdb/) tooget gestart. 

Opmerking: Mongo DB API gebaseerd Cosmos DB verzamelingen wordt momenteel niet ondersteund. 

## <a name="basics-of-cosmos-db-as-an-output-target"></a>Basisprincipes van Cosmos-database als een output-doel
Hello Azure DB die Cosmos-uitvoer in Stream Analytics kunt schrijven uw stream resultaten als JSON-uitvoer in uw verzameling(en) Cosmos DB verwerken. Stream Analytics maakt geen verzamelingen in uw database, zodat u in plaats daarvan hoeft toocreate ze tevoren betaalt. Dit is zodat Hallo facturering kosten van Cosmos DB verzamelingen transparante tooyou zijn en zodat u Hallo-prestaties afstemmen kunt, consistentie en capaciteit van uw verzamelingen direct met Hallo [Cosmos DB-API's](https://msdn.microsoft.com/library/azure/dn781481.aspx). Wordt u aangeraden een Cosmos-DB-Database per taak toologically afzonderlijke streaming uw verzamelingen voor streaming-taak.

Sommige opties voor het verzamelen van Cosmos DB Hallo worden hieronder beschreven.

## <a name="tune-consistency-availability-and-latency"></a>Consistentie, beschikbaarheid en latentie afstemmen
toomatch uw vereisten van webtoepassingen Cosmos DB kunt u toofine afstemmen Hallo database en verzamelingen en controleer verschillen tussen de consistentie, beschikbaarheid en latentie. Afhankelijk van welke mate van lezen van consistentie op basis van de behoeften van uw scenario lezen en schrijven latentie, dat kunt u een consistentiecontrole-niveau voor het databaseaccount van uw. Standaard kunnen Cosmos DB ook synchrone indexeren op elke verzameling CRUD bewerking tooyour. Dit is een andere optie nuttig toocontrol Hallo schrijven leestijd prestaties in Cosmos-DB. Raadpleeg voor meer informatie over dit onderwerp Hallo [wijzigen van uw database en query consistentieniveaus](../documentdb/documentdb-consistency-levels.md) artikel.

## <a name="upserts-from-stream-analytics"></a>Upserts vanuit Stream Analytics
Stream Analytics-integratie met Cosmos DB, kunt u tooinsert of update-records in uw Cosmos-DB-verzameling op basis van een bepaalde Document-ID-kolom. Dit is ook bedoeld tooas een *Upsert*.

Stream Analytics maakt gebruik van een optimistische Upsert benadering, waarbij de updates worden alleen uitgevoerd als invoegen is mislukt vanwege een conflict van tooa Document-ID. Deze update wordt uitgevoerd door de Stream Analytics als een PATCH, zodat u kunt gedeeltelijke updates toohello document, dat wil zeggen het toevoegen van nieuwe eigenschappen of het vervangen van die een bestaande eigenschap incrementeel wordt uitgevoerd. Houd er rekening mee dat wijzigingen in waarden van Matrixeigenschappen in de JSON-document Hallo leiden tot volledige Hallo-matrix ophalen overschreven, dat wil zeggen Hallo matrix niet worden samengevoegd.

## <a name="data-partitioning-in-cosmos-db"></a>Partitioneren van gegevens in Cosmos-DB
Cosmos DB [gepartitioneerde verzamelingen](../cosmos-db/partition-data.md) Hallo aanbevolen benadering voor het partitioneren van uw gegevens zijn. 

Verzamelingen met één Cosmos DB kunt Stream Analytics nog steeds u voor uw gegevens op basis van Hallo querypatronen en prestatiebehoeften van uw toepassing toopartition. Elke verzameling mogelijk up too10GB van gegevens (maximaal) en op dit moment er geen manier tooscale up is bevatten (of overloop) een verzameling. Voor het uitbreiden, Stream Analytics kunt u toowrite toomultiple verzamelingen met een gegeven voorvoegsel (Zie onderstaande details van gebruik). Stream Analytics maakt gebruik van consistente Hallo [Hash partitie Resolver](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.partitioning.hashpartitionresolver.aspx) strategie op basis van gebruiker Hallo opgegeven PartitionKey kolom toopartition de uitvoer-records. Hallo aantal verzamelingen met Hallo voorvoegsel gegeven op Hallo streaming begintijd van taak wordt gebruikt als Hallo uitvoer partitie aantal toowhich Hallo taak schrijft tooin parallel (Cosmos DB verzamelingen = uitvoer partities). Voor één verzameling met de vertraagde indexering doen alleen ingevoegd, over 0,4 schrijfbewerkingen MB/s kan worden verwacht. Met behulp van meerdere verzamelingen, kunt u tooachieve hogere doorvoer en verbeterde capaciteit.

Als u van plan aantal tooincrease Hallo-partities in toekomstige hello bent, moet u mogelijk toostop de taak opnieuw partitioneren Hallo gegevens van uw bestaande verzamelingen in nieuwe verzamelingen en vervolgens opnieuw opstarten Hallo Stream Analytics-taak. Meer informatie over het gebruik van PartitionResolver en opnieuw partitioneren samen met voorbeeldcode, worden opgenomen in een vervolgzelfstudie post. Hallo artikel [partitionering en schalen in Cosmos DB](../documentdb/documentdb-partition-data.md) biedt ook informatie over dit.

## <a name="cosmos-db-settings-for-json-output"></a>Cosmos DB-instellingen voor JSON-uitvoer
Maken van de Cosmos-DB als uitvoer in Stream Analytics genereert een prompt voor meer informatie, zoals hieronder wordt weergegeven. Deze sectie bevat een uitleg van Hallo eigenschappen definitie.

Gepartitioneerde verzameling | Verzamelingen met meerdere 'Één partitie'
---|---
![documentdb stream analytics uitvoerscherm](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-1.png) |  ![documentdb stream analytics uitvoerscherm](media/stream-analytics-documentdb-output/stream-analytics-documentdb-output-2.png)


  
> [!NOTE]
> Hallo **meerdere verzamelingen met 'Één partitie'** scenario vereist een partitiesleutel en configuratie wel wordt ondersteund. 

* **Uitvoer Alias** – een alias toorefer dit uitvoer in uw query ASA  
* **De accountnaam** – Hallo-naam of het eindpunt-URI van Hallo Cosmos-DB-account.  
* **Account van de sleutel** – Hallo gedeelde toegangssleutel voor Hallo Cosmos-DB-account.  
* **Database** – hello Cosmos DB databasenaam.  
* **Verzameling naampatroon** – Hallo verzamelingsnaam of hun patroon voor Hallo verzamelingen toobe gebruikt. indeling van de verzameling Hallo kan worden samengesteld met Hallo optionele {partition}-token, waarbij partities beginnen bij 0. Hieronder vindt u voorbeeld geldige invoer:  
  1\) MyCollection: een verzameling met de naam 'MyCollection' moet aanwezig zijn.  
  2\) MyCollection {partition} – deze verzamelingen moeten bestaan – 'MyCollection0', 'MyCollection1', 'MyCollection2', enzovoort.  
* **Partitie-sleutel** : optioneel. Dit is alleen nodig als u een token {partitie} in het patroon van de naam van verzameling. de naam van de Hallo van Hallo veld in de uitvoer gebeurtenissen die worden gebruikt toospecify Hallo sleutel voor het partitioneren van uitvoer in collecties. Voor één verzameling uitvoer, elke willekeurige uitvoerkolom kan worden gebruikt, bijvoorbeeld PartitionId.  
* **ID-document** : optioneel. Hallo-naam van Hallo veld in uitvoergebeurtenissen gebruikt toospecify Hallo primaire sleutel op welke insert of update bewerkingen zijn gebaseerd.  
