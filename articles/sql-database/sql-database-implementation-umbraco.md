---
title: aaaAzure casestudy voor SQL Database Azure - Umbraco | Microsoft Docs
description: Meer informatie over hoe Umbraco maakt gebruik van SQL-Database tooquickly inrichten en scale-services voor duizenden tenants in de cloud Hallo
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5243d31e-3241-4cb0-9470-ad488ff28572
ms.service: sql-database
ms.custom: reference
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 93e39e509831a5ff90f129d9537ece0b0dafef0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="umbraco-uses-azure-sql-database-tooquickly-provision-and-scale-services-for-thousands-of-tenants-in-hello-cloud"></a>Umbraco maakt gebruik van Azure SQL Database tooquickly inrichten en scale-services voor duizenden tenants in de cloud Hallo
![Umbraco-Logo](./media/sql-database-implementation-umbraco/umbracologo.png)

Umbraco is een populaire open-source inhoud-beheersysteem (CMS) dat toepassingen van kleine campagne of brochure sites toocomplex voor Fortune 500-bedrijven en globale media websites uitvoeren kan. 

> "We hebben zeer grote community van ontwikkelaars die gebruikmaken van Hallo-systeem met meer dan 100.000 ontwikkelaars op onze forums en meer dan 350.000 sites die zijn live, Umbraco uitgevoerd."
> 
> — Morten Christensen, technische Lead Umbraco
> 
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-Case-Study-Umbraco/player]
> 
> 

implementaties van de klant toosimplify, Umbraco toegevoegd Umbraco-as-a-Service (UaaS): een software-as-a-service (SaaS)-oplossing die niet meer nodig voor on-premises implementaties Hallo biedt ingebouwde schalen en management overhead verwijderen door in te schakelen ontwikkelaars toofocus op het gebied van product innovatie in plaats van een oplossing. Umbraco is kunnen tooprovide alle voordelen van vertrouwen op Hallo flexibel platform as a service (PaaS) model aangeboden door Microsoft Azure.

UaaS kunt SaaS klanten toouse Umbraco CMS mogelijkheden die eerder buiten hun bereik waren. Deze klanten zijn ingericht met een werkende CMS-omgeving die een productiedatabase. Klanten kunnen toevoegen, tootwo extra databases voor ontwikkelings- en faseringsomgevingen, afhankelijk van de vereisten. Wanneer een nieuwe omgeving wordt aangevraagd, een geautomatiseerd proces toegewezen die klant een database automatisch. Hallo nieuwe database kan in seconden, omdat de database Hallo al vooraf zijn ingericht met Umbraco uit een Azure elastische groep met beschikbare databases (Zie afbeelding 1).

![Inrichting lifecycle Umbraco](./media/sql-database-implementation-umbraco/figure1.png)

Afbeelding 1. Inrichting van de levenscyclus voor Umbraco als een Service (UaaS)

## <a name="azure-elastic-pools-and-automation-simplify-deployments"></a>Azure elastische pools en automatisering vereenvoudigen implementaties
Met Azure SQL Database en andere Azure-services, Umbraco klanten kunnen zelf hun omgeving inrichten en Umbraco eenvoudig kunt controleren en beheren van databases als onderdeel van een intuïtieve werkstroom:

1. Inrichten
   
   Umbraco onderhoudt een capaciteit van 200 beschikbare vooraf is ingericht databases van elastische pools. Wanneer een nieuwe klant zich registreert voor UaaS, biedt Umbraco Hallo klant met een nieuwe CMS-omgeving in bijna realtime door toe te wijzen een database van Hallo beschikbaarheid van toepassingen.
   
   Wanneer een beschikbaarheid van toepassingen de drempel bereikt, wordt een nieuwe elastische pool wordt gemaakt en nieuwe databases vooraf is ingericht toobe toocustomers toegewezen zo nodig zijn.
   
   Implementatie is volledig geautomatiseerd met C# management-bibliotheken en Azure Service Bus-wachtrijen.
2. Gebruikmaken van
   
   Klanten gebruik een toothree-omgevingen (productie, fasering en/of ontwikkeling), elk met een eigen database. Klantendatabases zijn in elastische pools, waardoor Umbraco tooprovide efficiënt schalen zonder tooover inrichten.
   
   ![Overzicht van het project Umbraco](./media/sql-database-implementation-umbraco/figure2.png)
   
   ![Details van de projecten Umbraco](./media/sql-database-implementation-umbraco/figure3.png)
   
   Afbeelding 2. Umbraco-as-a-Service (UaaS) klant website met overzicht van project en details
   
   Azure SQL Database's (Database Transaction Units) toorepresent Hallo relatieve kracht vereist voor de werkelijke databasetransacties gebruikt. Voor klanten UaaS, databases doorgaans op ongeveer 10 dtu's werken, maar elk Hallo elasticiteit tooscale op verzoek heeft. Dit betekent dat UaaS kunt ervoor zorgen dat gebruikers altijd benodigde resources zelfs tijdens piektijden hebben. Bijvoorbeeld, tijdens een recente zondag Sport-gebeurtenis wordt één UaaS klant opgetreden in database pieken up too100 dtu's voor Hallo duur van de game Hallo. Azure elastische pools maakte het mogelijk voor Umbraco toosupport die grote vraag zonder verminderde prestaties.
