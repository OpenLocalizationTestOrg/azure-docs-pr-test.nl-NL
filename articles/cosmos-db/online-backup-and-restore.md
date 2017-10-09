---
title: aaaOnline back-up en herstel met Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe tooperform automatische back-up en herstellen op een Azure DB die Cosmos-database.
keywords: Backup and restore online back-up
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Automatische online back-up en herstel met Azure Cosmos-DB
Azure Cosmos-database wordt automatisch back-ups van al uw gegevens met regelmatige tussenpozen. Hallo automatische back-ups worden gemaakt zonder Hallo prestaties of beschikbaarheid van uw databasebewerkingen. Uw back-ups apart zijn opgeslagen in een andere storage-service en deze back-ups globaal voor tolerantie tegen regionale noodsituaties worden gerepliceerd. Hallo automatische back-ups zijn bedoeld voor scenario's wanneer u uw Comos DB-container per ongeluk verwijdert en later nodig hebt voor herstel van gegevens of een noodherstel.  

Dit artikel begint met een snelle samenvatting van Hallo gegevensredundantie en beschikbaarheid in een Cosmos-database en vervolgens back-ups besproken. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Hoge beschikbaarheid met Cosmos-DB - een samenvatting
Cosmos DB is ontworpen toobe [globaal gedistribueerde](distribute-data-globally.md) – Hiermee kunt u tooscale doorvoer over meerdere Azure-regio's samen met aangestuurd transparante multihoming API's en failover-beleid. Als een database system aanbieding [99,99% beschikbaarheid serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db), alle Hallo schrijfbewerkingen in Cosmos DB blijvend doorgevoerd toolocal schijven door een quorum van replica's binnen een lokaal datacenter zijn voordat de client toohello zijn bevestigd. Houd er rekening mee dat Hallo hoge beschikbaarheid van Cosmos-database is afhankelijk van de lokale opslag en is niet afhankelijk van een externe opslagtechnologieën. Als de databaseaccount gekoppeld aan meer dan één Azure-regio is, worden uw schrijfbewerkingen bovendien gerepliceerd in andere regio's ook. tooscale uw doorvoer en toegang tot gegevens op lage latenties, u kunt hebben als veel gebieden die zijn gekoppeld aan uw databaseaccount als u wilt lezen. In elke regio lezen, is de Hallo (gerepliceerd) gegevens blijvend persistent via een replicaset.  

Zoals geïllustreerd in het volgende diagram hello, een enkele Cosmos-DB-container is [horizontaal gepartitioneerde](partition-data.md). Een 'partitie' wordt aangeduid met een cirkel in het volgende diagram Hallo en elke partitie is maximaal beschikbaar is via een replicaset is gemaakt. Dit is de lokale distributiepunten Hallo binnen (aangeduid met Hallo X-as) één Azure-regio. Elke partitie (met de bijbehorende replica is ingesteld) wordt verder dan globaal gedistribueerd over meerdere regio's die zijn gekoppeld aan uw databaseaccount (bijvoorbeeld in deze afbeelding Hallo drie gebieden: VS-Oost, VS-West en centrale India). Hallo 'partitie instellen' is een wereldwijd gedistribueerde entiteit die bestaat uit meerdere exemplaren van uw gegevens in elke regio (aangeduid door Hallo Y-as). U kunt prioriteit toewijzen toohello regio's die zijn gekoppeld aan uw databaseaccount en Cosmos DB wordt transparant failover toohello volgende gebied in geval van noodsituaties. U kunt ook handmatig failover tootest Hallo end-to-end beschikbaarheid van uw toepassing simuleren.  

Hallo volgende afbeelding ziet u Hallo hoge mate van redundantie met Cosmos-DB.

![Hoge mate van redundantie met Cosmos-DB](./media/online-backup-and-restore/redundancy.png)

