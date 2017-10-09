---
title: beheer van de aaaService voor Azure Search in hello Azure-portal
description: Azure Search, een gehoste cloud search-service in Microsoft Azure met behulp van hello Azure-portal beheren.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: c87d1fdd-b3b8-4702-a753-6d7e29dbe0a2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/18/2017
ms.author: heidist
ms.openlocfilehash: 9bb33660d93e068e0f35b856cba0a41c92623644
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-administration-for-azure-search-in-hello-azure-portal"></a>Beheer van de service voor Azure Search in hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> * [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.management.search)
> * [Python](https://pypi.python.org/pypi/azure-mgmt-search/0.1.0)> 

Azure Search is een volledig beheerde, cloud-gebaseerde zoekservice gebruikt voor het bouwen van een uitgebreide zoekervaring in aangepaste apps. Dit artikel behandelt Hallo *service-beheer* taken die u in Hallo uitvoeren kunt [Azure-portal](https://portal.azure.com) voor een zoekservice die u al hebt ingericht. *Service-beheer* is een lichtgewicht standaard beperkt toohello taken te volgen:

* Beheren en beveiligen van toegang toohello *api-sleutels* gebruikt voor lees- of schrijftoegang tooyour-service.
* Servicecapaciteit door het wijzigen van Hallo toewijzing van partities en replica's aanpassen.
* Monitor Resourcegebruik, limieten voor relatieve toomaximum van de servicelaag.

**Niet binnen het bereik** 

*Inhoudsbeheer* (of index-management) verwijst toooperations zoals zoeken verkeer toounderstand query volume wordt geanalyseerd, detecteren die mensen termen zoekt en hoe zoekactie resultaten begeleiding klanten toospecific documenten in uw index. Zie voor meer informatie in dit opzicht [Search Traffic Analytics voor Azure Search](search-traffic-analytics.md).

*Query-prestaties* ook valt buiten bereik Hallo van dit artikel. Zie voor meer informatie [gebruiks- en metrische gegevens controleren](search-monitor-usage.md) en [prestaties en optimalisatie](search-performance-optimization.md).

*Upgrade* is niet een beheertaak. Omdat bronnen worden toegewezen wanneer Hallo-service is ingericht, vereist bewegende tooa andere tier een nieuwe service. Zie voor meer informatie [maken van een Azure Search-service](search-create-service-portal.md).

<a id="admin-rights"></a>

## <a name="administrator-rights"></a>Administrator-rechten
Het inrichten of buiten gebruik stellen Hallo-service zelf kan worden gedaan door de beheerder van de Azure-abonnement of CO-beheerder.

Binnen een service en heeft iedereen met toegang toohello service-URL en een admin api-sleutel lees-/ schrijftoegang toohello service. Lees-/ schrijftoegang biedt Hallo mogelijkheid tooadd, verwijderen of wijzigen van de server-objecten, met inbegrip van api-sleutels, indexen, indexeerfuncties, gegevensbronnen, schema's en roltoewijzingen geïmplementeerd via [RBAC gedefinieerde rollen](#rbac).

Alle gebruikersinteractie met Azure Search valt binnen een van deze modi: lezen-schrijven toegang toohello service (beheerdersrechten) of alleen-lezentoegang toohello service (query rechten). Zie voor meer informatie [Hallo api-sleutels beheren](#manage-keys).

<a id="sys-info"></a>

## <a name="set-rbac-roles-for-administrative-access"></a>RBAC-rollen voor beheerderstoegang instellen
Azure biedt een [globale op rollen gebaseerde verificatie model](../active-directory/role-based-access-control-configure.md) voor alle services die worden beheerd via het Hallo-portal of de Resource Manager-API's. Rollen eigenaar, bijdrager en lezer bepalen Hallo-niveau voor servicebeheer van Active Directory-gebruikers, groepen en -principals tooeach toegewezen beveiligingsrol. 

RBAC machtigingen bepalen voor Azure Search Hallo administratieve taken te volgen:

| Rol | Taak |
| --- | --- |
| Eigenaar |Maak of verwijder Hallo service of een object op Hallo-service, inclusief api-sleutels, indexen, indexeerfuncties, indexeerfunctie gegevensbronnen en indexeerfunctie schema's.<p>Bekijk de servicestatus, met inbegrip van aantallen en de opslaggrootte.<p>Toevoegen of verwijderen van lidmaatschap van de rol (alleen een eigenaar kunt rollidmaatschap beheren).<p>Abonnementbeheerders en eigenaren van de service kunt u de automatische lid zijn van Hallo eigenaars rol. |
| Inzender |Hetzelfde niveau van toegang als eigenaar, min RBAC rollen beheren. Bijvoorbeeld, een Inzender kunt weergeven en opnieuw genereren `api-key`, maar rollidmaatschappen niet wijzigen. |
| Lezer |De status en query sleutels service weergeven. Leden van deze rol kunnen de configuratie van de service niet wijzigen, noch kunnen ze administratorsleutels weergeven. |

Rollen ken geen toegang rechten toohello service-eindpunt. Search-servicebewerkingen, zoals beheer van de index, populatie van de index en query's op zoekgegevens, worden beheerd via api-sleutels, niet rollen. Zie voor meer informatie 'Autorisatie voor het beheer van versus gegevensbewerkingen' in [wat is er op rollen gebaseerde toegangsbeheer](../active-directory/role-based-access-control-what-is.md).

<a id="secure-keys"></a>
## <a name="logging-and-system-information"></a>Logboekregistratie en systeeminformatie
Azure Search maakt logboekbestanden voor een afzonderlijke service via de portal Hallo of programmatische interfaces niet beschikbaar. Op de basisstaffel hello en hoger bewaakt Microsoft alle Azure Search-services voor beschikbaarheid van 99,9% per serviceovereenkomsten (SLA). Als Hallo-service langzaam is of doorvoer van aanvragen onder SLA drempelwaarden valt, bekijk ondersteuningsteams Hallo logboek bestanden beschikbaar toothem en adres Hallo probleem.

U kunt informatie in de volgende manieren Hallo verkrijgen in termen van algemene informatie over uw service:

* In het Hallo-portal op Hallo servicedashboard via meldingen, eigenschappen en statusberichten.
* Met behulp van [PowerShell](search-manage-powershell.md) of Hallo [Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/) te[service-eigenschappen ophalen](https://docs.microsoft.com/rest/api/searchmanagement/services), of de status van het Resourcegebruik van de index.
* Via [zoeken traffic analytics](search-traffic-analytics.md), zoals eerder is aangegeven.

<a id="manage-keys"></a>

## <a name="manage-api-keys"></a>Api-sleutels beheren
Alle aanvragen tooa search-service moet een api-sleutel die is gegenereerd specifiek voor uw service. Deze api-sleutel is Hallo enige mechanisme voor het verifiëren van toegang tooyour search-service-eindpunt. 

Een api-sleutel is een tekenreeks van willekeurige getallen en letters bestaan. Via [RBAC machtigingen](#rbac), kunt u verwijderen of Hallo toetsen niet lezen, maar u kunt een sleutel niet vervangen met een door de gebruiker gedefinieerd wachtwoord. 

Twee soorten sleutels zijn gebruikte tooaccess uw search-service:

* Beheerder (geldig voor een bewerking lezen-schrijven tegen de Hallo-service)
* Query (geldig voor alleen-lezen bewerkingen, zoals een query uitgevoerd naar een index)

Een admin api-sleutel wordt gemaakt wanneer het Hallo-service is ingericht. Er zijn twee administratorsleutels aangewezen als *primaire* en *secundaire* tookeep ze rechtstreeks, maar in feite uitwisselbaar zijn. Elke service heeft twee administratorsleutels zodat u een overschakelen kunt zonder verlies van tooyour-access-service. Kunt u beide administratorsleutel opnieuw genereren, maar u toohello admin totaal aantal niet toevoegen. Er is een maximum van twee administratorsleutels per zoekservice.

Querysleutels zijn ontworpen voor clienttoepassingen die rechtstreeks zoeken aanroepen. U kunt maken van too50 querysleutels. In de toepassingscode geeft u Hallo zoeken URL en een query api-sleutel tooallow alleen-lezentoegang toohello-service. Uw toepassingscode geeft ook Hallo-index die wordt gebruikt door uw toepassing. Gezamenlijk Hallo-eindpunt een api-sleutel voor alleen-lezen toegang en een doelindex definiëren Hallo bereik en het toegangsniveau van Hallo verbinding van uw clienttoepassing.

tooget of opnieuw genereren api-sleutels, open Hallo servicedashboard. Klik op **sleutels** tooslide Hallo Sleutelbeheer pagina openen. Opdrachten voor opnieuw genereren of het maken van sleutels zijn bovenaan Hallo Hallo pagina. Standaard worden alleen administratorsleutels gemaakt. Query api-sleutels moeten handmatig worden gemaakt.

 ![][9]

<a id="rbac"></a>

## <a name="secure-api-keys"></a>Api-sleutels beveiligen
Sleutelbeveiliging wordt gegarandeerd door het beperken van toegang via de portal Hallo of Resource Manager-interfaces (PowerShell of opdrachtregelinterface). Zoals is aangegeven, kunnen abonnementbeheerders weergeven en opnieuw genereren van alle api-sleutels. Bekijk voorzorg rol toewijzingen toounderstand die toegang toohello administratorsleutels heeft.

1. In het servicedashboard hello, klikt u op Hallo toegang pictogram tooslide open Hallo blade gebruikers.
   ![][7]
2. Controleer in gebruikers, bestaande roltoewijzingen. Zoals verwacht, hebt abonnementsbeheerders al volledige toegang toohello via de rol van eigenaar Hallo.
3. toodrill verdere, klikt u op **abonnementsbeheerders** en vouw vervolgens Hallo rol toewijzing lijst toosee die mede beheerdersrechten op uw search-service heeft.

Een andere manier tooview machtigingen is tooclick **rollen** op de blade gebruikers Hallo. Hiermee geeft u beschikbare rollen en het aantal gebruikers of groepen toegewezen tooeach rol Hallo.

<a id="sub-5"></a>

## <a name="monitor-resource-usage"></a>Resourcegebruik van de monitor
In Hallo dashboard is Broncontrole beperkt toohello informatie wordt weergegeven in het servicedashboard hello en enkele metrische gegevens die u aanvragen kunt door het uitvoeren van query's Hallo-service. U kunt op Hallo servicedashboard in de sectie voor het gebruik van Hallo snel bepalen of partitie resource niveaus, geschikt voor uw toepassing zijn.

Hallo-API van zoekservice gebruikt, kunt u een aantal aan documenten en indexen ophalen. Er zijn een vaste limieten die zijn gekoppeld aan dit aantal is gebaseerd op Hallo prijscategorie. Zie voor meer informatie [Servicelimieten zoeken](search-limits-quotas-capacity.md). 

* [Indexstatistieken opvragen](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)
* [Aantal documenten](https://docs.microsoft.com/rest/api/searchservice/count-documents)

> [!NOTE]
> Gedrag caching, kunt u een limiet tijdelijk overstate. Bijvoorbeeld, wanneer u gedeelde Hallo-service gebruikt, ziet u een document aantal via Hallo vaste limiet van 10.000 documenten. Hallo te is tijdelijk en wordt gedetecteerd op Hallo controle van de volgende afdwingen. 
> 
> 

## <a name="disaster-recovery-and-service-outages"></a>Disaster recovery en service uitval

Hoewel we uw gegevens restwaarde kunnen, biedt Azure Search geen chatberichten failover van de service Hallo als er een storing op Hallo cluster of data center-niveau. Als een cluster is mislukt in het datacenter hello, Hallo operationele team detecteert en toorestore service werken. Treedt uitvaltijd tijdens het terugzetten van de service. U kunt service tegoed toocompensate voor de service niet beschikbaar zijn per Hallo aanvragen [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). 

Als continue is vereist in de gebeurtenis Hallo van onherstelbare fouten buiten het beheer van Microsoft, kan [inrichten van een extra service](search-create-service-portal.md) in een andere regio en implementeer een geo-replicatie strategie tooensure indexen volledig redundante zijn op alle services.

Klanten die gebruikmaken van [indexeerfuncties](search-indexer-overview.md) toopopulate en vernieuw indexen aankan herstel na noodgevallen via geo-specifieke indexeerfuncties Hallo gebruik van dezelfde gegevensbron. Twee services in verschillende regio's, elk met een indexeerfunctie uitgevoerd kunnen indexeren van Hallo dezelfde gegevensbron tooachieve geografische redundantie. Als u van gegevensbronnen die ook geografisch redundante zijn indexeren, let er dan voor dat dat Azure Search indexeerfuncties alleen uitvoeren kunnen, incrementele indexering van de primaire replica's. In een failover worden ervoor toore punt Hallo indexeerfunctie toohello nieuwe primaire replica. 

Als u geen indexeerfuncties gebruikt, gebruikt u de toepassing code toopush objecten en gegevens toodifferent zoekservices parallel. Zie voor meer informatie [prestaties en optimalisatie in Azure Search](search-performance-optimization.md).

## <a name="backup-and-restore"></a>Back-ups en herstellen

Omdat Azure Search niet een opslagoplossing primaire gegevens is, bieden we een formele mechanisme voor self-service back-up en herstel niet. De toepassingscode die wordt gebruikt voor het maken en vullen met een index is Hallo feitelijke terugzetten optie als u per ongeluk een index verwijdert. 

toorebuild een index, zou u verwijderen (ervan uitgaande dat deze bestaat), Hallo index in Hallo-service opnieuw en opnieuw laden door het ophalen van gegevens van uw primaire data store. U kunt ook u kan bereiken te[klantondersteuning]() toosalvage geïndexeerd als er een regionale uitval.


<a id="scale"></a>

## <a name="scale-up-or-down"></a>Omhoog of omlaag schalen
Elke search-service wordt gestart met ten minste één replica en één partitie. Als u zich hebt aangemeld voor een [laag waarmee toegewijde bronnen](search-limits-quotas-capacity.md), klikt u op Hallo **SCALE** -tegel in het Resourcegebruik van Hallo service dashboard tooadjust.

Wanneer u capaciteit via een resource toevoegt, Hallo service ze automatisch gebruikt. Er is geen verdere actie vereist van uw kant, maar er is een lichte vertraging voordat Hallo impact van de nieuwe resource hello wordt gerealiseerd. Het kan 15 minuten of meer tooprovision duren aanvullende bronnen.

 ![][10]

### <a name="add-replicas"></a>Replica's toevoegen
Verhogen van query's per seconde (QPS) of bereiken van maximale beschikbaarheid wordt gedaan door replica's toe te voegen. Elke replica heeft één exemplaar van een index, zodat één meer replica toe te voegen tooone vertaalt meer index beschikbaar voor de verwerking van query-serviceaanvragen. Een minimum van 3 replica's zijn vereist voor hoge beschikbaarheid (Zie [capaciteitsplanning](search-capacity-planning.md) voor meer informatie).

Een service voor zoeken met meer replica's kunt query van aanvragen verdelen over laden via een groter aantal indexen. Een niveau van de query volume gezien, gaat query doorvoer toobe sneller wanneer er meer exemplaren van Hallo index beschikbaar tooservice Hallo aanvraag. Als u Querylatentie ondervindt, kunt u een positieve invloed op prestaties verwachten zodra Hallo extra replica online is.

Query doorvoer gaat u als u replica's toevoegt, maar deze niet exact dubbele of triple als u replica's tooyour service toevoegen. Alle zoektoepassingen zijn onderwerp tooexternal factoren die van invloed op de prestaties van query's zijn kunnen. Zijn twee factoren die toovariations in reactietijden van de query bijdragen complexe query's en netwerklatentie.

### <a name="add-partitions"></a>Partities toevoegen
De meeste servicetoepassingen hebben een ingebouwde hebben om meer replica's in plaats van partities. Voor gevallen waarin een aantal toegenomen document vereist is, kunt u partities toevoegen als u zich aangemeld voor Standard-service. Laag Basic biedt geen voor extra partities.

Standard-laag van Hallo partities worden toegevoegd in veelvouden van 12 (specifiek, 1, 2, 3, 4, 6 of 12). Dit is een artefact van sharding. Een index is gemaakt in 12 shards, die kunnen worden alle opgeslagen op 1 partitie of gelijkmatig verdeeld 2, 3, 4, 6 of 12 partities (één shard per partitie).

### <a name="remove-replicas"></a>Replica's verwijderen
U kunt na perioden van hoge query volumes replica's verminderen nadat zoeken querybelasting hebben (bijvoorbeeld nadat vakantiedag verkoop via zijn) genormaliseerd.

toodo deze, verplaatsen Hallo replica schuifregelaar back tooa lager getal. Er zijn geen verdere stappen vereist op uw kant. Hallo-aantal replica's te verlagen vervangen door virtuele machines in het datacenter Hallo. Uw query's en bewerkingen voor opname wordt nu uitgevoerd op minder virtuele machines dan voordat. Hallo minimumlimiet is één replica.

### <a name="remove-partitions"></a>Partities verwijderen
In tegenstelling tot het verwijderen van replica's waarvoor geen extra moeite ondernemen, moet u wellicht sommige toodo werk als u meer opslagruimte dan kan worden verkleind. Bijvoorbeeld, als uw oplossing van drie partities gebruikmaakt, downsizing tooone of twee partities genereren een fout als de nieuwe opslagruimte Hallo kleiner dan vereist is. Zoals u verwachten zou, uw keuzes zijn toodelete indexen of documenten binnen een bijbehorende index toofree ruimte of behouden van de huidige configuratie Hallo.

Er is geen detectiemethode die aangeeft welke shards index op specifieke partities zijn opgeslagen. Elke partitie bevat ongeveer 25 GB in de opslag, dus moet u tooreduce tooa opslaggrootte dat door het aantal partities die u hebt Hallo kan worden opgeslagen. Als u wilt dat toorevert tooone partitie, moet alle 12 shards toofit.

toohelp met toekomstige planning kunt u toocheck opslag (met behulp van [statistieken voor Index ophalen](https://docs.microsoft.com/rest/api/searchservice/Get-Index-Statistics)) toosee hoeveel u daadwerkelijk gebruikt. 

<a id="advanced-deployment"></a>

## <a name="best-practices-on-scale-and-deployment"></a>Aanbevolen procedures op schaal en implementatie
Deze 30 minuten durende video bekijkt aanbevelingen voor geavanceerde implementatiescenario's waaronder geografisch verspreide werkbelastingen. U ziet ook [prestaties en optimalisatie in Azure Search](search-performance-optimization.md) voor help-pagina's die Hallo behandeld dezelfde verwijst.

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<a id="next-steps"></a>

## <a name="next-steps"></a>Volgende stappen
Zodra u de basisbegrippen Hallo achter servicebeheer, kunt u overwegen [PowerShell](search-manage-powershell.md) tooautomate taken.

Wordt ook aangeraden Hallo controleren [prestaties en optimalisatie van het artikel](search-performance-optimization.md).

Een andere aanbeveling is toowatch Hallo video in de vorige sectie Hallo hebt genoteerd. Het biedt diepere dekking van Hallo technieken die in deze sectie wordt vermeld.

<!--Image references-->
[7]: ./media/search-manage/rbac-icon.png
[8]: ./media/search-manage/Azure-Search-Manage-1-URL.png
[9]: ./media/search-manage/Azure-Search-Manage-2-Keys.png
[10]: ./media/search-manage/Azure-Search-Manage-3-ScaleUp.png



