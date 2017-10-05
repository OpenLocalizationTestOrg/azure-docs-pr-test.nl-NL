---
title: Online back-up en herstel met Azure Cosmos DB | Microsoft Docs
description: Informatie over het uitvoeren van automatische back-up en herstellen op een Azure DB die Cosmos-database.
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
ms.openlocfilehash: 130f0eb259621737d6dbdb151e363915fb334ce1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Automatische online back-up en herstel met Azure Cosmos-DB
Azure Cosmos-database wordt automatisch back-ups van al uw gegevens met regelmatige tussenpozen. De automatische back-ups worden gemaakt zonder de prestaties of beschikbaarheid van uw databasebewerkingen. Uw back-ups apart zijn opgeslagen in een andere storage-service en deze back-ups globaal voor tolerantie tegen regionale noodsituaties worden gerepliceerd. De automatische back-ups zijn bedoeld voor scenario's wanneer u uw Comos DB-container per ongeluk verwijdert en later nodig hebt voor herstel van gegevens of een noodherstel.  

Dit artikel begint met een snelle samenvatting van de gegevensredundantie en beschikbaarheid in een Cosmos-database en vervolgens back-ups besproken. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Hoge beschikbaarheid met Cosmos-DB - een samenvatting
Cosmos DB is ontworpen om te worden [globaal gedistribueerde](distribute-data-globally.md) – Hiermee kunt u de schaal van doorvoer voor meerdere Azure-regio's samen met aangestuurd transparante multihoming API's en failover-beleid. Als een database system aanbieding [99,99% beschikbaarheid serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db), alle schrijfbewerkingen in Cosmos DB zijn blijvend doorgevoerd naar lokale schijven door een quorum van replica's binnen een lokale datacentrum voordat naar de client zijn bevestigd. Houd er rekening mee dat de hoge beschikbaarheid van de Cosmos-DB is afhankelijk van de lokale opslag, en is niet afhankelijk van een externe opslagtechnologieën. Als de databaseaccount gekoppeld aan meer dan één Azure-regio is, worden uw schrijfbewerkingen bovendien gerepliceerd in andere regio's ook. Als u wilt schalen de doorvoer en toegang tot gegevens op lage latenties, kunt u hebben zoals veel gebieden die zijn gekoppeld aan uw databaseaccount als u wilt lezen. In elke regio lezen, wordt de (gerepliceerde) gegevens blijvend vastgehouden in een replicaset.  

Zoals weergegeven in het volgende diagram, is het een enkele container van de Cosmos-DB [horizontaal gepartitioneerde](partition-data.md). Een 'partitie' wordt aangeduid met een cirkel in het volgende diagram en elke partitie is maximaal beschikbaar is via een replicaset is gemaakt. Dit is de lokale distributiepunten binnen (aangeduid met de X-as) één Azure-regio. Elke partitie (met de bijbehorende replica is ingesteld) wordt verder dan globaal gedistribueerd over meerdere regio's die zijn gekoppeld aan uw databaseaccount (bijvoorbeeld in deze afbeelding de drie regio's: VS-Oost, VS-West en centrale India). Het 'instellen voor partitie' is een wereldwijd gedistribueerde entiteit die bestaat uit meerdere exemplaren van uw gegevens in elke regio (aangeduid met de Y-as). U kunt de prioriteit toewijzen aan de regio's die zijn gekoppeld aan uw databaseaccount en Cosmos DB wordt transparant failover naar de volgende regio in geval van noodsituaties. U kunt ook handmatig failover wilt testen, de beschikbaarheid van de end-to-end van uw toepassing simuleren.  

De volgende afbeelding ziet u de hoge mate van redundantie met Cosmos-DB.

![Hoge mate van redundantie met Cosmos-DB](./media/online-backup-and-restore/redundancy.png)

