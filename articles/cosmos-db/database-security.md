---
title: aaaDatabase security - Azure Cosmos DB | Microsoft Docs
description: Meer informatie over hoe Azure Cosmos DB biedt beveiliging en gegevens Databasebeveiliging voor uw gegevens.
keywords: nosql-database beveiliging, informatiebeveiliging, beveiliging van gegevens, versleuteling van de database, databasebeveiliging, beveiligingsbeleid, beveiliging testen
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: a02a6a82-3baf-405c-9355-7a00aaa1a816
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: mimig
ms.openlocfilehash: 85ffa62f611bfad00bf3fc5dbe536f91f97f1113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-database-security"></a>Beveiliging van Azure DB Cosmos-database

Dit artikel worden de aanbevolen beveiligingsprocedures voor database en de belangrijkste functies die worden aangeboden door Azure Cosmos DB toohelp u detecteren, voorkomen van en reageren toodatabase schendingen.
 
## <a name="whats-new-in-azure-cosmos-db-security"></a>Wat is nieuw in Azure DB die Cosmos-beveiliging?

Codering in rust is nu beschikbaar voor documenten en back-ups opgeslagen in Azure Cosmos DB in alle Azure-regio's. Codering in rust wordt automatisch toegepast op nieuwe en bestaande klanten in deze regio's. Er is geen tooconfigure nodig; hebt u dezelfde geweldige latentie, doorvoer, beschikbaarheid en functionaliteit Hallo zoals voordat voor Hallo voordeel van weten uw gegevens veilig en beveiligd met versleuteling in rust.

## <a name="how-do-i-secure-my-database"></a>Hoe worden mijn database kunt beveiligen? 

