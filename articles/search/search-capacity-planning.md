---
title: planning voor Azure Search aaaCapacity | Microsoft Docs
description: Partitie en replica computerbronnen in Azure Search, waarbij een prijs van elke resource in factureerbare search-eenheden aanpassen.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 1dc16afe-56f9-439d-8874-1733ae1a2b74
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 02/08/2017
ms.author: heidist
ms.openlocfilehash: 4bbbb929a36b932ea7af12e494ca095d98b9005e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-resource-levels-for-query-and-indexing-workloads-in-azure-search"></a>Resource schaalniveaus voor query's en workloads in Azure Search indexeren
Nadat u [Kies een prijscategorie](search-sku-tier.md) en [inrichten van een zoekservice](search-create-service-portal.md), de volgende stap Hallo is toooptionally toename Hallo aantal replica's of partities die worden gebruikt door uw service. Elke laag biedt een vast aantal facturering eenheden. Dit artikel wordt uitgelegd hoe tooallocate die tooachieve eenheden een optimale configuratie die door een compromis tussen uw vereisten voor het uitvoeren van de query te indexeren en opslag.

Resourceconfiguratie is beschikbaar bij het instellen van een service op Hallo [basisstaffel](http://aka.ms/azuresearchbasic) of een van de Hallo [standaard lagen](search-limits-quotas-capacity.md). Voor factureerbare services op deze lagen capaciteit is aangeschaft per *zoekeenheden* (SUs) waar elke partitie en replica telt als een SU. 

Gebruik minder SUs resulteert in een proportioneel lagere factuur. Facturering geldt voor zolang Hallo-service is ingesteld. Als u een service, de enige manier Hallo tooavoid facturering op Hallo service verwijderen en vervolgens opnieuw maken wanneer dat nodig is tijdelijk niet gebruikt.

> [!Note]
> Verwijderen van een service, worden alle gegevens verwijderd. Er is geen faciliteit in Azure Search voor back-up en herstellen van zoekgegevens persistent. een bestaande index op een nieuwe service tooredeploy, moet u Hallo programma gebruikt toocreate uitvoeren en oorspronkelijk laden. 

## <a name="terminology-partitions-and-replicas"></a>Terminologie: partities en replica 's
Partities en replica's zijn primaire Hallo-resources die back-search-service.

| Resource | Definitie |
|----------|------------|
|*Partities* | Voorziet index opslag en i/o-lees-/ schrijfbewerkingen (bijvoorbeeld wanneer opnieuw samenstellen of een index te vernieuwen).|
|*Replica 's* | Exemplaren van de service voor zoeken in hello, voornamelijk tooload saldo querybewerkingen gebruikt. Elke replica altijd fungeert als host voor één exemplaar van een index. Als u 12 replica's hebt, hebt u 12 kopieën van elke index op Hallo service geladen.|

> [!NOTE]
> Er is geen manier toodirectly bewerken of te beheren welke indexen worden uitgevoerd op een replica. Één exemplaar van elke index op elke replica maakt deel uit van de architectuur van Hallo-service.
>

## <a name="how-tooallocate-partitions-and-replicas"></a>Hoe tooallocate partities en replica's
Een service in Azure Search is in eerste instantie een minimumniveau aan resources die bestaan uit één partitie en één replica toegewezen. Voor de lagen die dit ondersteunen, kunt u stapsgewijs rekenbronnen aanpassen door partities verhogen als u meer opslagruimte en i/o-nodig, of Voeg meer replica's van grotere volumes van de query of betere prestaties. Een enkele service moet voldoende bronnen toohandle hebben alle werkbelastingen (indexeren en query's). U kunt werkbelastingen tussen meerdere services kan geen onderverdelen.

tooincrease of wijzig Hallo-toewijzing van replica's en partities, wordt u aangeraden hello Azure-portal. Hallo-portal wordt afgedwongen beperkingen met betrekking tot toegestane combinaties die onder bovengrenzen:

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) en selecteer Hallo search-service.
2. In **instellingen**Open Hallo **Scale** blade en gebruik Hallo schuifregelaars tooincrease of Hallo aantal partities en replica's verminderen.

