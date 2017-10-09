---
title: aaaArchitecture van Azure Service Fabric | Microsoft Docs
description: Service Fabric is dat een platform voor gedistribueerde systemen gebruikt toobuild schaalbare, betrouwbare en gemakkelijk te beheren toepassingen voor Hallo cloud. In dit artikel wordt Hallo-architectuur van Service Fabric.
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Service Fabric-architectuur
Service Fabric is gebouwd met gelaagde subsystemen. Deze subsystemen inschakelen toowrite toepassingen die zijn:

* Maximaal beschikbare
* Schaalbaar
* Beheerbare
* Testable

Hallo volgende diagram ziet u belangrijke subsystemen Hallo van Service Fabric.

![Diagram van Service Fabric-architectuur](media/service-fabric-architecture/service-fabric-architecture.png)

In een gedistribueerde systeem Hallo mogelijkheid toosecurely communicatie tussen knooppunten in een cluster is van cruciaal belang. Grondtal van Hallo-stack is Hallo Hallo transport subsysteem waarmee veilige communicatie tussen knooppunten. Subsysteem liggen boven Hallo transport Hallo federation subsysteem, welke clusters Hallo verschillende knooppunten in één entiteit (clusters genoemd), zodat de Service Fabric kunt fouten opsporen, opvulteken keuze uitvoeren en bieden consistente routering. Hallo betrouwbaarheid subsysteem gelaagd boven op Hallo federation subsysteem, is verantwoordelijk voor Hallo betrouwbaarheid van Service Fabric-services via mechanismen zoals replicatie bronbeheer en failover. Hallo federation subsysteem voltooiingscallback ook Hallo hosting en activering subsysteem die Hallo levenscyclus van een toepassing op één knooppunt beheert. Hallo management subsysteem beheert Hallo levenscyclus van toepassingen en services. Hallo testbaarheid subsysteem kan ontwikkelaars hun services via gesimuleerde fouten testen voor en na het implementeren van toepassingen en services tooproduction omgevingen. Service Fabric biedt Hallo mogelijkheid tooresolve servicelocaties via de communicatiesubsysteem. Hallo toepassing programmeermodellen blootgestelde toodevelopers zijn gelaagd boven deze subsystemen samen met de Hallo toepassing model tooenable tooling op.

## <a name="transport-subsystem"></a>Subsysteem voor transport
Hallo transport subsysteem implementeert een point-to-point communicatie datagramkanaal. Dit kanaal wordt gebruikt voor communicatie in service fabric-clusters en de communicatie tussen Hallo service fabric-cluster en clients. Deze ondersteuning biedt voor één richting en aanvragen / antwoorden communicatiepatronen, waardoor Hallo basis voor het implementeren van broadcast en multicast in Hallo Federation-laag. Hallo transport subsysteem communicatie beveiligt met behulp van X509 certificaten of Windows-beveiliging. Dit subsysteem wordt intern gebruikt door de Service Fabric en is niet rechtstreeks toegankelijk toodevelopers voor het programmeren van toepassing.

## <a name="federation-subsystem"></a>Subsysteem voor Federatie
In de volgorde tooreason over een verzameling van knooppunten in een gedistribueerde systemen moet u toohave een consistente weergave van Hallo-systeem. Hallo federation subsysteem Hallo communicatie primitieven geleverd door Hallo transport subsysteem gebruikt en steken Hallo verschillende knooppunten in een uniform cluster die deze reden kan over. Het biedt Hallo gedistribueerde systemen primitieven nodig door Hallo andere subsystemen - foutdetectie, opvulteken keuze en consistente routering. Hallo federation subsysteem is ingebouwd in gedistribueerde hashtabellen met een 128-bits token ruimte. Hallo-subsysteem zorgt voor een ringtopologie via Hallo knooppunten, met op elk knooppunt in een subset van Hallo token ruimte wordt toegewezen voor eigendom Hallo-ring. Hallo laag gebruikt voor de detectie is mislukt, een leasemechanisme op basis van hart kloppen in de race en arbitrage. Hallo federation subsysteem garandeert ook via het complexe lid worden en vertrek protocollen die slechts één eigenaar van een token op elk gewenst moment bestaat. Dit biedt opvulteken keuze en consistente routering garanties.

## <a name="reliability-subsystem"></a>Subsysteem voor betrouwbaarheid
Hallo betrouwbaarheid subsysteem biedt Hallo mechanisme toomake Hallo status van een Service Fabric-service die maximaal beschikbaar is via Hallo Hallo *Replicator*, *Failover Manager*, en  *Resource Balancer*.