3. Bewaken
   
   Umbraco monitors database activiteit met dashboards binnen hello Azure-portal, samen met aangepaste e-mailwaarschuwingen.
4. Herstel na noodgevallen
   
   Azure biedt twee opties voor noodherstel (DR): actieve geo-replicatie en geo-herstel. Hallo DR-optie die een bedrijf moet selecteert is afhankelijk van de [zakelijke continuïteit doelstellingen](sql-database-business-continuity.md).
   
   actieve geo-replicatie biedt de snelste niveau Hallo van antwoord in de gebeurtenis Hallo uitvaltijd. Actieve geo-replicatie kunt u up toofour leesbare secundaire replica's op servers in verschillende regio's en kunt u failover tooany van Hallo secundaire replica's in geval van een storing Hallo initiëren.
   
   Umbraco geen geo-replicatie vereist, maar deze profiteren van Azure geo-restore toohelp minimale downtime in geval van een storing Hallo garanderen. geo-restore afhankelijk van de databaseback-ups in geografisch redundante Azure-opslag. Waarmee gebruikers toorestore vanaf een back-up wanneer er een storing in Hallo primaire regio.
5. Deactivering inrichten
   
   Wanneer een project-omgeving wordt verwijderd, worden alle bijbehorende databases (ontwikkeling, staging of live) tijdens het opschonen van Azure Service Bus-wachtrij verwijderd. Dit proces automatische herstelacties Hallo van niet-gebruikte databases tooUmbraco elastische database-beschikbaarheid van toepassingen, zodat ze beschikbaar zijn voor het inrichten van toekomstige behoud maximaal worden gebruikt.

## <a name="elastic-pools-allow-uaas-tooscale-with-ease"></a>Elastische pools toestaan UaaS tooscale met gemak
Door gebruik te maken van Azure elastische pools, kunt Umbraco optimaliseren voor klanten zonder tooover of onder inrichten. Umbraco heeft momenteel bijna 3.000 databases tussen 19 elastische pools, met Hallo mogelijkheid tooeasily schalen als benodigde tooaccommodate van hun bestaande 325,000 klanten of nieuwe klanten die gereed toodeploy een CMS in Hallo cloud.

In feite volgens tooMorten Christensen, technische leiden op Umbraco, 'UaaS is nu met de groei van ongeveer 30 nieuwe klanten per dag. Onze klanten zijn zeer tevreden over Hallo gemak kunnen tooprovision nieuwe projecten worden in seconden, onmiddellijk publiceer updates tootheir live sites van een ontwikkelomgeving met één klik-implementatie en aanbrengen net zo snel als ze fouten vinden . "

Als een klant een tweede en/of derde omgeving niet meer nodig, het hoeft te verwijderen die omgevingen. Die bronnen die kunnen worden gebruikt voor andere klanten als onderdeel van Hallo Umbraco elastische database-beschikbaarheid van toepassingen vrijgemaakt.

![Architectuur voor Umbraco-implementatie](./media/sql-database-implementation-umbraco/figure4.png)

Afbeelding 3. Architectuur van UaaS-implementatie in Microsoft Azure

## <a name="hello-path-from-datacenter-toocloud"></a>Hallo-pad van het datacenter toocloud
Wanneer er Hallo Umbraco ontwikkelaars gedaan in eerste instantie Hallo besluit toomove tooa SaaS-model, kent ze dat zou moeten een rendabele en schaalbare manier toobuild Hallo-service uit.

> 'elastische pools zijn een bij uitstek geschikt voor onze SaaS-aanbieding omdat we capaciteit omhoog en omlaag naar behoefte kunt kiezen. Inrichting is eenvoudig en met onze setup we gebruik kunt houden met een maximum."
> 
> — Morten Christensen, technische Lead Umbraco
> 
> 

' We wilden toospend onze tijd op het oplossen van problemen van onze klanten, niet infrastructuurbeheer. We wilden toomake gemakkelijk voor onze klanten tooget meeste waarde Hallo ' Niels Hartvig, oprichting van Umbraco staat. "We in eerste instantie beschouwd als Hallo servers onszelf hosten, maar capaciteitsplanning had een nachtmerrie." Tegelijk komt Umbraco niet gebruikmaken van elke databasebeheerders die een toegevoegde waarde van sleutel voor het gebruik van UaaS onderstrepingstekens.

Een belangrijk doel voor Hallo Umbraco ontwikkelaars is tooprovide een manier voor UaaS klanten tooprovision omgevingen snel en zonder beperkingen van de capaciteit. Maar bieden dat een toegewijde gehoste service in Umbraco-datacenters vereist veel overtollige capaciteit toohandle zou hebben barst bij de verwerking. Die zou hebben bedoeld aanzienlijk beheerinfrastructuur die zou hebben is regelmatig onderbenutte toe te voegen.

