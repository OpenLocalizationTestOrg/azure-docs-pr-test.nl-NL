---
title: aaaMulti Tenant Web Application patroon | Microsoft Docs
description: Architectuur overzichten en ontwerppatronen waarin wordt beschreven hoe een multitenant tooimplement webtoepassing op Azure vinden.
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Multitenant-toepassingen in Azure
Een multitenant-toepassing is een gedeelde bron waarmee afzonderlijke gebruikers of '-tenants,' tooview Hallo toepassing alsof het was hun eigen. Een typisch scenario die gepaard tooa multitenant toepassing is een in alle gebruikers van Hallo toepassing mogelijk wilt toocustomize Hallo gebruikerservaring maar anders hebben Hallo dezelfde elementaire zakelijke vereisten. Voorbeelden van grote multitenant toepassingen zijn Office 365, Outlook.com en visualstudio.com.

Vanuit het perspectief van de toepassingsprovider van een, van Hallo voordelen van multitenancy voornamelijk betrekking toooperational en efficiëntie kosten. Hallo behoeften van veel tenants/klanten, zodat de consolidatie van systeem beheertaken, zoals controle, prestaties afstemmen, onderhoud en gegevensback-ups kan voorzien in een versie van uw toepassing.

Hallo volgende geeft een lijst van de belangrijkste doelstellingen Hallo en vereisten vanuit het perspectief van de provider van.

* **Inrichting**: U moet nieuwe tenants kunnen tooprovision voor Hallo-toepassing.  Voor multitenant-toepassingen met een groot aantal tenants, het is doorgaans nodig tooautomate dit proces door selfservice inrichting inschakelen.
* **Onderhoud**: moeten kunnen tooupgrade Hallo toepassing en andere onderhoudstaken uitvoeren terwijl's hier gebruik van meerdere tenants.
* **Bewaking**: U moet kunnen toomonitor Hallo-toepassing op alle tijden tooidentify eventuele problemen en tootroubleshoot ze. Dit omvat hoe een elke tenant met behulp van de toepassing hello bewaking.

Een goed geïmplementeerde multitenant toepassing biedt Hallo volgende voordelen biedt voor toousers.

* **Isolatie**: Hallo activiteiten van individuele tenants hebben geen invloed op Hallo gebruik van de toepassing hello van andere tenants. Tenants geen toegang tot elkaars gegevens. Toohello tenant lijkt het alsof ze exclusief gebruik van de toepassing hello hebben.
* **Beschikbaarheid**: individuele tenants wilt Hallo toepassing toobe voortdurend beschikbaar zijn, mogelijk met garanties gedefinieerd in een SLA. Opnieuw mag Hallo activiteiten van andere tenants niet Hallo beschikbaarheid van de toepassing hello beïnvloeden.
* **Schaalbaarheid**: toepassing hello schaalt toomeet Hallo vraag van individuele tenants. Hallo aanwezigheid en acties van andere tenants moeten geen invloed op prestaties van de toepassing hello Hallo.
* **Kosten**: kosten zijn lager is dan het uitvoeren van een toepassing speciale, één tenant omdat multi-tenancymodus Hiermee Hallo delen van bronnen.
* **Aanpassingsmogelijkheden**. Hallo mogelijkheid toocustomize Hallo-toepassing voor een afzonderlijke tenant op verschillende manieren zoals toevoegen of verwijderen van functies, kleuren en logo's wijzigen of zelfs de toevoeging van hun eigen code of script.

Kortom, terwijl er zijn een aantal zaken die u moet rekening account tooprovide een zeer schaalbare service, er zijn ook een aantal Hallo doelstellingen en vereisten die algemene toomany multitenant-toepassingen zijn. Sommige is mogelijk niet relevant zijn in bepaalde scenario's en Hallo belang van afzonderlijke doelstellingen en vereisten zullen variëren in elk scenario. Als een provider van multitenant toepassing hello ook hebt u doelen en vereisten zoals vergadering Hallo tenants doelstellingen en vereisten, winstgevendheid, facturering, meerdere serviceniveaus, inrichting, bewaking van onderhoud en automatisering.