* Hallo Replicator zorgt ervoor dat de status verandert in Hallo primaire service replica gerepliceerde toosecondary replica's, onderhouden van de consistentie tussen Hallo primaire en secundaire replica's in een replicaset service automatisch worden. Hallo replicator is verantwoordelijk voor quorumbeheer van replica's Hallo in Hallo replicaset. Deze samenwerkt met Hallo failover-eenheid tooget Hallo lijst met bewerkingen tooreplicate en Hallo herconfiguratie agent biedt het Hallo-configuratie van de replicaset Hallo. Deze configuratie geeft aan welke replica's Hallo-bewerkingen moeten toobe gerepliceerd. Service Fabric bevat een standaard replicator Fabric Replicator, die kan worden gebruikt door Hallo programming model API toomake Hallo servicestatus maximaal beschikbare en betrouwbare aangeroepen.
* Hallo Failover Manager zorgt ervoor dat wanneer knooppunten worden verwijderd uit de cluster Hallo tooor toegevoegd, Hallo load automatisch opnieuw verdeeld over Hallo beschikbare knooppunten. Als een knooppunt in Hallo-cluster is mislukt, opnieuw Hallo cluster replica's Hallo-toomaintain servicebeschikbaarheid wordt automatisch configureren.
* Hallo Resource Manager service replica's geplaatst in domein van de fout in Hallo-cluster en zorgt ervoor dat alle failover-eenheden operationeel zijn. Hallo Resource Manager hoeveelheid ook serviceresources over Hallo onderliggende gedeelde groep met cluster knooppunten tooachieve optimale uniform verdeling.

## <a name="management-subsystem"></a>Subsysteem voor beheer
Hallo management subsysteem biedt end-to-end-service en de levenscyclus van Toepassingsbeheer. PowerShell-cmdlets en administratieve API's kunt u tooprovision, implementeren, patches, upgrades, en ongedaan inrichten toepassingen zonder verlies van beschikbaarheid. Hallo management subsysteem voert dit via Hallo services te volgen.

* **Clusterbeheer**: dit primaire Hallo-service die met Failover Manager Hallo van betrouwbaarheid tooplace Hallo toepassingen op Hallo-knooppunten op basis van plaatsingsbeperkingen Hallo-service communiceert is. Hallo Resource Manager in failover-subsysteem zorgt ervoor dat Hallo beperkingen nooit verbroken. Hallo cluster manager beheert Hallo levenscyclus van Hallo toepassingen van inrichten toode-inrichten. Het is geïntegreerd met Hallo health manager tooensure dat beschikbaarheid van toepassingen niet van een perspectief semantische health verloren gaan tijdens upgrades is.
* **De Health Manager**: met deze service kan de statuscontrole van toepassingen, services en entiteiten van de cluster. Cluster-entiteiten (zoals knooppunten, servicepartities en replica's) kunnen melden statusgegevens, vervolgens wordt samengevoegd in Hallo Gecentraliseerde health store. Deze informatie health biedt een momentopname van een algemene point-in-time-status van Hallo services en knooppunten die zijn verdeeld over meerdere knooppunten in het Hallo-cluster, zodat u tootake nodig corrigerende maatregelen. Health-query-API's kunnen u tooquery Hallo health gebeurtenissen gerapporteerd toohello health subsysteem. Hallo health query API's retourneren Hallo onbewerkte health opgeslagen in Hallo health gegevensarchief of Hallo geaggregeerd, statusgegevens voor een specifieke cluster entiteit geïnterpreteerd.
* **Image Store**: deze service biedt opslag en distributie van Hallo binaire bestanden van toepassingen. Deze service biedt een eenvoudige gedistribueerde archief waar Hallo toepassingen geüploade tooand gedownload van zijn.

## <a name="hosting-subsystem"></a>Subsysteem voor hosting
Hallo-Clusterbeheer informeert Hallo hosting-subsysteem (uitgevoerd op elk knooppunt) die het onderhoudt toomanage moet voor een bepaald knooppunt. hosting-subsysteem vervolgens Hallo beheert Hallo levenscyclus van de toepassing hello op dat knooppunt. Deze samenwerkt met Hallo betrouwbaarheid en health onderdelen tooensure dat Hallo replica correct zijn ingevoerd, en zijn in orde.

## <a name="communication-subsystem"></a>Communicatiesubsysteem
Dit subsysteem biedt betrouwbare berichten in de cluster en de service discovery Hallo via Hallo Naming service. Hallo Naming service namen tooa servicelocatie in Hallo-cluster wordt omgezet en kan gebruikers toomanage servicenamen en eigenschappen. Hallo Naming service gebruikt, kunnen clients veilig communiceren met een willekeurig knooppunt in Hallo cluster tooresolve een servicenaam en ophalen van metagegevens. Met behulp van een eenvoudige Naming client API kunnen gebruikers van Service Fabric ontwikkelen services en clients die geschikt is voor het omzetten van de huidige netwerklocatie Hallo ondanks knooppunt dynamiek of wijzigen van Hallo het formaat van Hallo-cluster.

## <a name="testability-subsystem"></a>Subsysteem voor testbaarheid
Testbaarheid is een suite met hulpprogramma's die speciaal is ontworpen voor het testen van services is gebaseerd op de Service Fabric. Hallo hulpprogramma's kunt een ontwikkelaar eenvoudig zinvolle fouten veroorzaken en tooexercise voor test-scenario's worden uitgevoerd en valideren Hallo talrijke statussen en overgangen die een service tijdens de levensduur allemaal in een beheerde en veilige wijze optreden zal. Testbaarheid biedt een mechanisme toorun ook langer tests die verschillende mogelijke fouten zonder verlies van beschikbaarheid kunnen doorlopen. Dit biedt u een test in productie-omgeving.