![Hoge mate van redundantie met Cosmos-DB](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Volledige, automatische, online back-ups
Oeps, verwijderd ik mijn container of de database. Met Cosmos DB, niet alleen uw gegevens, maar Hallo back-ups van uw gegevens worden ook gemaakt maximaal redundante en robuuste tooregional noodsituaties. Deze automatische back-ups worden momenteel ongeveer elke vier uur genomen en meest recente 2 back-ups te allen tijde worden opgeslagen. Als Hallo gegevens per ongeluk is verwijderd of beschadigd, neem [Neem contact op met de ondersteuning van Azure](https://azure.microsoft.com/support/options/) binnen de 8 uur. 

Hallo back-ups worden gemaakt zonder Hallo prestaties of beschikbaarheid van uw databasebewerkingen. Cosmos DB duurt Hallo back-up op de achtergrond Hallo zonder uw ingerichte RUs verbruikt of die betrekking hebben op prestaties Hallo en zonder Hallo beschikbaarheid van uw database. 

In tegenstelling tot de gegevens die zijn opgeslagen in Cosmos DB, Hallo automatische back-ups opgeslagen in Azure Blob Storage-service. lage latentie/efficiënt uploaden tooguarantee hello, Hallo momentopname van de back-up is geüploade tooan exemplaar van Azure Blob storage in dezelfde regio bevinden als de huidige schrijven regio van uw databaseaccount Cosmos DB Hallo Hallo. Voor tolerantie tegen regionale na noodgevallen, elke momentopname van de back-upgegevens in Azure Blob-opslag opnieuw gerepliceerd via geografisch redundante opslag (GRS) tooanother regio. Hallo volgende diagram ziet u dat Hallo volledige Cosmos-DB-container (met alle drie primaire partities in VS-West, in dit voorbeeld) is een back-up in een externe Azure Blob Storage-account in VS-West en vervolgens GRS tooEast gerepliceerd ons. 

Hallo volgende afbeelding ziet u periodieke volledige back-ups van alle Cosmos DB entiteiten in GRS Azure Storage.

![Periodieke volledige back-ups van alle Cosmos DB entiteiten in GRS Azure Storage](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Back-up bewaarperiode
Zoals hierboven wordt beschreven, wordt Azure Cosmos DB duurt momentopnamen van uw gegevens om de vier uur en behoudt de laatste twee momentopnamen Hallo van elke partitie gedurende 30 dagen. Per onze nalevingsreglementen worden momentopnamen na 90 dagen permanent verwijderd.

Als u uw eigen momentopnamen toomaintain wilt, kunt u de exportoptie tooJSON Hallo in hello Azure Cosmos DB [hulpprogramma voor gegevensmigratie](import-data.md#export-to-json-file) tooschedule aanvullende back-ups. 

## <a name="restoring-a-database-from-an-online-backup"></a>Een database terugzetten vanuit een online back-up
Als u de database of een verzameling per ongeluk verwijdert, kunt u [bestand een ondersteuningsticket](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) of [contact op met ondersteuning voor Azure](https://azure.microsoft.com/support/options/) toorestore Hallo gegevens van Hallo laatste automatische back-up. Als u uw database toorestore vanwege beschadigingsprobleem gegevens moet, Zie [afhandeling van gegevensbeschadiging](#handling-data-corruption) behoefte aanvullende tootake tooprevent Hallo beschadigd gegevens stappen vanuit penetrerende Hallo back-ups. Voor een specifieke momentopname van uw back-toobe hersteld vereist Cosmos DB Hallo gegevens is beschikbaar voor de duur van back-cyclus voor het die momentopname Hallo Hallo.

## <a name="handling-data-corruption"></a>Beschadigde gegevens verwerken
Azure Cosmos DB behoudt Hallo laatste twee back-ups van elke partitie in Hallo-systeem. Dit model werkt uitstekend wanneer een container (verzameling van documenten, grafiek, tabel) of een database per ongeluk worden verwijderd omdat een van de laatste versies Hallo kan worden hersteld. Echter in Hallo kan geval wanneer gebruikers leiden een probleem met de beschadiging van gegevens tot kunnen, Azure Cosmos DB mogelijk niet bewust van Hallo gegevensbeschadiging als het is mogelijk dat Hallo beschadiging hebben gepenetreerd Hallo back-ups. Zo snel is beschadigd, moet u Hallo beschadigd container (graph-verzameling/tabelnaam) verwijderen zodat back-ups worden beveiligd met beschadigde gegevens wordt overschreven. Omdat de laatste back-up Hallo kan vier uur oud is, Hallo-gebruiker kunt gebruikmaken van [wijzigen van de feed](change-feed.md) toocapture en store Hallo afgelopen vier uur waard van gegevens voordat u de container Hallo verwijdert.

## <a name="next-steps"></a>Volgende stappen

tooreplicate uw database in meerdere datacenters, Zie [distribueren van uw gegevens globaal met Cosmos DB](distribute-data-globally.md). 

toofile Neem contact op met ondersteuning van Azure [bestand een ticket van hello Azure-portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

