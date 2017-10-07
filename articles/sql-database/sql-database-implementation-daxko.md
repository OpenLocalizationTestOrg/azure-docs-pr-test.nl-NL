---
title: aaaAzure casestudy voor SQL Database Azure - Daxko/CSI | Microsoft Docs
description: Meer informatie over hoe Daxko/CSI tooaccelerate SQL-Database de ontwikkelingscyclus en tooenhance gebruikt de klantenservices en prestaties
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 00c8a713-f20c-4d6b-b8b7-0c1b9ba5f05b
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 3e3d58a1d9c3c919fc0e4cdb2765f680719c19d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="daxkocsi-used-azure-tooaccelerate-its-development-cycle-and-tooenhance-its-customer-services-and-performance"></a>Daxko/CSI gebruikt Azure tooaccelerate de ontwikkelingscyclus en tooenhance de klantenservices en prestaties
![Daxko/CSI-Logo](./media/sql-database-implementation-daxko/csidaxkologo25.png)

Daxko/CSI Software geconfronteerd met een challenge: klantendatabase geschiktheid en opnieuw gemaakt is groeit snel, Bedankt toohello succes van de oplossing uitgebreide-softwareproducten voor ondernemingen, maar houden met de IT-infrastructuur nodig voor deze groeiende heeft Hallo klanten is van het bedrijf Hallo testen IT-personeel. Hallo bedrijf is steeds beperkt door stijgende operations-overhead, met name voor het beheren van de groeiende databases. Slechter, die overhead operations is knippen in ontwikkeling resources voor nieuwe initiatieven, zoals nieuwe functies voor mobiliteit voor software van het bedrijf Hallo.

Volgens tooDavid Molina, directeur van ontwikkeling van het Product bij Daxko/CSI Azure opgegeven CSI Software met Hallo platform as a service (PaaS) model dat deze toosimplify-databasebeheer nodig schaalbaarheid te verhogen en resources toofocus op vrijmaken de software in plaats van ops. "Azure SQL Database is een goede optie voor ons. Omdat u niet hoeft tooworry over het onderhouden van een SQL-Server, een failover-cluster en alle Hallo andere behoeften infrastructuur is ideaal voor ons."

Aangezien tooAzure migreert, moet CSI Software een operationele personeel van slechts twee toomanage via 600 klantendatabases. Hallo bedrijf gebruikt Azure SQL Database elastische pools toomove klantendatabases op basis van de grootte en nodig.

Molina blijft, 'onze klanten merkbaar Hallo onmiddellijk wijzigen. Voordat elastische pools hadden van tijd tot tijd ze-outs en andere problemen tijdens burst perioden. Met Azure elastische pools, kunnen ze burst naar behoefte en Hallo-software zonder problemen gebruiken."

Bovendien tooimproving prestaties voor klanten, Azure elastische pools vrijgemaakt CSI Software resources toofocus over het ontwikkelen van nieuwe services en -onderdelen, in plaats van te moeten omgaan met bewerkingen en beheer. De IT-bronnen geholpen CSI Software verbeteren van de enterprise-software biedt, SpectrumNG, toohelp benaderen maakt leden, personeel efficiëntie te verbeteren en personeel en leden mobiele toegang bieden voor interactieve taken en realtime meldingen.

Azure heeft ook CSI Software versnellen en Hallo ontwikkeling en kwaliteit-assurance (QA) cyclus verbeteren doordat automatiseringsopties geholpen. Met Azure implementatie van het bedrijf hello, kunnen managers build-onderdelen met Hallo Klik op de knop verpakken. Zoals in Molina wordt beschreven, 'als onderdeel van Hallo releasecyclus QA is nu kunnen toodeploy tooa testomgeving in Azure, dit komt sterk onze productie-stack overeen. We kunt builds kunt implementeren, onmiddellijk tooour dev omgeving toovet wordt gewijzigd. Die is een grote win voor ons, omdat we pariteit voor testen voorafgaand aan die niet beschikbaar."

## <a name="offloading-toohello-cloud"></a>Offloading van toohello cloud
Voordat u doorgaat toohello cloud, CSI Software had is gebouwd op basis de eigen multitenant-infrastructuur in een lokaal datacenter in Houston. Hallo bedrijf uitgevouwen, het toenemende groeipijn van aanschaffen, inrichting en het onderhoud Hallo hardware te maken en software vereist toosupport zijn klanten. IT-personeel toohandle bewerkingen is een andere knelpunt die hebben geleid tooa vertraging van de nieuwe resources inrichten en implementeren van nieuwe services toocustomers geworden.