Beveiliging van gegevens is een gedeelde verantwoordelijkheid tussen u, Hallo klant en uw databaseprovider. Afhankelijk van het Hallo-databaseprovider die u kiest, kan Hallo hoeveelheid u blijven verantwoordelijkheid variëren. Als u een on-premises-oplossing kiest, moet u tooprovide alles van eindpunt beveiliging toophysical beveiliging van uw hardware - dit geen eenvoudige taak is. Als u een PaaS-cloud databaseprovider zoals Azure Cosmos DB kiest, wordt uw regio problematisch aanzienlijk verkleind. Hallo volgende afbeelding, van Microsoft geleend [gedeeld verantwoordelijkheden voor Cloud Computing](https://aka.ms/sharedresponsibility) witboek, ziet u hoe uw verantwoordelijkheid met een PaaS-provider, zoals Azure Cosmos DB afneemt.

![De verantwoordelijkheden van klant en database-provider](./media/database-security/nosql-database-security-responsibilities.png)

Hallo voorgaande diagram toont op hoog niveau cloud security-onderdelen, maar welke items u hoeven tooworry over specifiek voor uw databaseoplossing? En hoe kunt u andere oplossingen tooeach vergelijken? 

Het wordt aangeraden de Hallo controlelijst van vereisten op welke databasesystemen toocompare te volgen:

- Netwerkbeveiliging en firewall-instellingen
- Verificatie van gebruikers en fijnmazige gebruikersbesturingselementen
- Gegevens van de mogelijkheid tooreplicate globaal voor regionale fouten
- Mogelijkheid tooperform failovers van een data center tooanother
- Replicatie van de lokale gegevens binnen een datacentrum
- Automatische gegevensback-ups
- Herstellen van verwijderde gegevens vanuit back-ups
- Beveiligen en isoleren van gevoelige gegevens
- Bewaking voor aanvallen
- Tooattacks reageert
- Mogelijkheid toogeo fence gegevens tooadhere toodata governance beperkingen
- Fysieke beveiliging van servers in beveiligde datacenters

Hoewel het lijkt misschien duidelijk, recente [grootschalige database schendingen](http://thehackernews.com/2017/01/mongodb-database-security.html) herinneren ons Hallo eenvoudige maar kritiek belang van Hallo volgens de vereisten:
- Patches servers die worden bewaard van toodate
- HTTPS door standaard/SSL-versleuteling
- Beheerdersaccounts met sterke wachtwoorden

## <a name="how-does-azure-cosmos-db-secure-my-database"></a>Hoe Azure Cosmos DB mijn database beveiligen?

Bekijk terug Hallo voorafgaand aan de lijst - hoeveel van de beveiligingsvereisten Azure Cosmos DB biedt? Elke één een.

We gaan verdiepen in elk criterium in detail.

|Beveiligingsvereiste|Azure Cosmos-DB beveiliging benadering|
|---|---|---|
|Netwerkbeveiliging|Gebruik van een IP-firewall is Hallo eerste laag van beveiliging toosecure uw database. Azure Cosmos DB ondersteunt beleid IP gebaseerd toegangsbeheer voor binnenkomende firewallondersteuning aangestuurd. Hallo toegangsbeheer op basis van IP zijn vergelijkbaar toohello firewallregels die wordt gebruikt door traditionele databasesystemen, maar ze zijn uitgevouwen zodat Azure DB die Cosmos-databaseaccount alleen toegankelijk vanuit een goedgekeurde reeks machines of cloudservices is. <br><br>Azure Cosmos-database kunt u tooenable een specifiek IP-adres (168.61.48.0), een IP-adresbereik (168.61.48.0/8) en combinatie van IP-adressen en -bereiken. <br><br>Alle aanvragen die afkomstig zijn van computers buiten deze lijst met toegestane zijn geblokkeerd door Azure Cosmos DB. Aanvragen van goedgekeurd machines en cloudservices vervolgens Hallo verificatie proces toobe krijgt toegang tot besturingselement toohello bronnen moeten voltooien.<br><br>Meer informatie [Azure DB die Cosmos-firewallondersteuning](firewall-support.md).|
|Autorisatie|Azure Cosmos DB waarbij hash op basis van een message authenticatiecode (HMAC) voor autorisatie. <br><br>Elke aanvraag wordt gehasht met Hallo geheime sleutel en Hallo daaropvolgende base-64 gecodeerde hash bij elke aanroep tooAzure Cosmos DB verzonden. Hallo toovalidate aanvragen gebruikt Azure Cosmos DB Hallo Hallo juiste geheime sleutel en eigenschappen toogenerate een hash en vervolgens het Hallo-waarde met de Hallo Hallo aanvraag worden vergeleken. Als de twee waarden Hallo overeenkomen, Hallo bewerking met succes is geautoriseerd en Hallo-aanvraag wordt verwerkt, anders er is een Autorisatiefout en Hallo-aanvraag wordt afgewezen.<br><br>U kunt een gebruiken een [hoofdsleutel](secure-access-to-data.md#master-keys), of een [resource token](secure-access-to-data.md#resource-tokens) zodat fijnmazig toegang tooa resource zoals een document.<br><br>Meer informatie [toegang beveiligen tooAzure Cosmos DB resources](secure-access-to-data.md).|
|Gebruikers en machtigingen|Met behulp van Hallo [hoofdsleutel](#master-key) voor Hallo-account, kunt u Gebruikersbronnen en bronnen van de machtiging per database maken. Een [resource token](#resource-token) is gekoppeld aan een machtiging in een database en bepaalt of Hallo gebruiker toegang heeft (lezen / schrijven, alleen-lezen, of geen toegang) tooan toepassingsbron in Hallo-database. Toepassingsresources bevatten verzamelingen, documenten, bijlagen, opgeslagen procedures, triggers en UDF's. Hallo resource token wordt vervolgens gebruikt tijdens de verificatie tooprovide of weigeren van toegang toohello resource.<br><br>Meer informatie [toegang beveiligen tooAzure Cosmos DB resources](secure-access-to-data.md).|
|Active directory-integratie (RBAC)| U kunt ook toohello database toegangsaccount met behulp van toegangsbeheer (IAM) in hello Azure-portal opgeven, zoals weergegeven in Hallo schermafbeelding na deze tabel. IAM biedt toegangsbeheer op basis van rollen en kan worden geïntegreerd met Active Directory. U kunt ingebouwde rollen of aangepaste rollen voor personen en groepen zoals weergegeven in Hallo installatiekopie te volgen.|
|Globale replicatie|Azure Cosmos DB biedt klare globale distributie, waarmee u tooreplicate uw gegevens tooany een van de Azure wereldwijd datacenters met Hallo klikt u op een knop. Globale replicatie kunt u globaal worden geschaald en lage latentie toegang tooyour gegevens Hallo wereld bieden.<br><br>In de context van de Hallo van beveiliging, globale replicatie weet u zeker gegevensbeveiliging tegen regionale fouten.<br><br>Meer informatie [Distribueer gegevens globaal](distribute-data-globally.md).|
|Regionale failover|Als u uw gegevens in meer dan één datacenter zijn gerepliceerd, Azure Cosmos DB automatisch wordt getotaliseerd via uw bewerkingen moet een regionaal datacenter offline gaan. U kunt een geprioriteerde lijst met failover-regio's met behulp van Hallo regio's waar uw gegevens worden gerepliceerd. <br><br>Meer informatie [regionale Failovers in Azure Cosmos DB](regional-failover.md).|
|Lokale replicatie|Zelfs binnen één datacenter, repliceert Azure Cosmos DB automatisch gegevens voor hoge beschikbaarheid, geeft u de keuze van Hallo [consistentieniveaus](consistency-levels.md). Er wordt gegarandeerd dat een [99,99% beschikbaarheid beschikbaarheids-SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db) en wordt geleverd met een financiële garantie - iets er geen andere database-Services kan bieden.|
|Geautomatiseerde online back-ups|Azure DB Cosmos-databases worden regelmatig een back-up gemaakt en opgeslagen in een archief georedundant. <br><br>Meer informatie [automatische online back-up en herstel met Azure Cosmos DB](online-backup-and-restore.md).|
|Gegevens herstellen die zijn verwijderd|Hallo geautomatiseerde online back-ups kunnen worden gebruikt toorecover gegevens die u mogelijk per ongeluk hebt verwijderd van te ~ 30 dagen na Hallo-gebeurtenis. <br><br>Meer informatie [automatische online back-up en herstel met Azure Cosmos-DB](online-backup-and-restore.md)|
|Beveiligen en isoleren van gevoelige gegevens|Alle gegevens in Hallo regio's die worden vermeld in [wat is er nieuw?](#whats-new) nu in rust versleuteld.<br><br>PII en andere vertrouwelijke gegevens kunnen worden geïsoleerd toospecific verzamelingen en alleen-lezen of alleen-lezen toegang kan worden beperkt toospecific gebruikers.|
|Monitor voor aanvallen|Met behulp van het controlelogboek en activiteitenlogboeken, kunt u uw account voor normaal en abnormaal activiteit controleren. U kunt weergeven welke bewerkingen zijn uitgevoerd op uw resources die heeft Hallo-bewerking gestart wanneer het Hallo-bewerking heeft plaatsgevonden, Hallo status van Hallo bewerking, en nog veel meer zoals weergegeven in het Hallo-schermafbeelding onder deze tabel.|
|Tooattacks reageren|Zodra u hebt verbinding gemaakt met de ondersteuning van Azure tooreport bij een aanval, wordt een respons op incidenten 5-stap-proces gestart. Hallo doel van Hallo 5-proces is toorestore normale servicebeveiliging en werking zo snel mogelijk na een probleem wordt gedetecteerd en onderzoek is gestart.<br><br>Meer informatie [reactie van Microsoft Azure-beveiliging in Hallo Cloud](https://aka.ms/securityresponsepaper).|
|Geofencing|Azure Cosmos DB zorgt ervoor dat gegevens bestuur en naleving voor soevereine regio's (bijvoorbeeld Duitsland, China, ons Gov).|
|Beveiligde faciliteiten|Gegevens in Azure Cosmos-database is opgeslagen op SSD's in Azure beveiligde datacenters.<br><br>Meer informatie [globale datacenters van Microsoft](https://www.microsoft.com/en-us/cloud-platform/global-datacenters)|
|HTTPS/SSL/TLS-versleuteling|Alle client-naar-service Azure Cosmos DB interacties zijn SSL/TLS 1.2 afgedwongen. Alle intra datacenter en cross datacenter replicatie wordt ook SSL/TLS 1.2 afgedwongen.|
|Versleuteling 'at rest'|Alle gegevens die zijn opgeslagen in Azure Cosmos DB in rust versleuteld. Meer informatie [Azure DB die Cosmos-versleuteling in rust](.\database-encryption-at-rest.md)|
|Patches servers|Als de database van een beheerde elimineert Azure Cosmos DB Hallo nodig toomanage en patch-servers, die automatisch voor u heeft gedaan.|
|Beheerdersaccounts met sterke wachtwoorden|De vaste toobelieve we zelfs toomention moet deze vereiste, maar in tegenstelling tot enkele van onze concurrenten is het onmogelijk toohave een Administrator-account zonder een wachtwoord in Azure Cosmos DB.<br><br> Beveiliging via SSL en HMAC geheime gebaseerde verificatie is standaard uitbreidbaar standaard.|
|Beveiligings- en data protection certificeringen|Azure Cosmos DB heeft [ISO 27001](https://www.microsoft.com/en-us/TrustCenter/Compliance/ISO-IEC-27001), [Europese Model componenten (EUMC)](https://www.microsoft.com/en-us/TrustCenter/Compliance/EU-Model-Clauses), en [HIPAA](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) certificeringen. Extra certificaten worden uitgevoerd.|

Hallo volgende schermafbeelding ziet u Active directory-integratie (RBAC) met behulp van toegangsbeheer (IAM) in hello Azure-portal: ![toegangsbeheer (IAM) in hello Azure portal - beveiliging van de database te demonstreren](./media/database-security/nosql-database-security-identity-access-management-iam-rbac.png)

Hallo volgende schermafbeelding ziet u hoe u het controlelogboek en activiteit registreert toomonitor uw account: ![logboeken van de activiteit voor Azure Cosmos-DB](./media/database-security/nosql-database-security-application-logging.png)

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over hoofdsleutels en resource tokens [Securing access tooAzure Cosmos DB gegevens](secure-access-to-data.md).

Zie voor meer informatie over Microsoft certificeringen [Azure Vertrouwenscentrum](https://azure.microsoft.com/support/trust-center/).
