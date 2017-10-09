---
title: aaaResolving T-SQL verschillen-migratie-Azure SQL Database | Microsoft Docs
description: Transact-SQL-instructies die minder dan volledig worden ondersteund in Azure SQL Database
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: c05abd9e-28a7-4c97-9bdf-bc60d08fc92e
ms.service: sql-database
ms.custom: load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 03/17/2017
ms.author: rickbyh
ms.openlocfilehash: 3852013338bfdc6c7da9d1d879c54781682bc635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resolving-transact-sql-differences-during-migration-toosql-database"></a>Transact-SQL-verschillen tijdens migratie tooSQL Database oplossen   
Wanneer [migreren van uw database](sql-database-cloud-migrate.md) van SQL Server tooAzure SQL Server, ontdekt u mogelijk de database moeten sommige herstructureren voordat Hallo SQL Server kunnen worden gemigreerd. Dit onderwerp bevat richtlijnen tooassist u in zowel het uitvoeren van deze herstructureren en kennis Hallo redenen waarom onderliggende hello herstructureren nodig is. compatibiliteitsproblemen toodetect, gebruik Hallo [gegevens migratie-assistent (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).

## <a name="overview"></a>Overzicht
De meeste Transact-SQL-functies die gebruikmaken van toepassingen worden volledig ondersteund in Microsoft SQL Server en Azure SQL Database. Hallo bijvoorbeeld SQL kernonderdelen zoals gegevenstypen, operators, string, rekenkundig logische, en functies van de cursor, werken identiek in SQL Server en SQL-Database. Er zijn echter enkele TSQL-verschillen in DDL (data definition language) en (gegevens manipulatie language) van de DML-elementen waardoor T-SQL-instructies en query's die worden slechts gedeeltelijk ondersteund (die bespreken we verderop in dit onderwerp).

Bovendien worden sommige functies en syntaxis die niet wordt ondersteund op alle omdat Azure SQL Database ontworpen tooisolate functies van afhankelijkheden van de hoofddatabase Hallo en het Hallo-besturingssysteem. De meeste serverniveau activiteiten zijn als zodanig niet geschikt voor SQL-Database. Opties en T-SQL-instructies zijn niet beschikbaar als ze serverniveau opties, de onderdelen van het besturingssysteem configureren, of geef configuratie bestandssysteem. Als er dergelijke mogelijkheden zijn vereist, is vaak een geschikt alternatief beschikbaar zijn in een andere manier van SQL-Database of van een andere Azure-functie of service. 

Hoge beschikbaarheid is bijvoorbeeld ingebouwd in Azure, dus configureren AlwaysOn niet nodig is (Hoewel u tooconfigure actieve geo-replicatie voor sneller herstel in geval van een noodgeval Hallo wilt mogelijk). T-SQL-instructies verwante dus tooavailability groepen worden niet ondersteund door SQL-Database en Hallo dynamische Beheerweergave weergaven gerelateerde tooAlways op worden ook niet ondersteund.

Zie voor een lijst met Hallo-functies die worden ondersteund en worden niet ondersteund door SQL-Database, [vergelijking van functies van Azure SQL Database](sql-database-features.md). Hallo-lijst op deze pagina is een aanvulling op dat onderwerp richtlijnen en functies en legt de nadruk op Transact-SQL-instructies.

## <a name="transact-sql-syntax-statements-with-partial-differences"></a>Transact-SQL-syntaxis instructies met gedeeltelijke verschillen
Hallo core DDL (data definition language)-instructies zijn beschikbaar, maar sommige DDL-componenten extensies gerelateerde toodisk plaatsing en niet-ondersteunde functies. 

- MAKEN en ALTER DATABASE instructies hebben meer dan drie dozijn opties. Hallo-instructies zijn plaatsing van bestanden, FILESTREAM en opties van service broker voor die Server tooSQL alleen van toepassing. Dit mogelijk niet van belang als u databases maakt voordat u migreert, maar als u migreert T-SQL-code die databases maakt moet u vergelijken [CREATE DATABASE (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) met SQL Server op Hallo syntax [maken DATABASE (SQL Server Transact-SQL)](https://msdn.microsoft.com/library/ms176061.aspx) toomake ervoor dat alle Hallo opties waarmee u worden ondersteund. CREATE DATABASE voor Azure SQL Database beschikt ook over servicedoelstelling en elastisch schalingsopties die van toepassing zijn alleen tooSQL Database.
- Hallo maken en ALTER TABLE-instructies hebben bestandstabel opties op de SQL-Database kunnen niet worden gebruikt omdat FILESTREAM wordt niet ondersteund.
- MAKEN en ALTER login-instructies worden ondersteund, maar SQL-Database biedt niet alle Hallo-opties. uw meer draagbare database SQL-Database worden gebruikers aangemoedigd met behulp van toomake opgenomen databasegebruikers in plaats van aanmeldingen indien mogelijk. Zie voor meer informatie [CREATE/ALTER LOGIN](https://msdn.microsoft.com/library/ms189828.aspx) en [beheren en het verlenen van toegang tot de database](https://docs.microsoft.com/azure/sql-database/sql-database-manage-logins).

## <a name="transact-sql-syntax-not-supported-in-sql-database"></a>De Transact-SQL-syntaxis wordt niet ondersteund in SQL Database   
Bovendien tooTransact-SQL-instructies gerelateerde toohello van niet-ondersteunde functies beschreven in [vergelijking van functies van Azure SQL Database](sql-database-features.md), Hallo-instructies en groepen van de instructies, worden niet ondersteund. Als zodanig of uw database toobe gemigreerd wordt gebruikt voor geen van de volgende Hallo opnieuw samenstellen uw tooeliminate T-SQL-functies, deze functies van T-SQL en instructies.

- Systeemobjecten sorteren
- Aan verbindingen gerelateerd: eindpuntinstructies, `ORIGINAL_DB_NAME`. SQL-Database biedt geen ondersteuning voor Windows-verificatie, maar ondersteuning biedt voor Hallo vergelijkbare Azure Active Directory-verificatie. Sommige verificatietypen vereisen Hallo meest recente versie van SSMS. Zie voor meer informatie [verbinding maakt met tooSQL Database of SQL Data Warehouse door met behulp van Azure Active Directory-verificatie](sql-database-aad-authentication.md).
- Databaseoverschrijdende query’s met drie of vier onderdeelnamen. (Alleen-lezen query’s die databaseoverschrijdend zijn worden ondersteund dankzij [elastische databasequery’s](sql-database-elastic-query-overview.md).)
- Databaseoverschrijdend het eigendom koppelen, instelling `TRUSTWORTHY`
- `DATABASEPROPERTY` Gebruik in plaats daarvan `DATABASEPROPERTYEX`.
- `EXECUTE AS LOGIN` Gebruik in plaats daarvan 'EXECUTE AS USER'.
- Versleuteling wordt ondersteund, behalve voor Extensible Key Management
- Eventing: Gebeurtenissen, meldingen van gebeurtenissen, querymeldingen
- Plaatsing van bestanden: syntaxis gerelateerde toodatabase bestandsplaatsing, grootte en databasebestanden die automatisch worden beheerd door Microsoft Azure.
- Hoge beschikbaarheid: syntaxis gerelateerde toohigh beschikbaarheid, die wordt beheerd via uw Microsoft Azure-account. Dit omvat syntaxis voor back-ups, herstellen, Always On, databasespiegeling, de back-upfunctie voor logboekbestanden en herstelmodi.
- Meld u lezer: syntaxis die is afhankelijk van de logboekweergave hello, die niet beschikbaar op SQL-Database: Push-replicatie, Change Data Capture. SQL Database kan abonnee zijn op een artikel over push-replicatie.
- Functies: `fn_get_sql`, `fn_virtualfilestats`, `fn_virtualservernodes`
- Algemene tijdelijke tabellen
- Hardware: Syntaxis gerelateerde toohardware-gerelateerde serverinstellingen: zoals geheugen, werkthreads, CPU-affiniteit, trace vlaggen. Gebruik in plaats daarvan serviceniveaus.
- `HAS_DBACCESS`
- `KILL STATS JOB`
- `OPENQUERY`, `OPENROWSET`, `OPENDATASOURCE`, en vierdelige namen
- .NET framework: CLR-integratie met SQL Server
- Semantische zoekopdrachten
- Referenties voor server: Gebruik [database binnen het bereik van referenties](https://msdn.microsoft.com/library/mt270260.aspx) in plaats daarvan.
- Items op serverniveau: serverrollen, `IS_SRVROLEMEMBER`, `sys.login_token`. `GRANT`, `REVOKE`, en `DENY` van de machtigingen op serverniveau zijn niet beschikbaar, hoewel enkele hiervan worden vervangen door machtigingen op databaseniveau. Sommige handige DMV’s op serverniveau hebben vergelijkbare DMV’s op databaseniveau.
- `SET REMOTE_PROC_TRANSACTIONS`
- `SHUTDOWN`
- `sp_addmessage`
- `sp_configure`-opties en `RECONFIGURE`. Sommige opties zijn beschikbaar met [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).
- `sp_helpuser`
- `sp_migrate_user_to_contained`
- SQL ServerAgent: De syntaxis van de die van de Hallo SQL Server Agent of Hallo MSDB-database gebruikmaken: waarschuwingen, operators, Centraal beheer-servers. Gebruik in plaats daarvan opties voor scripts, zoals Azure PowerShell.
- SQL Server audit: Gebruik SQL Database auditing in plaats daarvan.
- SQL Server-tracering
- Trace-vlaggen: sommige items zijn traceringsvlag toocompatibility modi verplaatst.
- Transact-SQL-foutopsporing
- Triggers: triggers binnen het serverbereik of aanmeldingstriggers
- `USE`de instructie: toochange Hallo database context tooa andere database, moet u een nieuwe verbinding toohello nieuwe database maken.

## <a name="full-transact-sql-reference"></a>Volledige naslaginformatie voor Transact-SQL
Zie [Naslaginformatie voor Transact-SQL (database-engine)](https://msdn.microsoft.com/library/bb510741.aspx) in SQL Server Books Online voor meer informatie over Transact-SQL-grammatica, -gebruik en -voorbeelden. 

### <a name="about-hello-applies-to-tags"></a>Over Hallo 'Is van toepassing op' tags
Hallo Transact-SQL-naslaginformatie bevat onderwerpen over verwante tooSQL Server versies 2008 toohello aanwezig. Onder Hallo onderwerptitel is een Pictogrammenbalk en aanbieding Hallo vier SQL Server-platforms die duiden toepasbaarheid. Beschikbaarheidsgroepen zijn bijvoorbeeld geïntroduceerd in SQL Server 2012. De [AVAILABILTY groep maken](https://msdn.microsoft.com/library/ff878399.aspx) onderwerp geeft aan dat de instructie Hallo toepast op **SQL-Server (te beginnen met 2012)**. Hallo-instructie is niet van toepassing tooSQL Server 2008, SQL Server 2008 R2, Azure SQL Database, Azure SQL Data Warehouse of Parallel Data Warehouse.

In sommige gevallen Hallo algemeen onderwerp van een onderwerp in een product kan worden gebruikt, maar er zijn kleine verschillen tussen producten. Hallo verschillen worden aangegeven op middelpunten in Hallo onderwerp naar gelang van toepassing. In sommige gevallen Hallo algemeen onderwerp van een onderwerp in een product kan worden gebruikt, maar er zijn kleine verschillen tussen producten. Hallo verschillen worden aangegeven op middelpunten in Hallo onderwerp naar gelang van toepassing. Bijvoorbeeld is Hallo CREATE TRIGGER onderwerp beschikbaar in SQL-Database. Maar Hallo **alle SERVER** optie voor het niveau van de server-triggers, geeft aan dat het niveau van de server-triggers kunnen niet worden gebruikt in SQL-Database. Gebruik in plaats daarvan databaseniveau triggers.

## <a name="next-steps"></a>Volgende stappen

Zie voor een lijst met Hallo-functies die worden ondersteund en worden niet ondersteund door SQL-Database, [vergelijking van functies van Azure SQL Database](sql-database-features.md). Hallo-lijst op deze pagina is een aanvulling op dat onderwerp richtlijnen en functies en legt de nadruk op Transact-SQL-instructies.