CSI Software opgezocht in de cloud-opties voor die overhead verwijderen zodat deze zich op de code, in plaats van bewerkingen concentreren kan. Hallo bedrijf gedetecteerd dat veel van de bovenste cloudproviders Hallo alleen oplossingen aan te bieden infrastructure as a service (IaaS) waarvoor nog steeds een grote IT-personeel toomanage hello IaaS-stack. In Hallo-end bepaald CSI Software dat hello Azure PaaS-oplossing Hallo beste geschikt is voor de behoeften is. Molina wordt uitgelegd, "Azure opgehaald Hallo hardware en software buiten Hallo manier, zodat we ons kunnen richten op de offerings software bij onze IT-overhead verminderen."

## <a name="making-hello-transition-tooazure"></a>Hallo overgang tooAzure maken
Na het selecteren van Azure voor de PaaS-oplossing, begon CSI Software met de back-end-infrastructuur en databases toohello-cloud migreert. Eerdere tooAzure SpectrumNG klanten nodig tooinstall een clienttoepassing die met een Windows Communication Foundation (WCF)-service op de back-end Hallo gecommuniceerd. Op basis van tooMolina, 'Hoewel sommige klanten alles in hun eigen datacenters gehost, we uit Hallo product toobe multitenant gebouwd. We gehost alles in een datacenter in Houston, met behulp van SQL Server als gegevensopslag Hallo.

"De aanbieding van ons product opgenomen ook lid gerichte webportal (geschreven in ASP.net), die ontworpen toobe wit gelabeld toomatch Hallo van klant aanwezigheid op het web, en een SOAP-API toosupport Hallo online-pagina's en eventuele integratie van derden is."

Hallo migratie toohello cloud is niet lang duren voor Hallo-architectuur. Op basis van tooMolina, 'Hallo meerderheid van Hallo inspanning behandeld aanpassing Hallo manier dat we config bestandsgegevens, de wijziging van een gecentraliseerde verbindingsreeks, lees- en automatiseren Hallo verpakking, uploaden en implementeren van onze releases."

Hallo toodevelop vorm van automatisering ontwikkelen, CSI softwareontwikkelaars gebruikt Azure PowerShell en REST-API's toocreate pakketten en uploadt u de faseringsomgeving tooa voor elke nacht release.
Hallo algehele overgang tooan Azure-cloud-gebaseerde implementatie is gegaan soepel en snel voor Hallo CSI Software IT-team. Molina wordt uitgelegd, 'In alle, hebben we een beta-omgeving in de cloud Hallo binnen drie toofour weken op Hallo-project te nemen. Dat was een verrassend win voor ons."

Nadat hello omgeving configureren en testen, CSI Software begon met het migreren van klanten. Hallo overgang is voor klanten die al gebruikmaken van CSI Software die als host fungeert, bijna naadloze. Voor klanten die migratie van een on-premises implementatie, Hallo migratie toohello cloud wat extra tijd nodig was, maar is nog steeds voornamelijk pijn vrij voor klanten en CSI Software.

Voor nieuwe klanten, CSI Software van IT-medewerkers gebruiken Hallo na proces tooon-board ze tooAzure:

1. Azure PowerShell-scripts zijn gebruikte toospin een nieuwe database voor de klant Hallo; alle klanten start uit op een premium-laag tooensure voldoende initiële doorvoer voor Hallo overgang.
2. Indien mogelijk, CSI Software maakt gebruik van hello Azure SQL Migration Wizard toomove bestaande gegevens tooan Azure SQL Database-exemplaar.
3. Ten slotte Microsoft SQL Server Integration Services (SSIS) gebruikte tooreconcile worden eventuele verschillen in Hallo gegevens of tooperform opschoontaken gegevens als vereist.

Vandaag de dag worden ongeveer 99 procent van klanten CSI Software gehost in Azure, in vier regionale datacenters (Noord-centraal, Zuid-centraal, Oost en West). Doordat de datacentra in elke klant geografische regio, wordt latentie opgeslagen tooa minimale.

## <a name="azure-elastic-pools-free-up-it-resources"></a>Azure elastische pools om een IT-bronnen vrij te maken
Verschillende functies van Azure hebben bijgedragen CSI Software verschuiving van de infrastructuur en bewerkingen gerichte toobeing-functie en ontwikkeling die zijn gericht. Mogelijk is de grootste voordeel Hallo van elastische pools.

Op dit moment biedt CSI Software ongeveer 550 databases voor klanten. Voordat u Elastische pools was het moeilijk toomanage dat veel databases binnen een structuur laag. OPS managers had tooassign prestatielagen op basis van Hallo burst behoeften van klanten, die significante IT-resource overhead vereist. Met elastische pools kunnen managers tenants premium- of standard-pool naar gelang van toepassing, toewijst en verplaats klanten op basis van de grootte en nodig. Klanten merkbaar Hallo gevolgen van het Hallo elastische pools bijna onmiddellijk; voordat u Elastische pools klanten-outs en andere problemen waren tijdens perioden burst gebruik, maar met elastische pools klanten activiteit bursts kunnen problemen indien nodig en kunnen ze toouse SpectrumNG zonder problemen doorgaan.