Hallo Umbraco ontwikkelteam wilde bovendien een oplossing waarmee ze tooreuse zo veel mogelijk van hun bestaande code mogelijk. Als ontwikkelaar Umbraco statussen Mikkel Madsen, 'We zijn blij met Hallo Microsoft ontwikkelprogramma's die al bekend bent met, zoals Microsoft SQL Server, Microsoft Azure SQL Database, ASP.net en Internet informatieservices (IIS zijn). Cloud-oplossing, voordat u investeert in een IaaS- of een PaaS wilden we toomake ervoor dat deze zou ondersteuning voor onze Microsoft-programma's en platformen, zodat we geen toomake grote veranderingen tooour codebasis hebt. "

alle toomeet van de criteria Umbraco opgezocht voor een cloud partner Hello kwalificaties te volgen:

* Voldoende capaciteit en betrouwbaarheid
* Ondersteuning voor Microsoft ontwikkelingsprogramma's, zodat die Umbraco engineers niet worden gedwongen toocompletely hun ontwikkelomgeving doelen
* Aanwezigheid in alle Hallo geografische markten waarin UaaS (bedrijven moeten tooensure concurreert dat toegang te krijgen hun gegevens snel tot en dat er gegevens worden opgeslagen op een locatie die voldoet aan de regionale wettelijke vereisten)

## <a name="why-umbraco-chose-azure-for-uaas"></a>Waarom Azure in Umbraco hebt gekozen voor UaaS
Op basis van tooMorten Christensen 'met inbegrip van alle opties voor onze we geselecteerd Azure omdat deze is voldaan aan alle onze criteria, van beheerbaarheid en schaalbaarheid toofamiliarity en kosteneffectiviteit. We stellen Hallo omgevingen op Azure Virtual machines en elke omgeving heeft een eigen Azure SQL Database-exemplaar met alle Hallo-exemplaren in elastische pools. Door het scheiden van databases tussen ontwikkeling, fasering en productieomgevingen kunt bieden wij onze klanten krachtige prestaties isolatie overeenkomende tooscale: een enorme win. "

Morten blijft, 'voordat, hebben we handmatig tooprovision servers voor Webdatabases. Er zijn momenteel geen nu toothink erover. Alles wordt automatisch uitgevoerd, vanaf de inrichting toocleanup. "

Morten is ook tevreden Hello schalen van de mogelijkheden van Azure. 'elastische pools zijn een bij uitstek geschikt voor onze SaaS-aanbieding omdat we capaciteit omhoog en omlaag naar behoefte kunt kiezen. Inrichting is eenvoudig en met onze setup we gebruik kunt houden met een maximum." Morten statussen, 'Hallo eenvoud van elastische pools, samen met de Hallo zekerheid van de service tier-gebaseerde dtu's biedt ons Hallo power tooprovision nieuwe resourcegroepen op aanvraag. Een van onze klanten met grotere een onlangs piek too100 dtu's in de productieomgeving. Met Azure ons elastische pools opgegeven van de klant Hallo databases met Hallo-resources die ze nodig in realtime zijn zonder toopredict DTU vereisten. Kortom, ophalen onze klanten Hallo Schakel rond de tijd dat ze verwachten en we kunnen voldoen aan de serviceovereenkomsten prestaties."

Mikkel Madsen dit opgeteld: 'We helemaal bent gewonnen Hallo krachtige Azure algoritme die verbinding maakt een algemene SaaS scenario (nieuwe klanten voor onboarding in realtime op grote schaal) tooour patroon van toepassing (vooraf inrichten databases, beide ontwikkeling en live) boven op Hallo onderliggende technologie (met behulp van Azure Service Bus-wachtrijen in combinatie met Azure SQL Database).'

## <a name="with-azure-uaas-is-exceeding-customer-expectations"></a>Met Azure overschrijdt UaaS verwachtingen van klanten
Umbraco is sinds het kiezen van Azure als de partner van de cloud kunnen tooprovide UaaS klanten met optimale prestaties van de inhoud-management, zonder de vereiste van een host zichzelf oplossing Hallo IT-resource-investering. Als Morten zegt: 'We graag gemak van ontwikkelaars Hallo en schaalbaarheid waarmee Azure ons en onze klanten zijn geweldig Hallo functies en betrouwbaarheid. Over het algemeen is een uitstekende win voor ons!'

## <a name="more-information"></a>Meer informatie
* toolearn meer informatie over Azure elastische pools, Zie [elastische pools](sql-database-elastic-pool.md).
* Zie toolearn meer informatie over Azure Service Bus [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).
* toolearn meer informatie over webrollen en werkrollen, Zie [werkrollen](../fundamentals-introduction-to-azure.md#compute).    
* toolearn meer informatie over virtuele netwerken, Zie [virtuele netwerken](https://azure.microsoft.com/documentation/services/virtual-network/).    
* toolearn meer informatie over back-up en herstel, Zie [bedrijfscontinuïteit](sql-database-business-continuity.md).    
* toolearn meer informatie over het bewaken van ppols, Zie [bewaking van groepen](sql-database-elastic-pool-manage-portal.md).    
* toolearn meer informatie over Umbraco als een Service, Zie [Umbraco](https://umbraco.com/cloud).

