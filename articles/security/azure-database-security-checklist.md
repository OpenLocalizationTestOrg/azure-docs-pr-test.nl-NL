---
title: Controlelijst voor de beveiliging van de aaaAzure database | Microsoft Docs
description: In dit artikel biedt een reeks controlelijst voor beveiliging van de Azure-database.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 5e3a69591df3c8508a8707a2d47068342863ce93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-security-checklist"></a>Controlelijst voor de beveiliging van de Azure-database

toohelp betere beveiliging, Azure-Database bevat een aantal ingebouwde beveiligingsmechanismen toolimit gebruiken en toegangsbeheer.

Deze omvatten:

-   Een firewall waarmee u toocreate [firewall-regels](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) connectiviteit beperken door IP-adres
-   Niveau van de Server firewall toegankelijk is vanaf hello Azure-portal
-   Firewallregels voor databaseniveau toegankelijk is vanaf SSMS
-   Beveiligde verbindingen tooyour-database met de beveiligde verbindingsreeksen
-   Toegangsbeheer gebruiken
-   Gegevensversleuteling
-   Controle van SQL-Database
-   Detectie van dreigingen SQL-Database

## <a name="introduction"></a>Inleiding
Cloud computing nieuwe beveiliging paradigma's die gebruikers van de toepassing niet bekend toomany, databasebeheerders en programmeurs vereist. Als gevolg hiervan zijn sommige organisaties terughoudend tooimplement een cloudinfrastructuur voor gegevensbeheer vanwege tooperceived beveiligingsrisico's. Veel van dit probleem kan echter worden ondervangen via een beter begrip van beveiligingsfuncties Hallo ingebouwd in Microsoft Azure en Microsoft Azure SQL Database.

## <a name="checklist"></a>Controlelijst
Het is raadzaam dat u Hallo leest [Azure Security Best Practices](https://docs.microsoft.com/en-us/azure/security/azure-database-security-best-practices) artikel voorafgaande tooreviewing deze controlelijst. U zult kunnen tooget Hallo optimaal gebruik van deze controlelijst als u de aanbevolen procedures Hallo begrijpt. Vervolgens kunt u deze controlelijst toomake zeker dat u Hallo belangrijke problemen in Azure databasebeveiliging hebt verholpen.


|Controlelijst categorie| Beschrijving|
| ------------ | -------- |
|**Gegevens beveiligen**||
| <br> Codering in beweging/doorvoer| <ul><li>[Transport Layer Security](https://docs.microsoft.com/en-us/windows-server/security/tls/transport-layer-security-protocol), om gegevens te coderen wanneer gegevens worden verplaatst toohello netwerken.</li><li>Database vereist een beveiligde communicatie van clients op basis van Hallo [TDS (Tabular Data Stream)](https://msdn.microsoft.com/en-in/library/dd357628.aspx) protocol via TLS (Transport Layer Security).</li></ul> |
|<br>Versleuteling 'at rest'| <ul><li>[Met transparante gegevensversleuteling](http://go.microsoft.com/fwlink/?LinkId=526242)wanneer inactieve gegevens fysiek worden opgeslagen in een digitale vorm.</li></ul>|
|**Toegang beheren**||  
|<br> Toegang tot de database | <ul><li>[Verificatie](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) (Azure Active Directory-verificatie) AD-verificatie wordt gebruikgemaakt van identiteiten die worden beheerd door Azure Active Directory.</li><li>[Autorisatie](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-control-access) verlenen gebruikers Hallo minimaal benodigde bevoegdheden nodig zijn.</li></ul> |
|<br>Toegang tot toepassingen| <ul><li>[Rij level Security](https://msdn.microsoft.com/library/dn765131) (met behulp van beveiligingsbeleid op Hallo hetzelfde moment rijniveau toegang beperken op basis van de identiteit, rol of uitvoering context van een gebruiker).</li><li>[Dynamische-Gegevensmaskering](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dynamic-data-masking-get-started) (met behulp van machtiging & beleid beperkt blootstelling van gevoelige gegevens door te maskeren deze toonon beheerdersmogelijkheden)</li></ul>|
|**Proactieve controle**||  
| <br>Bijhouden & detecteren| <ul><li>[Controle](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing) houdt databasegebeurtenissen en schrijft deze tooan controlelogboek / activiteit log in uw [Azure Storage-account](https://docs.microsoft.com/en-us/azure/storage/storage-create-storage-account).</li><li>Gebruik van track Azure Database health [Azure Monitor activiteitenlogboeken](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs).</li><li>[Bedreigingendetectie](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-threat-detection) worden afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met gedetecteerd. </li></ul> |
|<br>Azure Security Center| <ul><li>[Bewaking van de gegevens](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-auditing-on-sql-databases) Azure Security Center gebruiken als een oplossing voor een gecentraliseerde veiligheidscontrole voor SQL en andere Azure-services.</li></ul>|     

## <a name="conclusion"></a>Conclusie
Azure-Database is een databaseplatform robuuste met een volledige reeks beveiligingsfuncties die voldoen aan veel organisatie- en regelgeving nalevingsvereisten. U kunt eenvoudig gegevens beveiligen door Hallo fysieke toegang tot tooyour gegevens beheren en het gebruik van een groot aantal opties voor beveiliging van gegevens op het Hallo file-, kolom- of met transparante gegevensversleuteling, -Celcodering of beveiliging op rijniveau. Altijd kan versleutelde ook bewerkingen op gecodeerde gegevens van toepassingsupdates hello vereenvoudigen. Op zijn beurt toegang tooauditing logboeken van de activiteit van de SQL-Database biedt u Hallo informatie die u nodig hebt, zodat u tooknow hoe en wanneer gegevens worden geopend.

## <a name="next-steps"></a>Volgende stappen
U kunt de beveiliging van uw database tegen kwaadwillende gebruikers of onbevoegde toegang met een paar eenvoudige stappen Hallo verbeteren. In deze zelfstudie leert u naar:

- Instellen van [firewall-regels](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-firewall-configure) voor de server en of de database.
- Uw gegevens beschermen met [versleuteling](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/sql-server-encryption).
- Schakel [SQL Database auditing](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing).

