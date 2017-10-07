---
title: aaaCreate & Azure SQL-servers & databases beheren | Microsoft Docs
description: Meer informatie over Azure SQL Database-server en database-concepten en over het maken en beheren van servers en -databases via hello Azure-portal, PowerShell hello Azure CLI, Transact-SQL en Hallo REST-API.
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 0f526e388a5a620349f5a14e8d57a8355ac451ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-sql-database-servers-and-databases"></a>Azure SQL Database-servers en databases maken en beheren

Een Azure SQL database is een beheerde database in Microsoft Azure die is gemaakt binnen een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) met een gedefinieerde set [berekenings- en bronnen voor verschillende werkbelastingen](sql-database-service-tiers.md). Een Azure SQL database is gekoppeld aan een logische Azure SQL Database-server op, die wordt gemaakt binnen een specifieke Azure-regio. 

## <a name="an-azure-sql-database-can-be-a-single-pooled-or-partitioned-database"></a>Een Azure SQL database kan zowel een enkele, gegroepeerde of gepartitioneerde database

Een Azure SQL database kan zijn:

- Een individuele database met een [eigen set resources](sql-database-what-is-a-dtu.md#what-are-database-transaction-units-dtus) (DTU's)
- Onderdeel van een [elastische SQL-groep](sql-database-elastic-pool.md) die [deelt van een set resources](sql-database-what-is-a-dtu.md#what-are-elastic-database-transaction-units-edtus) (edtu's)
- Een onderdeel van een set [uitgeschaalde Shard-databases](sql-database-elastic-scale-introduction.md#horizontal-and-vertical-scaling), welke individuele databases of databases in een groep kunnen zijn
- Een onderdeel van een set databases die deel uitmaken van een [SaaS-ontwerppatroon met meerdere tenants](sql-database-design-patterns-multi-tenancy-saas-applications.md), waarvan de databases individuele databases of een databases in een groep (of beide) kunnen zijn 

> [!TIP]
> Zie [Database-id's](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) voor geldige databasenamen. 
>
 
- Hallo standaarddatabasesortering die wordt gebruikt door Microsoft Azure SQL Database is **SQL_LATIN1_GENERAL_CP1_CI_AS**, waarbij **LATIN1_GENERAL** Engels (Verenigde Staten), **CP1** codetabel 1252, is **CI** is niet hoofdlettergevoelig, en **AS** accentgevoelig is. Zie voor meer informatie over hoe tooset sortering Hallo [COLLATE (Transact-SQL)](https://msdn.microsoft.com/library/ms184391.aspx).
- Microsoft Azure SQL Database ondersteunt tabular data stream (TDS)-protocol clientversie 7.3 of hoger.
- Alleen TCP/IP-verbindingen zijn toegestaan.

## <a name="what-is-an-azure-sql-logical-server"></a>Wat is een logische Azure SQL-server?

Een logische server fungeert als een administratieve middelpunt voor meerdere databases, met inbegrip van [SQL elastische pools](sql-database-elastic-pool.md) [aanmeldingen](sql-database-manage-logins.md), [firewall-regels](sql-database-firewall-configure.md), [controle regels](sql-database-auditing.md), [dreiging beleidsregels](sql-database-threat-detection.md), en [failover groepen](sql-database-geo-replication-overview.md). Een logische server kan zich in een andere regio dan de resourcegroep. Hallo logische server moet bestaan voordat u kunt hello Azure SQL database maken. Alle databases op een server worden gemaakt binnen Hallo dezelfde regio bevinden als Hallo logische server. 


> [!IMPORTANT]
> In SQL-Database is een server een logische constructie die verschilt van een SQL Server-exemplaar dat u mogelijk kent met in Hallo lokale wereld. In het bijzonder Hallo SQL Database-service maakt geen garanties met betrekking tot de locatie van het Hallo-databases in de relatie tootheir logische servers en beschrijft geen instantieniveau toegang of functies.
> 

Wanneer u een logische server maakt, Geef een beheerserver aanmeldingsaccount en het wachtwoord heeft beheerdersrechten toohello master-database op die server en alle databases die zijn gemaakt op die server. Dit eerste account is een SQL-aanmeldings-account. Azure SQL Database ondersteunt SQL-verificatie en Azure Active Directory-verificatie voor verificatie. Zie voor informatie over aanmeldingen en verificatie, [het beheren van Databases en aanmeldingen in Azure SQL Database](sql-database-manage-logins.md). Windows-verificatie wordt niet ondersteund. 

> [!TIP]
> Zie voor een geldige groep en server Resourcenamen [naamgeving van regels en beperkingen](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).
>

Een logische server met Azure Database:

- Binnen een Azure-abonnement is gemaakt, maar kan worden verplaatst met het abonnement van de tooanother ingesloten bronnen
- Hallo resource bovenliggende voor de databases en elastische pools datawarehouses
- Biedt een naamruimte voor de databases en elastische pools datawarehouses
- Een logische container met sterke levensduur semantiek - verwijderen wordt verwijderd van een server en het is Hallo ingesloten databases en elastische pools datawarehouses
- Maakt deel uit van [Azure op rollen gebaseerde toegangsbeheer (RBAC)](/active-directory/role-based-access-control-what-is) -databases en elastische pools datawarehouses binnen een server toegangsrechten van Hallo server overnemen
- Is een hogere-element van Hallo identiteit van de databases en elastische pools datawarehouses voor Azure resource management-toepassing (Zie Hallo URL-schema voor de databases en pools)
- Groepeert resources in een regio
- Biedt een verbindingseindpunt voor databasetoegang (<serverName>.database.windows.net)
- Biedt toegang tot toometadata met betrekking tot ingesloten bronnen via DMV's door de verbindende tooa hoofddatabase 
- Biedt Hallo bereik voor management-beleidsregels die toepassing tooits databases - aanmeldingen, firewall-, controleren, dreiging detectie, enz. 
- Wordt beperkt door een quotum binnen Hallo bovenliggende abonnement (zes servers per abonnement standaard - [Zie abonnement hier beperkt](../azure-subscription-service-limits.md))
- Hallo-bereik voor databasequotum en DTU-quotum biedt voor Hallo resources (zoals 45.000 DTU bevat)
- Hallo bereik versioning voor mogelijkheden ingeschakeld op ingesloten bronnen 
- Hoofdaanmeldingen op serverniveau kunnen alle databases op een server beheren
- Kan aanmeldingen bevatten vergelijkbaar toothose in exemplaren van SQL Server on-premises dat krijgen toegang tooone of meer databases op Hallo-server en kunnen worden verleend beperkte beheerdersrechten. Zie [Aanmeldingen](sql-database-manage-logins.md) voor meer informatie.

## <a name="azure-sql-databases-protected-by-sql-database-firewall"></a>Azure SQL databases hebt beveiligd met SQL Database-firewall

toohelp beschermt uw gegevens een [SQL Database-firewall](sql-database-firewall-configure.md) voorkomt u dat alle toegang tooyour database-server of een van de databases van buiten uw server verbinding toohello rechtstreeks via de verbinding van uw Azure-abonnement. tooenable aanvullende connectiviteit, moet u [maken van een of meer firewallregels](sql-database-firewall-configure.md#creating-and-managing-firewall-rules). Zie voor het maken en beheren van de elastische pools SQL, [elastische pools](sql-database-elastic-pool.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-portal"></a>Azure SQL-servers, databases en firewalls met hello Azure-portal beheren

U kunt hello Azure SQL database resourcegroep tevoren of tijdens het maken van Hallo-server zelf maken. Er zijn meerdere methoden voor het ophalen van tooa nieuw SQL serverformulier door het maken van een nieuwe SQL-server of als onderdeel van het maken van een nieuwe database. 

### <a name="create-a-blank-sql-server-logical-server"></a>Maak een lege SQL-server (logische server)

een Azure SQL Database-server (zonder een database) met toocreate Hallo [Azure-portal](https://portal.azure.com), navigeer tooa leeg SQL server (logische server) formulier. Hallo volgende schermafbeelding ziet u een methode voor het openen van een formulier toocreate een lege logische SQL-server. 

   ![logische server voltooid formulier maken](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

Als u toothis formulier met een andere methode krijgt, is informatie op Hallo formulier Hallo identiek.

### <a name="create-a-blank-or-sample-sql-database"></a>Maak een lege of voorbeeld SQL-database

een Azure SQL database met toocreate Hallo [Azure-portal](https://portal.azure.com), gaat u tooa leeg SQL Database-formulier en bieden Hallo aangevraagde informatie. U kunt de resourcegroep en de logische server tevoren of tijdens het Hallo-database zelf maken hello Azure SQL database maken. U kunt een lege database maken of maken van een voorbeelddatabase van Adventure Works LT. gebaseerd 

  ![database-1 maken](./media/sql-database-get-started-portal/create-database-1.png)

> [BELANGRIJK] Zie voor meer informatie over het selecteren van Hallo prijscategorie voor uw database [Servicelagen](sql-database-service-tiers.md).
>

### <a name="manage-an-existing-sql-server"></a>Een bestaande SQL server beheren

toomanage een bestaande server, gaat u toohello server met behulp van een aantal methoden - pagina voor specifieke SQL-database, zoals hello **SQL-servers** pagina of Hallo **alle resources** pagina. Hallo volgende schermafbeelding ziet hoe toobegin instellen van een firewall van het niveau van de server uit Hallo **overzicht** pagina voor een server. 

   ![overzicht van de logische server](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

een bestaande database toomanage navigeren toohello **SQL-databases** pagina en klik op de gewenste toomanage Hallo-database. Hallo volgende schermafbeelding ziet hoe toobegin instellen van een firewall van het niveau van de server voor een database uit Hallo **overzicht** pagina voor een database. 

   ![serverfirewallregel](./media/sql-database-get-started-portal/server-firewall-rule.png) 

> [!IMPORTANT]
> tooconfigure prestaties eigenschappen voor een database, Zie [Servicelagen](sql-database-service-tiers.md).
>

> [!TIP]
> Zie voor een Azure-portal snel starten-zelfstudie [maken van een Azure SQL database in Azure-portal Hallo](sql-database-get-started-portal.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-powershell"></a>Azure SQL-servers, databases, en firewalls beheren met behulp van PowerShell

toocreate en beheren van Azure SQL-server, databases en firewalls met Azure PowerShell, gebruikt u Hallo volgende PowerShell-cmdlets. Als u tooinstall moet of een upgrade van PowerShell, raadpleegt u [Installeer Azure PowerShell-module](/powershell/azure/install-azurerm-ps). Zie voor het maken en beheren van de elastische pools SQL, [elastische pools](sql-database-elastic-pool.md).

| Cmdlet | Beschrijving |
| --- | --- |
|[New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase)|Maakt een database |
|[Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)|Een of meer databases opgehaald|
|[Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase)|Stelt eigenschappen van een database of een bestaande database is verplaatst naar een elastische pool|
|[Verwijder AzureRmSqlDatabase](/powershell/module/azurerm.sql/remove-azurermsqldatabase)|Hiermee verwijdert u een database|
|[Nieuwe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)|Maakt een resourcegroep]
|[Nieuwe AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver)|Hiermee maakt u een server|
|[Get-AzureRmSqlServer](/powershell/module/azurerm.sql/get-azurermsqlserver)|Retourneert informatie over servers|
|[Set-AzureRmSqlServer](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/set-azurermsqlserver)|Hiermee wijzigt u de eigenschappen van een server|
|[Remove-AzureRmSqlServer](/powershell/module/azurerm.sql/remove-azurermsqlserver)|Hiermee verwijdert u een server|
|[New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule)|Hiermee maakt u een firewallregel op serverniveau |
|[Get-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/get-azurermsqlserverfirewallrule)|Firewallregels voor server opgehaald|
|[Set-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/set-azurermsqlserverfirewallrule)|Hiermee wijzigt u een firewallregel in een server|
|[Remove-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/remove-azurermsqlserverfirewallrule)|Hiermee verwijdert u een firewallregel van een server.|

> [!TIP]
> Zie voor een PowerShell snel starten-zelfstudie [maken van één Azure SQL database met behulp van PowerShell](sql-database-get-started-portal.md). Zie voor PowerShell-voorbeeldscripts, [Gebruik PowerShell toocreate één Azure SQL database en een firewallregel configureren](scripts/sql-database-create-and-configure-database-powershell.md) en [bewaken en schalen van een enkele SQL-database met behulp van PowerShell](scripts/sql-database-monitor-and-scale-database-powershell.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-azure-cli"></a>Azure SQL-servers, databases, en firewalls beheren met behulp van hello Azure CLI

toocreate en beheren van Azure SQL-server, databases en firewalls Hello [Azure CLI](/cli/azure/overview), gebruikt u de volgende Hallo [Azure CLI SQL Database](/cli/azure/sql/db) opdrachten. Gebruik Hallo [Cloud Shell](/azure/cloud-shell/overview) toorun Hallo CLI in uw browser of [installeren](/cli/azure/install-azure-cli) op Mac OS-, Linux- of Windows. Zie voor het maken en beheren van de elastische pools SQL, [elastische pools](sql-database-elastic-pool.md).

| Cmdlet | Beschrijving |
| --- | --- |
|[AZ sql-database maken](/cli/azure/sql/db#create) |Maakt een database|
|[AZ sql db-lijst](/cli/azure/sql/db#list)|Geeft een lijst van alle databases en datawarehouses in een server of alle databases in een elastische pool|
|[AZ sql db-edities](/cli/azure/sql/db#list-editions)|Een lijst met beschikbare service doelstellingen en opslaglimieten|
|[AZ sql db lijst-gebruik](/cli/azure/sql/db#list-usages)|Retourneert het gebruik van de database|
|[AZ sql db weergeven](/cli/azure/sql/db#show)|Een database of de data warehouse opgehaald|
|[AZ sql database-update](/cli/azure/sql/db#update)|Een database bijwerkt|
|[AZ sql db verwijderen](/cli/azure/sql/db#delete)|Hiermee verwijdert u een database|
|[AZ groep maken](/cli/azure/group#create)|Maakt een resourcegroep|
|[AZ sql server maken](/cli/azure/sql/server#create)|Hiermee maakt u een server|
|[lijst met AZ sql server](/cli/azure/sql/server#list)|Een lijst met servers|
|[AZ sql server lijst-gebruik](/cli/azure/sql/server#list-usages)|Retourneert het gebruik van server|
|[AZ sql server weergeven](/cli/azure/sql/server#show)|Een server opgehaald|
|[update van sql server AZ](/cli/azure/sql/server#update)|Een server worden bijgewerkt|
|[AZ sql server verwijderen](/cli/azure/sql/server#delete)|Een server verwijderen|
|[AZ sql server-firewallregel maken](/cli/azure/sql/server/firewall-rule#create)|Hiermee maakt u een firewallregel op server|
|[lijst van AZ sql server-firewallregel](/cli/azure/sql/server/firewall-rule#list)|Geeft een lijst van de firewallregels Hallo op een server|
|[AZ sql server-firewallregel weergeven](/cli/azure/sql/server/firewall-rule#show)|Hallo-details van een firewallregel|
|[update van AZ sql server-firewallregel](/cli/azure/sql/server/firewall-rule#update)|Een firewallregel bijgewerkt|
|[AZ sql server-firewallregel verwijderen](/cli/azure/sql/server/firewall-rule#delete)|Hiermee verwijdert u een firewallregel|

> [!TIP]
> Zie voor een zelfstudie snel starten met Azure CLI, [maken van één Azure SQL database met behulp van Azure CLI Hallo](sql-database-get-started-cli.md). Zie voor Azure CLI-voorbeeldscripts, [gebruik CLI toocreate één Azure SQL database en een firewallregel configureren](scripts/sql-database-create-and-configure-database-cli.md) en [gebruik CLI toomonitor en schaal één SQL-database](scripts/sql-database-monitor-and-scale-database-cli.md).
>

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-transact-sql"></a>Azure SQL-servers, databases, en firewalls beheren met behulp van Transact-SQL

toocreate en beheren van Azure SQL-server, databases en firewalls met Transact-SQL, Hallo volgende T-SQL-opdrachten gebruiken. U kunt deze opdrachten hello Azure-portal met de opdracht [SQL Server Management Studio](/sql/ssms/use-sql-server-management-studio), [Visual Studio Code](https://code.visualstudio.com/docs), of een ander programma dat kan verbinding maken met tooan Azure SQL Database-server en doorgeven Transact-SQL de opdrachten. Zie voor het beheren van de elastische pools SQL [elastische pools](sql-database-elastic-pool.md).

> [!IMPORTANT]
> U kunt maken of verwijderen van een server met behulp van Transact-SQL.
>

| Opdracht | Beschrijving |
| --- | --- |
|[DATABASE (Azure SQL Database) maken](/sql/t-sql/statements/create-database-azure-sql-database)|Maakt een nieuwe database. U moet verbonden toohello hoofddatabase toocreate een nieuwe database.|
| [ALTER DATABASE (Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) |Hiermee wijzigt u een Azure SQL database. |
|[ALTER DATABASE (Azure SQL datawarehouse)](/sql/t-sql/statements/alter-database-azure-sql-data-warehouse)|Hiermee wijzigt u een Azure SQL datawarehouse.|
|[DATABASE (Transact-SQL) verwijderen](/sql/t-sql/statements/drop-database-transact-sql)|Hiermee verwijdert u een database.|
|[sys.database_service_objectives (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-service-objectives-azure-sql-database)|Retourneert Hallo edition (servicelaag), servicedoelstelling (prijscategorie) en de naam van de elastische groep, indien aanwezig, voor een Azure SQL database of een Azure SQL Data Warehouse. Als u aangemeld bent op de hoofddatabase toohello in een Azure SQL Database-server, retourneert de informatie voor alle databases. Voor Azure SQL Data Warehouse moet u verbonden toohello hoofddatabase.|
|[sys.dm_db_resource_stats (Azure SQL Database)](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database)| Retourneert de CPU, i/o- en geheugen verbruik voor een Azure SQL Database-database. Één rij bestaat voor elke 15 seconden, zelfs als er geen activiteit in Hallo-database.|
|[sys.resource_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database)|Retourneert de gegevens in CPU-gebruik en opslag voor een Azure SQL Database. Hallo-gegevens worden verzameld en geaggregeerd binnen vijf minuten.|
|[sys.database_connection_stats (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-connection-stats-azure-sql-database)|Statistieken voor SQL-Database database connectiviteitsgebeurtenissen, met een overzicht van de database verbinding successen en mislukkingen bevat. |
|[sys.event_log (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-event-log-azure-sql-database)|Geslaagde Azure SQL Database-databaseverbindingen verbindingsfouten en impassen retourneert. U kunt deze informatie tootrack gebruiken of de activiteit van uw database met SQL Database oplossen.|
|[sp_set_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)|Maken of bijwerken van Hallo serverniveau firewall-instellingen voor uw SQL Database-server. Deze opgeslagen procedure is alleen beschikbaar in Hallo hoofddatabase toohello niveau van de server principal-aanmelding op. Een firewallregel op serverniveau kan alleen worden gemaakt met behulp van Transact-SQL nadat Hallo eerste niveau van de server firewall-regel is gemaakt door een gebruiker met machtigingen op Azure-niveau|
|[sys.firewall_rules (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database)|Retourneert informatie over Hallo serverniveau firewall-instellingen die zijn gekoppeld aan uw Microsoft Azure SQL Database.|
|[sp_delete_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database)|Hiermee verwijdert u serverniveau firewall-instellingen van uw SQL-Database-server. Deze opgeslagen procedure is alleen beschikbaar in Hallo hoofddatabase toohello niveau van de server principal-aanmelding op.|
|[sp_set_database_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)|Maken of bijwerken van Hallo databaseniveau firewallregels voor uw Azure SQL Database of SQL Data Warehouse. Database-firewall-regels kunnen worden geconfigureerd voor de hoofddatabase Hallo en gebruikersdatabases op SQL-Database. Database-firewallregels zijn nuttig wanneer databasegebruikers met behulp van opgenomen. |
|[sys.database_firewall_rules (Azure SQL Database)](/sql/relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database)|Retourneert informatie over Hallo databaseniveau firewall-instellingen die zijn gekoppeld aan uw Microsoft Azure SQL Database. |
|[sp_delete_database_firewall_rule (Azure SQL Database)](/sql/relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database)|Hiermee verwijdert u de instelling van de firewallregel op databaseniveau van uw Azure SQL Database of SQL Data Warehouse. |


> [!TIP]
> Zie voor een zelfstudie voor snel starten met behulp van SQL Server Management Studio op Microsoft Windows, [Azure SQL Database: gebruikt SQL Server Management Studio tooconnect en query gegevens](sql-database-connect-query-ssms.md). Zie voor een zelfstudie voor snel starten met behulp van Visual Studio Code op Hallo Mac OS-, Linux- of Windows, [Azure SQL Database: Gebruik Visual Studio Code tooconnect en query gegevens](sql-database-connect-query-vscode.md).

## <a name="manage-azure-sql-servers-databases-and-firewalls-using-hello-rest-api"></a>Azure SQL-servers, databases, en firewalls beheren met behulp van Hallo REST-API

toocreate en Azure SQL-server, databases en Hallo REST-API met firewalls beheren, Zie [REST-API van Azure SQL Database](/rest/api/sql/).

## <a name="next-steps"></a>Volgende stappen

- toolearn over het groeperen van databases met SQL elastische pools, Zie [elastische pools](sql-database-elastic-pool.md).
- Zie voor meer informatie over Azure SQL Database-service Hallo [wat is er SQL-Database?](sql-database-technical-overview.md).
- Zie toolearn over het migreren van een SQL Server database-tooAzure [tooAzure SQL-Database migreren](sql-database-cloud-migrate.md).
- Zie [Functies](sql-database-features.md) voor meer informatie over ondersteunde functies.