Als u een script of code gebaseerde inrichting benadering vereist, Hallo [Management REST API](https://msdn.microsoft.com/library/azure/dn832687.aspx) is een alternatieve toohello-portal.

Meestal moeten zoektoepassingen meer replica's dan partities, vooral wanneer Hallo servicebewerkingen zijn gericht op de query-werkbelastingen. sectie op Hallo [hoge beschikbaarheid](#HA) wordt uitgelegd waarom.

> [!NOTE]
> Nadat u een service is geconfigureerd, kan niet worden bijgewerkt tooa hogere SKU. U moet een search-service op de nieuwe laag Hallo toocreate en laad de indexen opnieuw. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor hulp bij het inrichten van de service.
>
>

<a id="HA"></a>

## <a name="high-availability"></a>Hoge beschikbaarheid
Omdat deze eenvoudig is en snel relatief tooscale up, in het algemeen wordt aangeraden dat u met één partitie en één begint of twee replica's en schaal omhoog als volumes query bouwen. Voor veel services op Hallo Basic of S1 lagen biedt één partitie voldoende opslag en i/o-(op 15 miljoen documenten per partitie).

Query-workloads uitvoeren voornamelijk op de replica's. Als u meer doorvoer of hoge beschikbaarheid nodig hebt, moet u waarschijnlijk meer replica's.

Algemene aanbevelingen voor hoge beschikbaarheid zijn:

* Twee replica's voor hoge beschikbaarheid van alleen-lezen werkbelastingen (query's)
* Drie of meer replica's voor hoge beschikbaarheid van lezen/schrijven-werkbelastingen (query's plus indexeren als afzonderlijke documenten worden toegevoegd, bijgewerkt of verwijderd)

Serviceovereenkomsten (SLA) voor Azure Search is gericht op querybewerkingen en op index-updates die bestaan uit toevoegen, bijwerken of verwijderen van documenten.

### <a name="index-availability-during-a-rebuild"></a>Index beschikbaarheid tijdens het opnieuw opbouwen

Hoge beschikbaarheid voor Azure Search geldt tooqueries en index updates die niet opnieuw opbouwen van een index. Als u een veld verwijderen, wijzigen van een type of wijzig de naam van een veld, moet u toorebuild Hallo index. toorebuild hello index, moet u Hallo index en Hallo gegevens opnieuw laden Hallo-index opnieuw maken.

> [!NOTE]
> U kunt nieuwe velden tooan Azure Search-index zonder het Hallo-index opnieuw opbouwen toevoegen. Hallo-waarde van het nieuwe veld Hallo is null voor alle documenten al in het Hallo-index.

toomaintain index beschikbaarheid tijdens het opnieuw opbouwen, moet u een kopie van het Hallo-index met een andere naam hebben op Hallo dezelfde service, of een kopie van Hallo index Hello dezelfde naam op een andere service en geef vervolgens omleiding of failover logica in uw code.

## <a name="disaster-recovery"></a>Herstel na noodgevallen
Er is momenteel geen ingebouwde methode voor herstel na noodgevallen. Toe te voegen partities of replica's zijn Hallo verkeerde strategie voor disaster recovery doelstellingen. de meest voorkomende benadering Hallo is tooadd redundantie op Hallo serviceniveau door het instellen van een tweede service voor zoeken in een andere regio. Net als bij beschikbaarheid tijdens het opnieuw opbouwen van een index, Hallo omleiding of failoverlogica moet afkomstig zijn van uw code.

## <a name="increase-query-performance-with-replicas"></a>Prestaties van query's met replica's vergroten
Latentie van query is een indicatie dat de replica's meer nodig zijn. Eerste stap bij het verbeteren van de prestaties van query's is in het algemeen tooadd meer van deze resource. Als u replica's toevoegt, extra exemplaren van Hallo index online toosupport groter query werkbelastingen worden gebracht en tooload saldo Hallo verzoeken via Hallo meerdere replica's.

