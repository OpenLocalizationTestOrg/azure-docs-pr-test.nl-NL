---
title: "AAA 'Prijscategorieën in Azure-Database voor PostgreSQL'"
description: "Prijscategorieën in Azure PostgreSQL-Database"
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.custom: mvc
ms.service: postgresql
ms.topic: article
ms.date: 05/31/2017
ms.openlocfilehash: f10389dd2ad1ff04e83b02786a407c10140a007b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-options-and-performance-understand-whats-available-in-each-pricing-tier"></a>Azure-Database voor PostgreSQL-opties en prestaties: inzicht in wat er beschikbaar is in elke prijscategorie
Wanneer u een Azure-Database voor PostgreSQL-server maakt, besluit u over drie belangrijkste keuzes tooconfigure Hallo resources toegewezen voor die server. Deze keuzes invloed hebben op Hallo prestaties en schaalbaarheid van Hallo-server.
- Prijscategorie
- Rekeneenheden
- Storage (GB)

Elke prijscategorie heeft een bereik van de prestaties niveaus (Compute Units) toochoose uit, afhankelijk van uw werkbelastingen. Hogere prestaties bieden aanvullende bronnen voor uw server ontworpen toodeliver hogere doorvoer. U kunt het prestatieniveau van Hallo server binnen een prijscategorie met vrijwel geen uitvaltijd voor toepassingen wijzigen.

> [!IMPORTANT]
> Tijdens het Hallo-service zich in de openbare preview, is er geen een gegarandeerde Service Level Agreement (SLA).

U kunt een of meerdere databases hebben binnen een Azure-Database voor PostgreSQL-server. U kunt kiezen toocreate een individuele database per server tooutilize alle Hallo resources of meerdere databases tooshare Hallo resources maken. 

## <a name="choose-a-pricing-tier"></a>Een prijscategorie kiezen
In de preview, biedt Azure Database voor PostgreSQL twee Prijscategorieën: Basic en Standard. Premium-laag is nog niet beschikbaar, maar wordt binnenkort beschikbaar. 

Hallo bevat volgende tabel voorbeelden van Hallo prijzen lagen die het meest geschikt voor werklasten met verschillende groepen van toepassingen.

| Prijscategorie | Beoogde workloads |
| :----------- | :----------------|
| Basic | Het meest geschikt voor kleine werkbelastingen waarvoor schaalbare berekeningen en opslag zonder IOPS garanderen. Voorbeelden zijn onder meer servers die worden gebruikt voor ontwikkeling of tests of kleinschalige, onregelmatig gebruikte toepassingen. |
| Standard | Ga-toooption voor cloud Hallo toepassingen die IOP's moeten met hoge doorvoer garanderen. Voorbeelden zijn web of analytische toepassingen. |
| Premium | Het meest geschikt voor werklasten die lage latentie voor i/o- en moeten. Biedt de beste ondersteuning Hallo voor veel gelijktijdige gebruikers. Van toepassing toodatabases die bedrijfskritieke toepassingen ondersteunen.<br />Hallo Premium-prijscategorie is niet beschikbaar in preview. |

toodecide voor een prijsinformatie trapsgewijs door vast te stellen als uw werkbelasting een garantie IOPS moet opnieuw opstarten. Als dit het geval is, gebruikt u de Standard-prijscategorie.

| **Functies van de lagen prijzen** | **Basic** | **Standard** |
| :------------------------ | :-------- | :----------- |
| Maximale Compute-eenheden | 100 | 800 | 
| Maximale totale opslagruimte | 1 TB | 1 TB | 
| IOPS-garantie van opslag | N.v.t. | Ja | 
| Maximale opslag IOP 's | N.v.t. | 3.000 | 
| De back-up bewaarperiode database | 7 dagen | 35 dagen | 

Tijdens een tijdsbestek van Hallo preview, u de prijscategorie niet wijzigen zodra Hallo-server is gemaakt. In toekomstige hello, wordt deze mogelijk tooupgrade of downgraden van een server uit één laag tooanother prijscategorie.