![Hoge mate van redundantie met Cosmos-DB](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Volledige, automatische, online back-ups
Oeps, verwijderd ik mijn container of de database. Met Cosmos DB, niet alleen uw gegevens, maar de back-ups van uw gegevens worden ook aangebracht maximaal redundante en robuuste regionale noodsituaties. Deze automatische back-ups worden momenteel ongeveer elke vier uur genomen en meest recente 2 back-ups te allen tijde worden opgeslagen. Als de gegevens per ongeluk is verwijderd of beschadigd, neem [Neem contact op met de ondersteuning van Azure](https://azure.microsoft.com/support/options/) binnen de 8 uur. 

De back-ups worden gemaakt zonder de prestaties of beschikbaarheid van uw databasebewerkingen. Cosmos DB neemt de back-up op de achtergrond, zonder uw ingerichte RUs verbruikt of die betrekking hebben op de prestaties en zonder de beschikbaarheid van uw database. 

In tegenstelling tot de gegevens die zijn opgeslagen in Cosmos DB, worden de automatische back-ups worden opgeslagen in Azure Blob Storage-service. Om te waarborgen van de lage latentie/efficiënt uploaden, wordt de momentopname van de back-up geüpload naar een exemplaar van Azure Blob storage in dezelfde regio bevinden als de huidige schrijven regio van uw databaseaccount Cosmos DB. Voor tolerantie tegen regionale na noodgevallen, elke momentopname van de back-upgegevens in Azure Blob-opslag opnieuw gerepliceerd via geografisch redundante opslag (GRS) naar een andere regio. Het volgende diagram ziet dat de volledige container Cosmos-DB (met alle drie primaire partities in VS-West, in dit voorbeeld) is een back-up in een externe Azure Blob Storage-account in VS-West en vervolgens GRS gerepliceerd naar VS-Oost. 

De volgende afbeelding ziet u periodieke volledige back-ups van alle Cosmos DB entiteiten in GRS Azure Storage.

![Periodieke volledige back-ups van alle Cosmos DB entiteiten in GRS Azure Storage](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Back-up bewaarperiode
Zoals hierboven wordt beschreven, wordt Azure Cosmos DB duurt momentopnamen van uw gegevens om de vier uur en behoudt de laatste twee momentopnamen van elke partitie gedurende 30 dagen. Per onze nalevingsreglementen worden momentopnamen na 90 dagen permanent verwijderd.

Als u onderhouden van uw eigen momentopnamen wilt, kunt u het exporteren naar een JSON-optie gebruiken in de database van de Cosmos Azure [hulpprogramma voor gegevensmigratie](import-data.md#export-to-json-file) aanvullende back-ups plannen. 

## <a name="restoring-a-database-from-an-online-backup"></a>Een database terugzetten vanuit een online back-up
Als u de database of een verzameling per ongeluk verwijdert, kunt u [bestand een ondersteuningsticket](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) of [contact op met ondersteuning voor Azure](https://azure.microsoft.com/support/options/) de gegevens van de laatste automatische back-up wilt terugzetten. Als u uw database terugzetten vanwege beschadigingsprobleem gegevens wilt, Zie [afhandeling van gegevensbeschadiging](#handling-data-corruption) als u aanvullende stappen uitvoeren om te voorkomen dat de beschadigde gegevens van de back-ups vocht nodig. Voor een specifieke momentopname van de back-up moet worden hersteld, vereist Cosmos DB dat de gegevens voor de duur van de back-cyclus voor het die momentopname beschikbaar is.

## <a name="handling-data-corruption"></a>Beschadigde gegevens verwerken
Azure Cosmos DB behoudt de laatste twee back-ups van elke partitie in het systeem. Dit model werkt uitstekend wanneer een container (verzameling van documenten, grafiek, tabel) of een database per ongeluk worden verwijderd omdat een van de laatste versies kan worden hersteld. Echter, in het geval wanneer wanneer gebruikers leiden een probleem met de beschadiging van gegevens tot kunnen, Azure Cosmos DB mogelijk niet bewust zijn van de gegevens beschadigd en is het mogelijk de beschadiging van de back-ups mogelijk hebben gepenetreerd. Zo snel is beschadigd, moet u de beschadigde container (graph-verzameling/tabelnaam) verwijderen zodat back-ups worden beveiligd met beschadigde gegevens wordt overschreven. Omdat de laatste back-up kan vier uur oud is, kunt gebruikmaken van de gebruiker [wijzigen van de feed](change-feed.md) vastleggen en opslaan van de laatste vier uur waard van gegevens voor het verwijderen van de container.

## <a name="next-steps"></a>Volgende stappen

Als u wilt repliceren uw database in meerdere datacenters, Zie [distribueren van uw gegevens globaal met Cosmos DB](distribute-data-globally.md). 

Bestand contact opnemen met ondersteuning van Azure [bestand een ticket vanuit de Azure-portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

