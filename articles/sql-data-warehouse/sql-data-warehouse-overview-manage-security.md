---
title: een database in SQL Data Warehouse aaaSecure | Microsoft Docs
description: Tips voor het beveiligen van een database in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 8fa2f5ca-4cf5-4418-99a2-4dc745799850
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 5ef4d760e00be46bfe7808bc95dbe1e4b3a51165
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-database-in-sql-data-warehouse"></a>Een database in SQL Data Warehouse beveiligen
> [!div class="op_single_selector"]
> * [Overzicht van beveiliging](sql-data-warehouse-overview-manage-security.md)
> * [Verificatie](sql-data-warehouse-authentication.md)
> * [Versleuteling (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Versleuteling (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

In dit artikel wordt uitgelegd Hallo basisprincipes van beveiliging van uw Azure SQL Data Warehouse-database. In het bijzonder in dit artikel krijgt u aan de slag met resources voor het beperken van toegang tot gegevens beveiligen en het controleren van activiteiten in een database.

## <a name="connection-security"></a>Verbindingsbeveiliging
Verbindingsbeveiliging verwijst toohow u beperken en beveiligde verbindingen tooyour database met behulp van de firewall-regels en versleutelde verbinding.

Firewall-regels worden gebruikt door beide Hallo-server en Hallo database tooreject verbindingspogingen van IP-adressen die niet expliciet wilt plaatsen zijn. tooallow verbindingen van uw toepassing of het openbare IP-adres client-computer, moet u eerst een firewallregel op serverniveau met hello Azure Portal, REST-API of PowerShell maken. U moet als een best practice Hallo IP-adresbereiken toegestaan via de firewall van uw server zoveel mogelijk beperken.  tooaccess Azure SQL Data Warehouse vanaf uw lokale computer, zorg ervoor dat het Hallo-firewall op uw netwerk en de lokale computer staat uitgaande communicatie op TCP-poort 1433.  Zie voor meer informatie [Azure SQL Database-firewall][Azure SQL Database firewall], [sp_set_firewall_rule][sp_set_firewall_rule], en [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Verbindingen tooyour SQL Data Warehouse zijn standaard versleuteld.  Wijzigen van de verbinding instellingen toodisable versleuteling worden genegeerd.

## <a name="authentication"></a>Authentication
Verificatie verwijst toohow u uw identiteit bewijzen bij het verbinden van toohello database. SQL Data Warehouse biedt momenteel ondersteuning voor SQL Server-verificatie met een gebruikersnaam en wachtwoord en een Azure Active Directory. 

Wanneer u de logische server Hallo voor uw database gemaakt, moet u een aanmelding 'serverbeheerder' met een gebruikersnaam en wachtwoord opgegeven. U kunt tooany database op die server als de database-eigenaar Hallo of 'dbo' via SQL Server-verificatie met behulp van deze referenties verifiëren.

Echter moeten, als een best practice gebruikers van uw organisatie gebruiken een ander account tooauthenticate. Op deze manier kunt u Hallo machtigingen verleend toohello toepassing beperken en verminderen het Hallo risico's van schadelijke activiteiten voor het geval de toepassingscode kwetsbaar tooa SQL-injectieaanvallen is. 

SQL-Server geverifieerde gebruiker, toocreate verbinding toohello **master** database op de server met uw aanmeldgegevens van serverbeheerder en maak een nieuwe server-aanmelding.  Bovendien is een goed idee toocreate een gebruiker in de hoofddatabase Hallo voor gebruikers van Azure SQL Data Warehouse. Maken van een gebruiker in master, kunt een gebruiker toologin met hulpmiddelen zoals SSMS zonder een databasenaam opgeven.  Ook kunnen ze toouse Hallo object explorer tooview alle databases op een SQL-server.

```sql
-- Connect toomaster database and create a login
CREATE LOGIN ApplicationLogin WITH PASSWORD = 'Str0ng_password';
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Sluit tooyour **SQL Data Warehouse-database** met uw aanmeldgegevens van serverbeheerder en maak een databasegebruiker op basis van de server-aanmelding Hallo u zojuist hebt gemaakt.

```sql
-- Connect tooSQL DW database and create a database user
CREATE USER ApplicationUser FOR LOGIN ApplicationLogin;
```

Als een gebruiker aanvullende bewerkingen doen gaat zoals het maken van aanmeldingen of nieuwe databases te maken, moet deze ook toobe toegewezen toohello `Loginmanager` en `dbmanager` rollen in de hoofddatabase Hallo. Zie voor meer informatie over deze extra functies en verifiërende tooa SQL-Database [databases en aanmeldingen in Azure SQL Database beheren][Managing databases and logins in Azure SQL Database].  Zie voor meer informatie over Azure AD voor SQL Data Warehouse [tooSQL Data Warehouse door met behulp van Azure Active Directory-verificatie verbinding te maken][Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication].

## <a name="authorization"></a>Autorisatie
Autorisatie verwijst toowhat kunt u doen in een Azure SQL Data Warehouse-database, en dit wordt bepaald door uw gebruikersaccount rollidmaatschappen en machtigingen. Als een best practice moet u gebruikers Hallo verlenen minimaal benodigde bevoegdheden nodig zijn. Azure SQL Data Warehouse maakt deze eenvoudig toomanage aan rollen in T-SQL:

```sql
EXEC sp_addrolemember 'db_datareader', 'ApplicationUser'; -- allows ApplicationUser tooread data
EXEC sp_addrolemember 'db_datawriter', 'ApplicationUser'; -- allows ApplicationUser toowrite data
```

Hallo beheerder serveraccount die u verbinding met maakt is lid van db_owner autoriteit toodo met Alles binnen het Hallo-database. Gebruik dit account voor het implementeren van schema-updates en andere beheerbewerkingen. Hallo 'ApplicationUser' account gebruiken met meer beperkte machtigingen tooconnect uit de database van uw toepassing toohello Hello minimaal benodigde bevoegdheden die nodig is voor uw toepassing.

Er zijn manieren toofurther limiet wat een gebruiker kan doen met Azure SQL Database:

* Gedetailleerde [machtigingen] [ Permissions] kunt u beheren welke bewerkingen kunt u op afzonderlijke kolommen, tabellen, weergaven, procedures en andere objecten in Hallo-database. Gebruik gedetailleerde machtigingen toohave Hallo meeste controle en verleen Hallo minimale machtigingen nodig. Hallo gedetailleerde machtiging system is erg ingewikkeld en waarvoor sommige toouse onderzoek effectief.
* [Databaserollen] [ Database roles] andere dan db_datareader en db_datawriter kunnen gebruikte toocreate krachtiger gebruikersaccounts van de toepassing of minder krachtige de accounts. Hallo ingebouwde vaste databaserollen bieden een eenvoudige manier toogrant machtigingen, maar kunnen ertoe leiden dat meer machtigingen worden dan nodig zijn.
* [Opgeslagen procedures] [ Stored procedures] gebruikte toolimit Hallo-acties die kunnen worden uitgevoerd op Hallo-database kan worden.

Databases en logische servers beheren vanaf Hallo klassieke Azure-Portal of met behulp van hello Azure Resource Manager-API wordt bepaald door uw portal gebruikersaccount roltoewijzingen. Zie voor meer informatie over dit onderwerp [toegangsbeheer op basis van rollen in Azure Portal][Role-based access control in Azure Portal].

## <a name="encryption"></a>Versleuteling
Azure SQL Data Warehouse transparante gegevens codering (TDE) beschermt tegen Hallo dreiging van schadelijke activiteiten door realtime versleuteling en ontsleuteling van uw gegevens in rust in te voeren.  Bij het versleutelen van uw database, worden gekoppelde back-ups en transactielogboekbestanden versleuteld zonder wijzigingen tooyour toepassingen. TDE versleutelt Hallo opslag van een volledige database met behulp van een symmetrische sleutel opgeroepen Hallo databaseversleutelingssleutel. In SQL-Database is Hallo databaseversleutelingssleutel beveiligd met een ingebouwde servercertificaat. ingebouwde Hallo-servercertificaat is uniek voor elke SQL-Database-server. Microsoft draait automatisch deze certificaten ten minste om de 90 dagen. Hallo-versleutelingsalgoritme die wordt gebruikt door SQL Data Warehouse is AES-256. Zie voor een algemene beschrijving van TDE [Transparent Data Encryption][Transparent Data Encryption].

U kunt de database met de Hallo versleutelen [Azure Portal] [ Encryption with Portal] of [T-SQL][Encryption with TSQL].

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie en voorbeelden voor het verbinden van tooyour SQL Data Warehouse met verschillende protocollen [tooSQL datawarehouse verbinding][Connect tooSQL Data Warehouse].

<!--Image references-->

<!--Article references-->
[Connect tooSQL Data Warehouse]: ./sql-data-warehouse-connect-overview.md
[Encryption with Portal]: ./sql-data-warehouse-encryption-tde.md
[Encryption with TSQL]: ./sql-data-warehouse-encryption-tde-tsql.md
[Connecting tooSQL Data Warehouse By Using Azure Active Directory Authentication]: ./sql-data-warehouse-authentication.md

<!--MSDN references-->
[Azure SQL Database firewall]: https://msdn.microsoft.com/library/ee621782.aspx
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx
[Database roles]: https://msdn.microsoft.com/library/ms189121.aspx
[Managing databases and logins in Azure SQL Database]: https://msdn.microsoft.com/library/ee336235.aspx
[Permissions]: https://msdn.microsoft.com/library/ms191291.aspx
[Stored procedures]: https://msdn.microsoft.com/library/ms190782.aspx
[Transparent Data Encryption]: https://msdn.microsoft.com/library/bb934049.aspx
[Azure portal]: https://portal.azure.com/

<!--Other Web references-->
[Role-based access control in Azure Portal]: https://azure.microsoft.com/documentation/articles/role-based-access-control-configure
