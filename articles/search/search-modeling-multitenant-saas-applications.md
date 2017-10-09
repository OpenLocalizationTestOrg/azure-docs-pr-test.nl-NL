---
title: aaaModeling Multitenancy in Azure Search | Microsoft Docs
description: Meer informatie over algemene ontwerppatronen voor multitenant SaaS-toepassingen tijdens het gebruik van Azure Search.
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Ontwerppatronen voor multitenant SaaS-toepassingen en Azure Search
Een multitenant-toepassing is een die Hallo biedt dezelfde mogelijkheden en services tooany aantal tenants die niet zien of delen van gegevens van een andere tenant Hallo. Dit document wordt besproken tenant isolatie strategieën voor multitenant toepassingen die zijn gebouwd met Azure Search.

## <a name="azure-search-concepts"></a>Azure Search-concepten
Als een oplossing zoeken as a service kunt Azure Search ontwikkelaars tooadd uitgebreide zoeken tooapplications optreedt zonder eventuele infrastructuurbeheer of u een expert in de zoekopdracht. Gegevens geüpload toohello service en vervolgens in Hallo cloud worden opgeslagen. Met behulp van eenvoudige aanvragen toohello Azure Search API kunnen Hallo gegevens vervolgens worden gewijzigd en doorzocht. Een overzicht van Hallo-service kan worden gevonden in [in dit artikel](http://aka.ms/whatisazsearch). Voordat u ontwerppatronen, is het belangrijk toounderstand enkele concepten die in Azure Search.

### <a name="search-services-indexes-fields-and-documents"></a>Search-services, indexen, velden en -documenten
Bij gebruik van Azure Search is een lid van tooa *zoekservice*. Omdat de gegevens geüploade tooAzure zoeken, wordt opgeslagen in een *index* binnen Hallo search-service. Er is een aantal indexen binnen een enkele service. toouse hello bekend concepten van databases, Hallo search-service kan worden vergeleken tooa database terwijl Hallo indexen in een service vergeleken tootables binnen een database worden kunnen.

Elke index binnen een search-service heeft een eigen schema, die wordt gedefinieerd door een aantal aanpasbare *velden*. Gegevens aan worden toegevoegd tooan Azure Search-index in de vorm Hallo van afzonderlijke *documenten*. Elk document moet geüploade tooa bepaalde index en die index schema moet passen. Bij het zoeken van gegevens met behulp van Azure Search worden Hallo zoekopdracht in volledige tekst-query's worden uitgegeven op basis van een bepaalde index.  toocompare deze toothose concepten van een database, velden kunnen worden vergeleken toocolumns in een tabel en documenten kunnen worden vergeleken toorows.

### <a name="scalability"></a>Schaalbaarheid
Een Azure Search-service in Hallo standaard [prijscategorie](https://azure.microsoft.com/pricing/details/search/) in twee dimensies kunt schalen: opslag en beschikbaarheid.

* *Partities* tooincrease Hallo opslag van een search-service kan worden toegevoegd.
* *Replica's* tooa service tooincrease Hallo doorvoer van aanvragen die een search-service kan verwerken kunnen worden toegevoegd.

Partities en replica's op toevoegen en verwijderen kunt Hallo-capaciteit van Hallo search service toogrow met Hallo hoeveelheid gegevens en verkeer Hallo toepassing eisen. In volgorde voor een zoekopdracht service tooachieve lezen [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), hiervoor twee replica's. In volgorde voor een service-tooachieve een lezen / schrijven [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), drie replica's is vereist.

### <a name="service-and-index-limits-in-azure-search"></a>In Azure Search-service en de index limieten
Er zijn slechts enkele andere [Prijscategorieën](https://azure.microsoft.com/pricing/details/search/) in Azure Search elk Hallo lagen heeft verschillende [limieten en quota's](search-limits-quotas-capacity.md). Sommige van deze beperkingen zijn op Hallo serviceniveau, sommige zijn op Hallo index-niveau, en andere op Hallo partitie-niveau.

|  | Basic | Standard1 | Standard2 | Standard3 | HD Standard3 |
| --- | --- | --- | --- | --- | --- |
| Maximum aantal replica's per Service |3 |12 |12 |12 |12 |
| Maximum aantal partities per Service |1 |12 |12 |12 |1 |
| Maximum aantal Search-eenheden (replica's * partities) per Service |3 |36 |36 |36 |36 (maximaal 3 partities) |
| Maximum aantal documenten per Service |1 miljoen |180 miljoen |720 miljoen |1.4 miljard |600 miljoen |
| Maximale opslag per Service |2 GB |300 GB |1,2 TB |2,4 TB |600 GB |
| Maximum aantal documenten per partitie |1 miljoen |15 miljoen |60 miljoen |120 miljoen |200 miljoen |
| Maximale opslag per partitie |2 GB |25 GB |100 GB |200 GB |200 GB |
| Maximum aantal indexen per Service |5 |50 |200 |200 |3000 (maximaal 1000 indexen/partitie) |

#### <a name="s3-high-density"></a>S3 High-density '
Er is een optie voor Hallo hoge dichtheid (HD) modus is speciaal ontworpen voor multitenant scenario's in Azure-Search S3 prijscategorie. In veel gevallen is het nodig toosupport een groot aantal kleinere tenants onder een service voor eenmalige tooachieve Hallo voordelen van eenvoud en kostenbesparing.

S3 HD kunt u veel kleine indexen toobe die door de handel Hallo mogelijkheid tooscale uit indexen met partities voor Hallo mogelijkheid toohost meer indexen in een enkele service onder beheer van een enkele zoekservice Hallo ingepakt Hallo.

Concrete invulling te geven, kan een service S3 hebben tussen 1 en 200 indexen die samen too1.4 miljard documenten kunnen hosten. Een HD S3 op Hallo daarentegen kunnen afzonderlijke indexen tooonly too1 miljoen documenten gaat, maar deze kan omgaan met up too1000-indexen per partitie (omhoog too3000 per service) met een telling van de totale document van 200 miljoen per partitie (up too600 miljoen per service).

## <a name="considerations-for-multitenant-applications"></a>Overwegingen voor multitenant-toepassingen
Multitenant toepassingen moeten effectief distribueren resources tussen Hallo tenants behoud een zekere mate van privacy tussen Hallo verschillende tenants. Er zijn enkele overwegingen bij het ontwerpen van Hallo-architectuur voor een dergelijke toepassing:

* *Tenantisolatie:* Toepassingsontwikkelaars hoeven tootake passende maatregelen tooensure dat geen tenants hebt geverifieerd of toegang tot toohello gegevens van andere tenants ongewenste. Afgezien van Hallo perspectief van de privacy van gegevens vereisen tenant isolatie strategieën effectief beheer van gedeelde bronnen en bescherming tegen ruis neighbors.
* *Kosten van de resource cloud:* als met een andere toepassing softwareoplossingen kosten concurrerende als onderdeel van een multitenant-toepassing moeten blijven.
* *Gebruiksgemak Operations:* bij het ontwikkelen van een multitenant architectuur Hallo gevolgen voor de bewerkingen van de toepassing hello en complexiteit is een belangrijk aandachtspunt. Azure Search is een [SLA van 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Globale footprint:* Multitenant toepassingen wellicht tooeffectively dienst tenants die over de hele wereld Hallo worden gedistribueerd.
* *Schaalbaarheid:* toepassingsontwikkelaars moet tooconsider hoe ze in overeenstemming brengen tussen het onderhouden van een voldoende laag niveau van complexiteit bij de toepassing en Hallo toepassing tooscale ontwerpen met het aantal tenants en Hallo grootte van de gegevens van tenants en werkbelasting.

Azure Search biedt een aantal grenzen die de gegevens en de werkbelasting gebruikte tooisolate tenants worden kunnen.

## <a name="modeling-multitenancy-with-azure-search"></a>Multitenancy modellering met Azure Search
In geval van een multitenant scenario Hallo Hallo toepassingsontwikkelaar maakt gebruik van een of meer search-services en delen van hun tenants tussen services, indexen of beide. Azure Search heeft enkele algemene patronen bij het modelleren van een multitenant scenario:

1. *Index per tenant:* elke tenant heeft zijn eigen index binnen een search-service die wordt gedeeld met andere tenants.
2. *Service per tenant:* elke tenant heeft zijn eigen toegewezen Azure Search-service offering hoogste niveau van de scheiding van gegevens en werkbelasting.
3. *De combinatie van beide:* tenants grotere, meer actief zijn speciale services toegewezen terwijl kleinere tenants afzonderlijke indexen binnen gedeelde services zijn toegewezen.

## <a name="1-index-per-tenant"></a>1. Index per tenant
![Een portrayal van Hallo index per tenant model](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

In een model index per tenant innemen meerdere tenants één Azure Search-service waarbij elke tenant hun eigen index heeft.

Tenants bereiken gegevensisolatie, omdat alle aanvragen zoeken en document bewerkingen op het indexniveau van een in Azure Search worden uitgegeven. In de toepassingslaag Hallo is het Hallo nodig awareness toodirect Hallo verschillende tenants verkeer toohello juiste indexen tijdens ook het beheren van resources op Hallo serviceniveau in alle tenants.

Sleutelkenmerk van Hallo index per tenant model is de mogelijkheid Hallo Hallo toepassing developer toooversubscribe Hallo capaciteit van een search-service tussen van de toepassing hello tenants. Als Hallo tenants hebben een ongelijke verdeling van werkbelasting, Hallo optimale combinatie van tenants kunnen worden verdeeld over indexeert een zoekservice tooaccommodate een aantal zeer actieve, bronintensieve tenants terwijl tegelijkertijd een lange staart van minder actieve tenants. Hallo nadeel is onvermogen Hallo Hallo model toohandle situaties waarbij elke tenant gelijktijdig maximaal actief is.

Hallo index per tenant model Hallo basis vormt voor een model variabele kosten, waar een volledige Azure Search-service is gekocht vooraf en vervolgens gevuld met tenants. Hierdoor ongebruikte capaciteit toobe aangewezen voor proefabonnementen en gratis accounts.

Voor toepassingen met een globale footprint Hallo index per tenant model mogelijk niet Hallo meest efficiënt. Als een toepassing tenants worden gedistribueerd over Hallo wereld, is het mogelijk dat een afzonderlijke service nodig is voor elke regio die mogelijk kosten op elk van deze dupliceren.

Azure Search kunt u Hallo schaal van zowel afzonderlijke Hallo-indexen en Hallo kunt u het totale aantal indexen toogrow. Als een juiste prijzen laag hebt gekozen, partities en replica's kunnen worden toegevoegd toohello gehele search-service wanneer een afzonderlijke index in Hallo-service te groot in termen van opslag- of -verkeer.

Als het totale aantal indexen hello te groot voor één service heeft een andere service toobe ingericht tooaccommodate Hallo nieuwe tenants. Als indexen toobe verplaatst tussen de search-services hebt als nieuwe services worden toegevoegd, gegevens van de index Hallo Hallo toobe handmatig wordt gekopieerd van een index toohello andere heeft als de Azure Search staat niet toe dat een index toobe verplaatst.

## <a name="2-service-per-tenant"></a>2. Service per tenant
![Een portrayal van Hallo per servicetenant model](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

In een architectuur service per tenant heeft elke tenant een eigen search-service.

In dit model realiseert Hallo toepassing hello maximumniveau isolatieniveau voor de tenants. Elke service heeft toegewezen opslag en doorvoer voor het verwerken van zoekaanvraag, evenals een afzonderlijke API-sleutels.

Hallo per servicetenant model is een daadwerkelijke keuze voor toepassingen waarbij elke tenant heeft een groot footprint of Hallo werkbelasting variëren van tenant tootenant als bronnen worden niet gedeeld door verschillende tenants werkbelastingen.

Een service per tenant model biedt ook Hallo voordeel van een kostprijsmodel voorspelbare, vaste. Er is geen investeringen in een hele search-service tot er een tenant toofill is, echter Hallo kosten per tenant is hoger dan het model van een index per tenant.

Hallo-service per tenant model is een efficiënte keuze voor toepassingen met een globale footprint. Met geografisch verspreide tenants, is het eenvoudig toohave elke tenant-service in de juiste regio Hallo.

Hallo uitdagingen bij het schalen van dit patroon zich mogelijk aandienen wanneer individuele tenants langzamerhand hun service. Azure Search biedt momenteel geen ondersteuning voor upgraden Hallo prijscategorie van een service voor zoeken, zodat alle gegevens handmatig gekopieerd toobe tooa nieuwe service zou hebben.

## <a name="3-mixing-both-models"></a>3. De combinatie van beide modellen
Een ander patroon voor het modelleren van multitenancy is de combinatie van strategieën voor zowel de index per tenant en de service per tenant.

Door de combinatie van patronen Hallo twee grootste tenants van een toepassing in beslag kunnen nemen toegewezen services terwijl Hallo lang archiefeinde van minder actieve, kleinere tenants in beslag indexen in een gedeelde service nemen kan. Dit model zorgt ervoor dat de grootste tenants Hallo consistent hoge prestaties van de service Hallo terwijl tooprotect Hallo kleinere tenants vanaf elke ruis neighbors.

Implementeren van deze strategie afhankelijk prognose voorspellen welke tenants wordt een specifieke service ten opzichte van een index in een gedeelde service nodig is. Met Hallo nodig toomanage beide van deze multitenancy modellen verhoogt de complexiteit van de toepassing.

## <a name="achieving-even-finer-granularity"></a>Achieving zelfs weer specifieker
Hallo hierboven ontwerp patronen toomodel multitenant scenario's in Azure Search wordt ervan uitgegaan dat een uniform bereik, waarbij elke tenant een hele exemplaar van een toepassing is. Toepassingen kunnen echter soms verwerken veel kleinere bereiken.

Als service per tenant en index per tenant modellen niet voldoende kleine bereiken zijn, is het mogelijk toomodel een index tooachieve een zelfs fijner mate van granulatie.

toohave een enkele index zich anders gedragen voor andere client-eindpunten, een veld is toegevoegd tooan index waarmee wordt aangegeven dat een bepaalde waarde voor elke mogelijke client. Telkens wanneer een client roept Azure Search tooquery of wijzigen van een index, Hallo-code van de clienttoepassing Hallo geeft Hallo geschikte waarde op voor het veld met behulp van Azure-Search [filter](https://msdn.microsoft.com/library/azure/dn798921.aspx) mogelijkheden op het moment dat de query.

Deze methode kan worden gebruikt tooachieve functionaliteit van afzonderlijke gebruikersaccounts, afzonderlijke machtigingsniveaus en ook volledig afzonderlijke toepassingen.

> [!NOTE]
> Met Hallo benadering die hierboven worden beschreven tooconfigure een enkele index tooserve meerdere tenants is van invloed op Hallo relevantie van zoekresultaten. Zoeken relevantie scores zijn berekend in een bereik van de index-niveau, niet op tenantniveau-bereik, zodat alle huurders gegevens is opgenomen in de onderliggende statistieken Hallo relevantie scores zoals frequentie van de termijn.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Azure Search is een aantrekkelijke keuze voor veel toepassingen [voor meer informatie over mogelijkheden voor robuuste Hallo-service](http://aka.ms/whatisazsearch). Wanneer evalueren Hallo verschillende ontwerppatronen voor multitenant-toepassingen, overweeg dan het Hallo [verschillende Prijscategorieën](https://azure.microsoft.com/pricing/details/search/) en Hallo respectieve [Servicelimieten](search-limits-quotas-capacity.md) toobest Azure Search toofit aanpassen toepassingsworkloads en -architecturen van elke grootte.

Vragen over Azure Search en multitenant scenario's kunnen worden omgeleid tooazuresearch_contact@microsoft.com.

