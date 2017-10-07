---
title: 'Versleuteling van de database in rust: Azure Cosmos DB | Microsoft Docs'
description: Meer informatie over hoe Azure Cosmos DB standaard codering van alle gegevens biedt.
services: cosmos-db
author: voellm
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 99725c52-d7ca-4bfa-888b-19b1569754d3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: voellm
ms.openlocfilehash: d52d55fe45fdd18394166ec7ccd6e46e8f8f434b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-encryption-at-rest"></a>Versleuteling van Azure DB Cosmos-database in rust

Codering in rust is een wachtwoordzin die meestal toohello versleuteling van gegevens op opslagapparaten met niet-vluchtige, verwijst zoals Solid-State stations (SSD's) en harde schijven (HDD's). De primaire databases cosmos DB opgeslagen op SSD's. De mediabijlagen en de back-ups worden opgeslagen in Azure Blob-opslag is doorgaans een back-up door HDD's. Hallo-versie van versleuteling in rust voor Cosmos DB, worden alle databases, mediabijlagen en back-ups versleuteld. Uw gegevens nu in transit versleuteld (via Hallo netwerk) en at-rest (niet-vluchtige opslag), zodat u end-to-end-versleuteling.

Als een PaaS-service DB Cosmos heel eenvoudig toouse is. Omdat alle gebruikersgegevens zijn opgeslagen in de DB Cosmos is versleuteld in rust en bij transport, hebt u geen tootake geen actie. Een andere manier tooput dit is dat versleuteling-at rest 'op' standaard is. Er zijn geen tooturn besturingselementen het in- of uitschakelen. We leveren deze functie terwijl we toomeet blijven onze [beschikbaarheid en prestaties van SLA's](https://azure.microsoft.com/support/legal/sla/cosmos-db).

## <a name="implement-encryption-at-rest"></a>Codering in rust implementeren

Codering in rust wordt geïmplementeerd met behulp van een aantal beveiligingstechnologieën, met inbegrip van beveiligde sleutel opslagsystemen, gecodeerde netwerken en cryptografische API's. Systemen die gegevens verwerken en ontsleuteld hebben toocommunicate voor systemen die sleutels beheren. Hallo diagram ziet u hoe de opslag van versleutelde gegevens en Hallo beheer van sleutels wordt gescheiden. 

![Diagram ontwerpen](./media/database-encryption-at-rest/design-diagram.png)

Hallo-basisstroom van een gebruikersaanvraag is als volgt:
- Hallo-gebruikersaccount voor database wordt gemaakt gereed en opslagsleutels worden opgehaald via een aanvraag toohello Management Service Resource Provider.
- Een gebruiker maakt een verbinding tooCosmos DB via HTTPS/secure transport. (Hallo SDK's abstracte Hallo details).
- Hallo gebruiker verzendt een JSON-document toobe opgeslagen via Hallo beveiligde verbinding eerder hebt gemaakt.
- Hallo JSON-document wordt geïndexeerd tenzij Hallo gebruiker heeft uitgeschakeld indexeren.
- Zowel de Hallo JSON-document als de indexgegevens zijn toosecure opslag geschreven.
- Periodiek gegevens lezen uit Hallo veilige opslag en een back-up toohello Azure versleutelde Bloblarchief.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="q-how-much-more-does-azure-storage-cost-if-storage-service-encryption-is-enabled"></a>V: hoe veel meer kost Azure Storage als versleuteling van opslag-Service is ingeschakeld?
A: Er is geen extra kosten.

### <a name="q-who-manages-hello-encryption-keys"></a>V: die Hallo versleutelingssleutels beheert?
A: Hallo sleutels worden beheerd door Microsoft.

### <a name="q-how-often-are-encryption-keys-rotated"></a>V: hoe vaak worden versleutelingssleutels gedraaid?
A: Microsoft heeft een set van interne richtlijnen voor codering sleutel worden gedraaid dat volgt op Cosmos-DB. Hallo-specifieke richtlijnen worden niet gepubliceerd. Microsoft Hallo publiceren [Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx), die is gezien als een subset van interne richtlijnen en aanbevolen procedures voor nuttig is voor ontwikkelaars.

### <a name="q-can-i-use-my-own-encryption-keys"></a>V: kan ik mijn eigen versleutelingssleutels gebruiken?
A: cosmos DB is een PaaS-service en we harde tookeep Hallo service eenvoudig toouse gewerkt. Ons opgevallen dat deze vraag is vaak gevraagd als een vraag proxy voor een nalevingsvereiste zoals PCI-DSS voldoen. Als onderdeel van het bouwen van deze functie gewerkt we met naleving auditors tooensure dat klanten die gebruikmaken van de Cosmos-DB voldoen aan de vereisten zonder Hallo nodig toomanage sleutels zelf.
Als gevolg hiervan wordt op dit moment bieden geen gebruikers Hallo optie tooburden zelf met Sleutelbeheer.

### <a name="q-what-regions-have-encryption-turned-on"></a>V: wat regio's hebt u versleuteling is ingeschakeld?
A: alle regio's van Azure Cosmos DB hebben versleuteling ingeschakeld voor alle gebruikersgegevens.

### <a name="q-does-encryption-affect-hello-performance-latency-and-throughput-slas"></a>V: versleuteling beïnvloedt Hallo prestaties latentie en doorvoer Sla's?
A: Er is geen gevolgen of wijzigingen toohello prestaties Sla's nu versleuteling in rust is ingeschakeld voor alle bestaande en nieuwe accounts. U vindt meer op Hallo [SLA voor Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db) toosee Hallo nieuwste garanties pagina.

### <a name="q-does-hello-local-emulator-support-encryption-at-rest"></a>V: Hallo lokale emulator ondersteunt de versleuteling in rust?
A: Hallo-emulator is een zelfstandig hulpprogramma dat ontwikkelen en testen en gebruikt geen Hallo key management services die Hallo beheerde Cosmos-DB-service wordt gebruikt. Onze aanbeveling is tooenable BitLocker op stations waar u gevoelige emulator testgegevens opslaat. Hallo [emulator ondersteunt veranderende Hallo standaard gegevensmap](local-emulator.md) of via een bekende locatie.

## <a name="next-steps"></a>Volgende stappen

Zie voor een overzicht van de Cosmos-DB beveiligings- en de laatste verbeteringen Hallo [Azure Cosmos DB databasebeveiliging](database-security.md).
Zie voor meer informatie over Microsoft certificeringen Hallo [Azure Vertrouwenscentrum](https://azure.microsoft.com/en-us/support/trust-center/).