Kan geen wij harde maakt een schatting op query's per seconde (QPS): query prestaties, hangt af van de complexiteit Hallo Hallo query en concurrerende werkbelastingen. Gemiddeld een replica basis-of S1 SKU's 15 QPS kunt onderhouden, maar de doorvoer kan hoger of lager, afhankelijk van de complexiteit van de query (meervoudige query's zijn meer complexe) en netwerklatentie. Het is ook belangrijk toorecognize dat hoewel voor het toevoegen van replica's wordt definitief toevoegen schaal en prestaties, Hallo resultaat is niet strikt lineaire: drie doorvoer wordt niet gegarandeerd drie replica's toe te voegen.

Zie toolearn over QPS, met inbegrip van strategieën voor het schatten van QPS voor uw werkbelastingen [uw zoekservice beheren](search-manage.md).

## <a name="increase-indexing-performance-with-partitions"></a>De prestaties van indexering met partities
Zoektoepassingen waarvoor near realtime gegevens vernieuwen moet proportioneel meer partities dan replica's. Lees-/ schrijfbewerkingen toe te voegen partities worden verspreid over een groter aantal rekenresources. Dit ook biedt u meer schijfruimte voor het opslaan van aanvullende indexen en documenten.

Grotere indexen duren tooquery langer. Als zodanig kan gebeuren dat elke incrementele stijging van de partities een kleinere maar evenredig toename van replica's vereist. Hallo complexiteit van uw query's en het volume van de query wordt factor in hoe snel de queryuitvoering rond is ingeschakeld.

## <a name="basic-tier-partition-and-replica-combinations"></a>Basic-laag: combinaties van partitie en replica
Een Basic service kunt precies één partitie hebben en tot toothree replica's, voor een maximumlimiet van drie SUs. Hallo alleen aanpasbare bron is replica's. U moet minimaal twee replica's voor hoge beschikbaarheid op query's.

<a id="chart"></a>

## <a name="standard-tiers-partition-and-replica-combinations"></a>Standaard lagen: combinaties van partitie en replica
Deze tabel ziet u Hallo SUs vereist toosupport combinaties van replica's en partities, onderwerp toohello 36 SU limiet voor alle standaard lagen.

|   | **1 partitie** | **2 partities** | **3 partities** | **4 partities** | **6 partities** | **12 partities** |
| --- | --- | --- | --- | --- | --- | --- |
| **1 replica** |1 SU |2 SU |3 SU |4 SU |6 SU |12 SU |
| **2 replica 's** |2 SU |4 SU |6 SU |8 SU |12 SU |24 SU |
| **3 replica 's** |3 SU |6 SU |9 SU |12 SU |18 SU |36 SU |
| **4 replica 's** |4 SU |8 SU |12 SU |16 SU |24 SU |N.v.t. |
| **5 replica 's** |5 SU |10 SU |15 SU |20 SU |30 SU |N.v.t. |
| **6 replica 's** |6 SU |12 SU |18 SU |24 SU |36 SU |N.v.t. |
| **12 replica 's** |12 SU |24 SU |36 SU |N.v.t. |N.v.t. |N.v.t. |

SUs-prijzen en capaciteit zijn in detail uitgelegd op Hallo Azure-website. Zie voor meer informatie [prijsinformatie](https://azure.microsoft.com/pricing/details/search/).

> [!NOTE]
> Hallo aantal replica's en partities gelijkmatig wordt verdeeld in 12 (specifiek, 1, 2, 3, 4, 6, 12). Dit is omdat elke index Azure Search vooraf in 12 shards verdeelt zodat deze in gedeelten gelijk voor alle partities kan worden verspreid. Als uw service drie partities heeft en u een index maakt, wordt elke partitie vier shards van Hallo index bevatten. Hoe Azure Search shards een index is een implementatie-informatie, de onderwerp toochange in toekomstige releases. Hoewel Hallo nummer 12 vandaag de dag, kunt u die number tooalways liggen 12 Hallo toekomstige mag niet verwacht.
>
>

## <a name="billing-formula-for-replica-and-partition-resources"></a>De formule facturering voor replica- en partitie bronnen
Hallo formule voor het berekenen van hoeveel SUs worden gebruikt voor specifieke combinaties is Hallo product van replica's en -partities bevat, of (R X P = SU). Bijvoorbeeld drie replica's vermenigvuldigd met drie partities wordt in rekening gebracht als negen SUs.

Kosten per SU wordt bepaald door het Hallo-laag, met een lagere per eenheid facturerings frequentie voor Basic dan voor standaard. Voor elke laag kan worden gevonden op classificeert [prijsinformatie](https://azure.microsoft.com/pricing/details/search/).