Zie voor meer informatie over aanvullende ontwerpoverwegingen van een toepassing met multitenant [die als host fungeert voor een Multitenant-toepassing in Azure][Hosting a Multi-Tenant Application on Azure]. Zie voor informatie over algemene gegevensarchitectuurpatronen van multitenant software as a service (SaaS)-databasetoepassingen, [Ontwerppatronen voor multitenant SaaS-toepassingen met Azure SQL Database](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

Azure biedt veel functies waarmee u tooaddress Hallo belangrijke problemen bij het ontwerpen van een multitenant-systeem.

**Isolatie**

* Tenants segment Website door hostheaders met of zonder SSL-communicatie
* Tenants segment Website door queryparameters
* Web-Services werkrollen
  * Werkrollen. die gegevens op Hallo back-end van een toepassing doorgaans niet verwerken.
  * Web-rollen die doorgaans als Hallo frontend voor toepassingen fungeren.

**Storage**

Gegevensbeheer zoals Azure SQL Database- of Azure Storage-services zoals Hallo Tabelservice dat voor opslag van grote hoeveelheden ongestructureerde gegevens biedt en de Blob-service waarmee services toostore grote hoeveelheden ongestructureerde tekst hello of binaire gegevens zoals video, audio en afbeeldingen.

* Het beveiligen van Multitenant-gegevens in de juiste SQL-Database per-tenant SQL Server-aanmeldingen.
* U kunt met behulp van Azure-tabellen voor de toepassing Resources door te geven een container niveau toegangsbeleid, mogelijkheid tooadjust machtigingen Hallo zonder tooissue nieuwe URL's voor Hallo bronnen worden beveiligd met handtekeningen voor gedeelde toegang.
* Azure wachtrijen voor toepassing Resources Azure wachtrijen zijn vaak gebruikte toodrive namens tenants verwerking, maar kan ook worden gebruikt toodistribute werk vereist voor het inrichten of management.
* Service Bus-wachtrijen voor toepassingsbronnen die pushes werk tooa gedeelde een service, kunt u een enkele wachtrij waar elke tenant afzender alleen machtigingen (die is afgeleid van claims die zijn uitgegeven vanuit uit ACS) toopush toothat wachtrij tijdens alleen Hallo ontvangers van Hallo-service heeft machtiging toopull van Hallo wachtrij Hallo gegevens die afkomstig zijn van meerdere tenants hebben.

**Verbinding en beveiligingsservices**

* Azure Service Bus een messaging-infrastructuur die tussen toepassingen zodat ze tooexchange berichten in een losse manier voor verbeterde schaal en tolerantie.

**Netwerkservices**

Azure biedt verschillende netwerkservices die ondersteuning bieden voor verificatie en de beheerbaarheid van uw gehoste toepassingen. Deze services zijn Hallo volgende:

* Azure Virtual Network-Hiermee kunt u inrichten en beheren van virtuele particuliere netwerken (VPN's) in Azure, alsmede veilig koppelen aan alle lokale IT-infrastructuur.
* Virtueel netwerk Traffic Manager kunt u tooload saldo binnenkomend verkeer over meerdere gehoste Azure-services of ze zijn uitgevoerd in Hallo hetzelfde datacenter of in verschillende datacenters Hallo wereld.
* Azure Active Directory (Azure AD) is een moderne, REST gebaseerde service die mogelijkheden voor beheer en toegang beheren voor uw cloudtoepassingen biedt. Met behulp van Azure AD voor toepassingsbronnen Azure AD-tooprovides een eenvoudige manier van verificatie en autorisatie van gebruikers toogain toegang tooyour-webtoepassingen en services tijdens het Hallo-functies van verificatie en autorisatie toobe meeberekend buiten uw de code.
* Azure Service Bus biedt een beveiligde berichten en gegevensstroom mogelijkheid voor gedistribueerd en hybride toepassingen, zoals communicatie tussen Azure gehoste toepassingen en on-premises toepassingen en services, zonder complexe firewall en beveiliging infrastructuren. Service Bus Relay gebruiken voor toepassingsbronnen toohello services die beschikbaar worden gesteld als eindpunten kunnen toohello behoren tenant (bijvoorbeeld buiten Hallo-systeem, bijvoorbeeld on-premises gehost) of ze misschien services die ingericht zijn specifiek voor Hallo tenant ( omdat gevoelige, tenant-specifieke gegevens passeert ze).

**Inrichting van Resources**

Azure biedt een aantal manieren inrichten van nieuwe tenants voor Hallo-toepassing. Voor multitenant-toepassingen met een groot aantal tenants, het is doorgaans nodig tooautomate dit proces door selfservice inrichting inschakelen.

* Werkrollen kunt u tooprovision en deactivering in te richten per tenant resources (zoals wanneer een nieuwe tenant tekenen-up of geannuleerd), verzamelen van meetgegevens over voor softwarelicentiecontrole gebruiken en beheren van de schaal na een bepaalde planning of in het antwoord toohello overschrijding van drempels van sleutel prestatie-indicatoren. Deze dezelfde rol kan ook worden gebruikt toopush updates en upgrades toohello-oplossing.
* Azure Blobs kunnen gebruikte tooprovision compute of vooraf geïnitialiseerd opslagbronnen voor nieuwe tenants en tegelijkertijd container toegangsniveau beleid tooprotect Hallo compute servicepakketten VHD-installatiekopieën en andere resources zijn.
* Opties voor het inrichten van SQL Database-resources voor een tenant zijn onder andere:
  
  * DDL in scripts of ingesloten als bronnen binnen de assembly's
  * SQL Server 2008 R2 DAC-pakketten via een programma wordt geïmplementeerd.
  * Kopiëren van een database master verwijzing
  * Met behulp van database importeren en exporteren tooprovision nieuwe databases uit een bestand.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
