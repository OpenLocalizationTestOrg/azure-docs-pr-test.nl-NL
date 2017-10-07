---
title: firewallregels voor SQL-Database aaaAzure | Microsoft Docs
description: Meer informatie over hoe de firewall met server- en databaseniveau regels toomanage firewalltoegang voor tooconfigure een SQL-database.
keywords: databasefirewall
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: ac57f84c-35c3-4975-9903-241c8059011e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 04/10/2017
ms.author: rickbyh
ms.openlocfilehash: 6a8cdf629d0d0e55421a5e9f9b894a21371be568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-server-level-and-database-level-firewall-rules"></a>Azure SQL Database-server- en databaseniveau firewall-regels 

Microsoft Azure SQL Database levert een relationele-databaseservice voor Azure en andere op internet gebaseerde toepassingen. toohelp uw gegevens beschermen, firewalls te voorkomen dat alle toegang tooyour-databaseserver totdat u opgeven welke computers over machtigingen beschikken. Hallo firewall verleent toegang toodatabases op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn.

## <a name="overview"></a>Overzicht

Alle Transact-SQL toegang tooyour Azure SQL-server wordt in eerste instantie wordt geblokkeerd door Hallo firewall. toobegin met behulp van uw Azure SQL-server, moet u een of meer serverniveau firewallregels waarmee toegang tooyour Azure SQL-server opgeven. Gebruik Hallo firewall-regels toospecify welk IP-adres een bereik van Hallo Internet zijn toegestaan en of Azure-toepassingen tooconnect tooyour Azure SQL-server kunnen proberen.

tooselectively verlenen toegang toojust een van de databases Hallo in uw Azure SQL-server, moet u een regel databaseniveau voor Hallo vereiste database maken. Geef een IP-adresbereik voor Hallo database firewallregel buiten Hallo IP-adresbereik dat is opgegeven in de firewallregel op serverniveau hello, en zorg ervoor dat Hallo IP-adres van de client Hallo Hallo bereik dat is opgegeven in Hallo databaseniveau regel valt.

Verbindingspogingen van Hallo Internet en Azure moet eerst Hallo firewall passeren voordat ze uw Azure SQL-server of SQL-Database bereiken kunnen, zoals wordt weergegeven in het volgende diagram Hallo:

   ![Diagram met beschrijving van firewallconfiguratie.][1]