## <a name="understand-hello-price"></a>Hallo prijs begrijpen
Wanneer u een nieuwe Azure-Database maken voor PostgreSQL binnen Hallo [Azure Portal](https://portal.azure.com/#create/Microsoft.PostgreSQLServer), klikt u op Hallo **prijscategorie** blade en Hallo maandelijkse kosten worden weergegeven op basis van Hallo-opties die u hebt geselecteerd. Als u niet een Azure-abonnement hebt, gebruikt u hello Azure prijscategorie Rekenmachine tooget een geschatte prijs. Bezoek Hallo [Azure prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/) website, klikt u vervolgens op **items toevoegen**, vouw Hallo **Databases** categorie, en kies **Azure Database voor PostgreSQL** toocustomize Hallo opties.

## <a name="choose-a-performance-level-compute-units"></a>Kies een prestatieniveau (Compute eenheden)
Als u Hallo prijscategorie voor uw Azure-Database voor PostgreSQL-server hebt vastgesteld, bent u klaar toodetermine Hallo prestatieniveau door Hallo aantal Compute eenheden nodig te selecteren. Een goed uitgangspunt is 200 of 400 Compute-eenheden voor toepassingen die hoger gelijktijdigheid van de gebruiker nodig voor hun web of analytische workloads en incrementeel indien nodig aanpassen. 

COMPUTE eenheden zijn een meting van CPU-verwerking doorvoer die gegarandeerd toobe beschikbaar tooa één Azure-Database voor PostgreSQL-server. Een Compute-eenheid is een gecombineerde meting van CPU en geheugenbronnen.  Zie voor meer informatie [waarin wordt uitgelegd Compute-eenheden](concepts-compute-unit-and-storage.md)

### <a name="basic-pricing-tier-performance-levels"></a>Basic prijscategorie laag prestatieniveaus:

| **Prestatieniveau** | **50** | **100** |
| :-------------------- | :----- | :------ |
| Maximale Compute-eenheden | 50 | 100 |
| Opgenomen opslaggrootte | 50 GB | 50 GB |
| Grootte van de opslagruimte voor de maximale\* | 1 TB | 1 TB |

### <a name="standard-pricing-tier-performance-levels"></a>Standaard prijscategorie laag prestatieniveaus:

| **Prestatieniveau** | **100** | **200** | **400** | **800** |
| :-------------------- | :------ | :------ | :------ | :------ |
| Maximale Compute-eenheden | 100 | 200 | 400 | 800 |
| Opgenomen opslaggrootte en ingerichte IOP 's | 125 GB<br/> 375 IOP 'S | 125 GB<br/> 375 IOP 'S | 125 GB<br/> 375 IOP 'S | 125 GB<br/> 375 IOP 'S |
| Grootte van de opslagruimte voor de maximale\* | 1 TB | 1 TB | 1 TB | 1 TB |
| Server voor max. IOP's ingericht | 3000 IOP 'S | 3000 IOP 'S | 3000 IOP 'S | 3000 IOP 'S |
| Server voor max. IOP's per GB ingericht | Vaste 3 IOP's per GB | Vaste 3 IOP's per GB | Vaste 3 IOP's per GB | Vaste 3 IOP's per GB |

\*Grootte van de opslagruimte voor de maximale verwijst toohello maximum ingerichte opslagruimte voor uw server.

## <a name="storage"></a>Storage 
Hallo-opslagconfiguratie definieert Hallo hoeveelheid opslag capaciteit beschikbaar tooan Azure Database voor PostgreSQL-server. Hallo opslag wordt gebruikt door Hallo service omvat Hallo-databasebestanden en transactielogboeken Hallo PostgreSQL server-Logboeken. Overweeg Hallo grootte van de opslag die nodig is toohost uw databases en Hallo prestatie-eisen (IOPS) bij het selecteren van Hallo opslagconfiguratie.

Sommige opslagcapaciteit is ten minste opgenomen met elke prijscategorie, vermeld in de voorgaande tabel staan als 'Opgenomen opslaggrootte.' Hallo Extra opslagcapaciteit kan worden toegevoegd wanneer het Hallo-server is gemaakt, in stappen van 125 GB toohello maximale toegestane opslagruimte. Hallo extra opslagcapaciteit kan onafhankelijk van Hallo eenheden Compute-configuratie worden geconfigureerd. Hallo prijswijzigingen die zijn gebaseerd op Hallo en de hoeveelheid opslagruimte die zijn geselecteerd.

Hallo IOPS configuratie in elke prestatieniveau verbindt toohello prijscategorie en de grootte van de opslagruimte Hallo gekozen. Laag Basic biedt geen garantie van een IOPS. Binnen Hallo standaard prijscategorie, Hallo IOPS proportioneel toomaximum opslaggrootte in een vaste verhouding van 3:1. Hallo opgenomen opslag van 125 GB garanties met betrekking tot 375 ingericht IOP's, elk met een i/o-grootte van up too256 KB. U kunt extra opslagruimte van too1 TB maximum, tooguarantee 3000 ingericht IOPS.

Monitor Hallo metrische gegevens grafiek in hello Azure portal- of schrijfbewerking Azure CLI-opdrachten toomeasure Hallo verbruik van opslag en IOP's. Relevante meetgegevens toomonitor zijn opslaglimiet bereikt, opslagpercentage opslag gebruikt en i/o-procent.

>[!IMPORTANT]
> In de preview, Hallo hoeveelheid opslag op Hallo tijd wanneer Hallo-server wordt gemaakt te kiezen. Wijzigen van de grootte van de opslagruimte op een bestaande server Hallo is nog niet ondersteund. 

## <a name="scaling-a-server-up-or-down"></a>Een server schaal omhoog of omlaag
U wordt in eerste instantie Hallo prijscategorie en prestatieniveau prijzen wanneer u uw Azure-Database voor PostgreSQL maakt. Later kunt u Hallo Compute eenheden omhoog of omlaag dynamisch, binnen het bereik van Hallo Hallo dezelfde schalen prijscategorie. In hello Azure-portal, schuif Hallo Compute-eenheden op van de server Hallo prijzen laag blade of het script door dit voorbeeld te volgen: [bewaken en schalen één PostgreSQL-server met Azure CLI](scripts/sample-scale-server-up-or-down.md)

Hallo Compute eenheden schalen gebeurt onafhankelijk van de maximale opslaggrootte Hallo die u hebt gekozen.

Achter de schermen hello, wijzigen van Hallo prestatieniveau van een database maakt een replica van de oorspronkelijke database Hallo op Hallo nieuwe prestatieniveau en vervolgens wordt de replica toohello overgeschakeld verbindingen. Gegevens niet verloren tijdens dit proces. Tijdens het Hallo korte ogenblikken wanneer we toohello replica overgeschakeld verbindingen toohello database uitgeschakeld, zodat sommige transacties tijdens de vlucht kunnen worden teruggedraaid. Deze tijdsduur varieert, maar is gemiddeld korter dan 4 seconden en in meer dan 99% van de gevallen minder dan 30 seconden. Als er grote aantallen transacties tijdens de vlucht op Hallo momenteel verbindingen zijn uitgeschakeld, wordt dit venster mogelijk ook langer.

Hallo duur van Hallo gehele scale proces, is afhankelijk van zowel de Hallo grootte en de prijscategorie van Hallo server vóór en na Hallo wijzigen. Bijvoorbeeld, voltooi een server die Compute eenheden wordt gewijzigd in Hallo standaard prijscategorie, binnen enkele minuten. Eigenschappen van nieuwe Hallo voor Hallo-server worden niet toegepast totdat Hallo wijzigingen voltooid zijn.

## <a name="next-steps"></a>Volgende stappen
- Zie voor meer informatie over de Compute-eenheden [waarin wordt uitgelegd Compute-eenheden](concepts-compute-unit-and-storage.md)
- Meer informatie over hoe te[bewaken en schalen één PostgreSQL-server met Azure CLI](scripts/sample-scale-server-up-or-down.md)