## <a name="azure-active-geo-replication-accelerates-reporting"></a>Azure actieve geo-replicatie versnelt rapportage
Klanten met verschillende CSI Software zijn ook profiteren van Azure actieve geo-replicatie. Met actieve geo-replicatie, up toofour leesbare secundaire databases kunnen worden geconfigureerd in Hallo dezelfde of verschillende datacenterregio's. CSI Software maakt gebruik van actieve geo-replicatie op twee manieren: eerst Hallo secundaire databases zijn beschikbaar in Hallo geval van een datacenter onderbreking of Hallo onvermogen tooconnect toohello primaire database. en ten tweede Hallo secundaire databases kunnen worden gelezen en gebruikte toooffload alleen-lezen werkbelastingen, zoals rapportage van taken kunnen worden. Sommige klanten CSI Software gebruiken deze voordeel tooaccelerate werkstromen reporting.

## <a name="csi-software-application-logic-and-architecture"></a>De toepassingslogica CSI Software en -architectuur
SpectrumNG maakt gebruik van web-rollen. Omdat de toepassing hello multitenant is, is een WCF-service gebruikte toohandle Hallo oorspronkelijke verbindingsaanvraag van klanten. Als Molina statussen, ' Hallo aanvraag identificeert elke klant, waarmee vervolgens ons bouwen een verbindingsreeks uit tootheir databases toodo wat moeten we toodo. "

Voor de weblaag Hallo van de service maakt CSI Software gebruik van Azure automatisch schalen op basis van de dag en tijd. Beschikbare resources zijn automatisch toegenomen tooaccommodate hoger gebruik tijdens de kantooruren, op basis van de tijdzone toohello van elk regionale datacenter. Resources zijn ook ingesteld tooscale omlaag in het weekend, wanneer de klant moet lager zijn.

![Daxko/CSI-architectuur](./media/sql-database-implementation-daxko/figure1.png)

Afbeelding 1. Een cloud services-werkrol tekent gestructureerde gegevens van Azure SQL Database en semi-gestructureerde gegevens uit de tabelopslag. SpectrumNG gebruikers communiceren met dat gegevens via een cloud services-Webrol.

## <a name="using-web-apps-and-a-web-plan-tier-for-mobile-apps"></a>Met behulp van web-apps en een laag web-plan voor mobiele apps
Met behulp van Azure SQL Database-resources voor CSI Software tooenable vrijgemaakt nieuwe initiatieven, met inbegrip van een volledige mobiel platform op basis van een aangepaste API gebruiken die worden gehost in Azure-web-apps. Hallo-platform stelt maakt leden en personeel toouse mobiele apparaten toocheck planningen boek klassen en ontvangen van berichten.

Hallo-platform gebruikt service oriented architecture (SOA) tootake één onderdeel, een verkooppunten (POS) of een verkoop-systeem, zoals: verplaatsen op Hallo invoegen tooanother web plan en vervolgens draaien van een service-toosupport dat onderdeel terwijl alle andere objecten op Hallo oorspronkelijke web planning. Deze mogelijkheid biedt grote flexibiliteit CSI Software en het helpt kostenbeperkend.

## <a name="azure-lets-csi-software-developers-focus-on-apps-and-services"></a>Azure kunt CSI Software ontwikkelaars zich richten op de apps en services
Azure SQL-Database niet alleen een boon tooSpectrumNG klanten die Profiteer Hallo snelle, betrouwbare service, het is ook een groot voordeel voor CSI Software van IT-personeel en ontwikkelaars. Door het offloaden van ops tooAzure in de cloud Hallo CSI Software beperkt de overhead voor resources en infrastructuur aanzienlijk versnelde de ontwikkelingscycli en toomicromanage databases toooptimize prestaties wordt niet langer nodig heeft voor de tenants.

## <a name="more-information"></a>Meer informatie
* toolearn meer informatie over Azure elastische pools, Zie [elastische pools](sql-database-elastic-pool.md).
* Zie toolearn meer informatie over hulpmiddelen voor databases en elastisch schalen [hulpmiddelen voor elastische databases en elastisch schalen](sql-database-elastic-scale-get-started.md).
* Zie toolearn meer informatie over het migreren van een SQL Server-database, Zie [migreren van een SQL Server-database tooAzure](sql-database-cloud-migrate.md).
* toolearn meer informatie over actieve geo-replicatie, Zie [actieve geo-replicatie](sql-database-geo-replication-overview.md).
* toolearn meer informatie over webrollen en werkrollen, Zie [werkrollen](../fundamentals-introduction-to-azure.md#compute).    
* Zie toolearn meer informatie over Azure Service Bus [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* Zie toolearn meer informatie over automatisch geschaald [cloudservices schalen](../cloud-services/cloud-services-how-to-scale.md).