* **Firewallregels op serverniveau:** deze regels inschakelen clients tooaccess uw hele Azure SQL-server, dat wil zeggen, alle Hallo databases binnen dezelfde logische server Hallo. Deze regels worden opgeslagen in Hallo **master** database. Firewallregels op serverniveau kunnen worden geconfigureerd met behulp van Hallo portal of met behulp van Transact-SQL-instructies. toocreate serverniveau firewallregels met hello Azure-portal of PowerShell, moet u de eigenaar van de Hallo-abonnement of een bijdrager abonnement. toocreate een firewallregel op serverniveau met Transact-SQL, moet u verbinding maken toohello SQL Database-exemplaar als Hallo principal-aanmelding op serverniveau of hello Azure Active Directory-beheerder (wat betekent dat er eerst een firewallregel op serverniveau moet worden gemaakt door een gebruiker met machtigingen op Azure-niveau).
* **Databaseniveau firewallregels:** deze regels inschakelen clients tooaccess bepaalde (beveiligde) databases binnen Hallo dezelfde logische server. U kunt deze regels voor elke database maken (inclusief Hallo **master** database0) en ze worden opgeslagen in afzonderlijke databases Hallo. Firewallregel op databaseniveau regels kunnen alleen worden geconfigureerd met behulp van Transact-SQL-instructies en pas nadat u hebt geconfigureerd Hallo eerste niveau van de server-firewall. Als u een IP-adresbereik in Hallo firewallregel op databaseniveau regel die is opgegeven in de firewallregel op serverniveau Hallo buiten Hallo-bereik opgeeft, alleen de clients die hebben Hallo databaseniveau bereik met IP-adressen, hebben toegang tot Hallo-database. U kunt voor een database maximaal 128 firewallregels op databaseniveau opgeven. Databaseniveau firewallregels voor hoofd- en -databases kunnen alleen worden gemaakt en beheerd via de Transact-SQL. Zie voor meer informatie over het configureren van de firewallregel op databaseniveau regels Hallo voorbeeld verderop in dit artikel en Zie [sp_set_database_firewall_rule (Azure SQL-Databases)](https://msdn.microsoft.com/library/dn270010.aspx).

**Aanbeveling:** Microsoft raadt het gebruik van de firewallregel op databaseniveau regels wanneer mogelijke tooenhance beveiligings- en toomake uw meer draagbare database. Gebruik firewallregels op serverniveau voor beheerders en wanneer er veel databases die Hallo hebben dezelfde vereisten voor toegang en u niet wilt dat toospend tijd elke database afzonderlijk configureren.

> [!Note]
> Zie voor meer informatie over draagbare databases in de context van Hallo van zakelijke continuïteit [verificatievereisten voor herstel na noodgevallen](sql-database-geo-replication-security-config.md).
>

### <a name="connecting-from-hello-internet"></a>Verbinding maken vanaf Internet Hallo

Wanneer een computer tooconnect tooyour-databaseserver van Hallo Internet probeert, controleert Hallo firewall eerst Hallo IP-adres van de aanvraag met de Hallo firewallregel op databaseniveau regels voor Hallo-database die Hallo verbinding vraagt Hallo die afkomstig zijn:

* Als Hallo IP-adres van de aanvraag Hallo binnen één van de opgegeven in Hallo databaseniveau firewallregels Hallo-bereiken, krijgt Hallo verbinding toohello SQL-Database waarin Hallo-regel.
* Als Hallo IP-adres van de aanvraag Hallo zich niet binnen een opgegeven in de firewallregel op databaseniveau Hallo Hallo-bereiken, worden Hallo serverniveau firewall-regels gecontroleerd. Als Hallo IP-adres van de aanvraag Hallo binnen één van de opgegeven in het niveau van de server-firewallregels Hallo Hallo-bereiken, wordt Hallo verbinding verleend. Firewallregels op serverniveau gelden tooall SQL-databases op Hallo Azure SQL-server.  
* Als Hallo IP-adres van de aanvraag Hallo valt niet binnen Hallo bereiken opgegeven in een Hallo databaseniveau of serverniveau firewallregels, Hallo-verbindingsaanvraag is mislukt.

> [!NOTE]
> tooaccess Azure SQL Database van de lokale computer, zorg ervoor dat het Hallo-firewall op uw netwerk en de lokale computer staat uitgaande communicatie op TCP-poort 1433.
> 

### <a name="connecting-from-azure"></a>Verbinding maken vanuit Azure
tooallow toepassingen vanuit Azure tooconnect tooyour Azure SQL-server, Azure-verbindingen moeten zijn ingeschakeld. Wanneer een toepassing van Azure tooconnect tooyour database-server probeert, controleert Hallo-firewall of dat de Azure-verbindingen zijn toegestaan. Een firewall instellen met de begin- en einddatum adres gelijk too0.0.0.0 geeft aan dat deze verbindingen zijn toegestaan. Als Hallo verbindingspoging niet is toegestaan, wordt in Hallo aanvraag hello Azure SQL Database-server niet bereiken.

> [!IMPORTANT]
> Deze optie configureert Hallo firewall tooallow alle verbindingen van Azure, inclusief verbindingen van Hallo abonnementen van andere klanten. Geautoriseerde gebruikers wanneer deze optie, zorg ervoor dat uw aanmelding en gebruikersmachtigingen tooonly toegang beperken.
> 

## <a name="creating-and-managing-firewall-rules"></a>Maken en beheren van de firewall-regels
Hallo eerste niveau van de server firewall-instellingen kan worden gemaakt met Hallo [Azure-portal](https://portal.azure.com/) of programmatisch met [Azure PowerShell](https://msdn.microsoft.com/library/azure/dn546724.aspx), [Azure CLI](/cli/azure/sql/server/firewall-rule#create), of Hallo [REST-API](https://msdn.microsoft.com/library/azure/dn505712.aspx). Volgende firewallregels op serverniveau kunt u maken en beheren met deze methoden en via Transact-SQL. 

> [!IMPORTANT]
> Firewallregel op databaseniveau regels kunnen alleen worden gemaakt en beheerd met behulp van Transact-SQL. 
>

tooimprove prestaties, serverniveau firewall regels op databaseniveau Hallo tijdelijk worden opgeslagen. toorefresh hello cache, Zie [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx). 

> [!TIP]
> U kunt [SQL Database Auditing](sql-database-auditing.md) wijzigingen van de server- en databaseniveau firewall tooaudit.
>

### <a name="azure-portal"></a>Azure Portal

tooset een firewallregel op serverniveau in hello Azure-portal, kunt u ofwel gaan toohello overzichtspagina voor uw Azure SQL database of Hallo overzichtspagina voor de logische server van uw Azure-Database.

> [!TIP]
> Zie voor een zelfstudie [maken een database met behulp van Azure-portal Hallo](sql-database-get-started-portal.md).
>

**Van de overzichtspagina van database**

1. tooset een firewallregel op serverniveau van overzichtspagina Hallo-database, klikt u op **ingesteld serverfirewall** op Hallo werkbalk zoals weergegeven in Hallo volgende afbeelding: Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend.

      ![serverfirewallregel](./media/sql-database-get-started-portal/server-firewall-rule.png) 

2. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd Hallo IP-adres van de computer Hallo u momenteel gebruikt en klik vervolgens op **opslaan**. Er wordt een firewallregel op serverniveau gemaakt voor uw huidige IP-adres.

      ![serverfirewallregel instellen](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

**Van de overzichtspagina van server**

Hallo overzichtspagina voor uw server wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver20170403.database.windows.net**) en biedt opties voor verdere configuratie.

1. tooset een regel niveau van de server van de overzichtspagina van server, klikt u op **Firewall** in Hallo links menu onder instellingen zoals weergegeven zoals in Hallo installatiekopie te volgen: 

     ![overzicht van de logische server](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Klik op **client-IP toevoegen** op Hallo werkbalk tooadd Hallo IP-adres van de computer Hallo u momenteel gebruikt en klik vervolgens op **opslaan**. Er wordt een firewallregel op serverniveau gemaakt voor uw huidige IP-adres.

     ![serverfirewallregel instellen](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

### <a name="transact-sql"></a>Transact-SQL
| Catalogusweergave of opgeslagen procedure | Niveau | Beschrijving |
| --- | --- | --- |
| [sys.firewall_rules](https://msdn.microsoft.com/library/dn269980.aspx) |Server |Hallo huidige serverniveau firewall-regels worden weergegeven |
| [sp_set_firewall_rule](https://msdn.microsoft.com/library/dn270017.aspx) |Server |Hiermee worden de firewallregels op serverniveau gemaakt of bijgewerkt |
| [sp_delete_firewall_rule](https://msdn.microsoft.com/library/dn270024.aspx) |Server |Verwijdert firewallregels op serverniveau |
| [sys.database_firewall_rules](https://msdn.microsoft.com/library/dn269982.aspx) |Database |Geeft het huidige firewallregel op databaseniveau regels Hallo |
| [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) |Database |Gemaakt of bijgewerkt Hallo databaseniveau firewall-regels |
| [sp_delete_database_firewall_rule](https://msdn.microsoft.com/library/dn270030.aspx) |Databases |Verwijdert firewallregels op databaseniveau |


Hallo volgende voorbeelden Bekijk Hallo bestaande regels, een bereik met IP-adressen op Hallo server Contoso inschakelen en een firewallregel worden verwijderd:
   
```sql
SELECT * FROM sys.firewall_rules ORDER BY name;
```
  
Voeg daarna een firewallregel toe.
   
```sql
EXECUTE sp_set_firewall_rule @name = N'ContosoFirewallRule',
   @start_ip_address = '192.168.1.1', @end_ip_address = '192.168.1.10'
```

een firewallregel op serverniveau, toodelete hello sp_delete_firewall_rule opgeslagen procedure uitvoeren. Hallo wordt volgende voorbeeld met de naam ContosoFirewallRule Hallo-regel:
   
```sql
EXECUTE sp_delete_firewall_rule @name = N'ContosoFirewallRule'
```   

### <a name="azure-powershell"></a>Azure PowerShell
| Cmdlet | Niveau | Beschrijving |
| --- | --- | --- |
| [Get-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546731.aspx) |Server |Retourneert de huidige serverniveau firewall-regels Hallo |
| [New-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546724.aspx) |Server |Maakt een nieuwe firewallregel op serverniveau |
| [Set-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546739.aspx) |Server |Updates Hallo eigenschappen van een bestaande firewallregel op serverniveau |
| [Remove-AzureSqlDatabaseServerFirewallRule](https://msdn.microsoft.com/library/azure/dn546727.aspx) |Server |Verwijdert firewallregels op serverniveau |


Hallo volgende voorbeeld wordt een firewallregel op serverniveau met behulp van PowerShell:

```powershell
New-AzureRmSqlServerFirewallRule -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -FirewallRuleName "AllowSome" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
```

> [!TIP]
> Zie voor PowerShell-voorbeelden in Hallo context van een snel starten, [maken DB - PowerShell](sql-database-get-started-powershell.md) en [een individuele database maken en configureren van een firewallregel met behulp van PowerShell](scripts/sql-database-create-and-configure-database-powershell.md)
>

### <a name="azure-cli"></a>Azure CLI
| Cmdlet | Niveau | Beschrijving |
| --- | --- | --- |
| [sql server-firewall AZ maken](/cli/azure/sql/server/firewall-rule#create) | Maakt een firewall regel tooallow toegang tooall SQL-Databases op Hallo-server uit Hallo opgegeven IP-adresbereik.|
| [AZ sql server firewall verwijderen](/cli/azure/sql/server/firewall-rule#delete)| Hiermee verwijdert u een firewallregel.|
| [lijst van AZ sql server-firewall](/cli/azure/sql/server/firewall-rule#list)| Geeft een lijst Hallo firewallregels.|
| [AZ sql server-firewallregel weergeven](/cli/azure/sql/server/firewall-rule#show)| Hallo worden details weergegeven van een firewallregel.|
| [AX-update van sql server firewall-regel](/cli/azure/sql/server/firewall-rule#update)| Een firewallregel bijgewerkt.

Hallo volgende voorbeeld wordt een firewallregel op serverniveau hello Azure CLI gebruiken: 

```azurecli-interactive
az sql server firewall-rule create --resource-group myResourceGroup --server $servername \
    -n AllowYourIp --start-ip-address 0.0.0.0 --end-ip-address 0.0.0.0
```

> [!TIP]
> Zie voor een voorbeeld Azure CLI in Hallo context van een snel starten [maken DDB - Azure CLI](sql-database-get-started-cli.md) en [een individuele database maken en configureren van een firewallregel hello Azure CLI gebruiken](scripts/sql-database-create-and-configure-database-cli.md)
>

### <a name="rest-api"></a>REST API
| API | Niveau | Beschrijving |
| --- | --- | --- |
| [List Firewall Rules](https://msdn.microsoft.com/library/azure/dn505715.aspx) (Lijst met firewallregels) |Server |Hallo huidige serverniveau firewall-regels worden weergegeven |
| [Create Firewall Rule](https://msdn.microsoft.com/library/azure/dn505712.aspx) (Firewallregel maken) |Server |Hiermee worden de firewallregels op serverniveau gemaakt of bijgewerkt |
| [Set Firewall Rule](https://msdn.microsoft.com/library/azure/dn505707.aspx) (Firewallregel instellen) |Server |Updates Hallo eigenschappen van een bestaande firewallregel op serverniveau |
| [Delete Firewall Rule](https://msdn.microsoft.com/library/azure/dn505706.aspx) (Firewallregel verwijderen) |Server |Verwijdert firewallregels op serverniveau |

## <a name="server-level-firewall-rule-versus-a-database-level-firewall-rule"></a>Firewallregel op serverniveau ten opzichte van een firewallregel op databaseniveau
Q. Gebruikers van één database worden volledig geïsoleerd van een andere database?   
  Zo ja, verlenen toegang met behulp van de firewallregel op databaseniveau regels. Zo voorkomt u met behulp van serverniveau firewallregels, die toegang via de firewall Hallo tooall databases verlenen, Hallo diepte van de beveiliging te verminderen.   
 
Q. Hebben gebruikers op Hallo IP-adres moet toegang tot tooall databases?   
  Gebruik serverniveau firewall-regels tooreduce Hallo hoe vaak die moet u firewallregels configureren.   

Q. Toegang via hello Azure-portal, PowerShell of REST-API Hallo hebben Hallo persoon die of het team alleen Hallo firewallregels configureren?   
  Hebt u firewallregels op serverniveau. Firewallregels databaseniveau kunnen alleen worden geconfigureerd met behulp van Transact-SQL.  

Q. Hallo persoon die of het team Hallo firewallregels configureren verboden in dat de geavanceerde machtiging op databaseniveau Hallo?   
  Gebruik de firewallregels op serverniveau. Configureren van de firewallregel op databaseniveau regels met Transact-SQL vereist ten minste `CONTROL DATABASE` op databaseniveau Hallo toestemming.  

Q. Hallo persoon die of het team configureren of Hallo firewallregels, controle is centraal beheren van de firewallregels voor veel (bijvoorbeeld 100) van databases?   
  Deze selectie zijn afhankelijk van uw behoeften en omgeving. Firewallregels op serverniveau misschien gemakkelijker tooconfigure maar regels op Hallo databaseniveau scripting kunt configureren. En zelfs als u firewallregels op serverniveau gebruikt, moet u mogelijk tooaudit Hallo database-firewallregels, toosee als gebruikers met `CONTROL` machtiging op Hallo database firewallregel op databaseniveau regels hebt gemaakt.   

Q. Kan ik een combinatie van beide firewallregels voor server- en databaseniveau gebruiken?   
  Ja. Sommige gebruikers, zoals beheerders mogelijk firewallregels op serverniveau. Andere gebruikers, zoals gebruikers van een databasetoepassing mogelijk databaseniveau firewallregels.   

## <a name="troubleshooting-hello-database-firewall"></a>Hallo-databasefirewall probleemoplossing
Overweeg de volgende punten wanneer toegang toohello Microsoft Azure SQL Database-service niet meer werkt zoals verwacht Hallo:

* **Configuratie van de lokale firewall:** voordat de computer toegang heeft tot Azure SQL Database, moet u mogelijk toocreate een firewall-uitzondering op uw computer voor TCP-poort 1433. Als u verbindingen binnen een grens van hello Azure-cloud maken, hebt u mogelijk tooopen extra poorten. Zie voor meer informatie, Hallo **SQL-Database: buiten tegenover binnen** sectie van [poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).
* **Netwerkadresomzetting (NAT):** vervaldatum tooNAT, Hallo IP-adres van uw computer tooconnect tooAzure SQL-Database is mogelijk anders dan Hallo IP-adres wordt weergegeven in uw computer IP-configuratie-instellingen. tooview hello IP-adres de computer is met behulp van tooconnect tooAzure toohello portal aanmelden en navigeer toohello **configureren** tabblad op Hallo-server die als host fungeert voor uw database. Onder Hallo **IP-adressen toegestaan** sectie hello **huidige IP-adres van de Client** wordt weergegeven. Klik op **toevoegen** toohello **IP-adressen toegestaan** tooallow deze computer tooaccess Hallo-server.
* **Acceptatielijst toohello wijzigingen zijn niet van kracht:** kunnen er maar liefst vijf minuten uitstellen wordt toohello Azure SQL Database firewall configuratie tootake effect gewijzigd.
* **Hallo-aanmelding is niet gemachtigd of een onjuist wachtwoord is gebruikt:** als een aanmelding heeft geen machtigingen voor hello Azure SQL Database-server of Hallo wachtwoord onjuist is, Hallo verbinding toohello Azure SQL Database-server is geweigerd. Maken van een firewallinstelling biedt alleen clients met een kans tooattempt verbinding tooyour server; elke client moet Hallo noodzakelijke beveiligingsreferenties opgeven. Zie Databases, aanmeldingen en gebruikers beheren in Azure SQL Database, voor meer informatie over het voorbereiden van aanmeldingen.
* **Dynamische IP-adres:** als u een internetverbinding met dynamische IP-adressering hebt en u problemen ondervindt bij het ophalen via de firewall Hallo, kunt u een van de volgende oplossingen Hallo kan proberen:
  
  * Vraag uw Internetproviderverbindingen (ISP) voor Hallo IP-adresbereik toegewezen tooyour clientcomputers die toegang hello Azure SQL Database-server en vervolgens Hallo IP-adresbereik toevoegen als een firewallregel.
  * Statische IP-adressen in plaats daarvan voor uw clientcomputers ophalen en voeg vervolgens Hallo IP-adressen als firewallregels.

## <a name="next-steps"></a>Volgende stappen

- Zie voor een snel starten over het maken van een database en een firewallregel op serverniveau [maken van een Azure SQL database](sql-database-get-started-portal.md).
- Zie voor hulp bij het maken van verbinding tooan Azure SQL-database van open-source of toepassingen van derden, [snel starten-clientcode voorbeelden tooSQL Database](https://msdn.microsoft.com/library/azure/ee336282.aspx).
- Zie voor informatie over extra poorten mogelijk moet u tooopen Hallo **SQL-Database: buiten tegenover binnen** sectie van [poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md)
- Zie voor een overzicht van Azure SQL Database-beveiliging [beveiliging van uw database](sql-database-security-overview.md)

<!--Image references-->
[1]: ./media/sql-database-firewall-configure/sqldb-firewall-1.png
