---
title: aaaAzure SQL-aanmeldingen en gebruikers | Microsoft Docs
description: Meer informatie over het beheer van SQL Database-beveiliging, specifiek hoe toomanage database toegang en meld u aan beveiliging via Hallo niveau van de server principal-account.
keywords: sql-databasebeveiliging,beheer databasebeveiliging,aanmeldingsbeveiliging,databasebeveiliging,databasetoegang
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 0a65a93f-d5dc-424b-a774-7ed62d996f8c
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 01/23/2017
ms.author: rickbyh
ms.openlocfilehash: dff889b9fed09146a10008c0d11ca9e71d91df5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-and-granting-database-access"></a>Toegang tot databases beheren en verlenen

Wanneer de firewallregels zijn geconfigureerd, mensen kunnen verbinding maken tooa SQL-Database als een van de beheerdersaccounts Hallo, als de eigenaar van de database Hallo of als een databasegebruiker in Hallo-database.  

>  [!NOTE]  
>  Dit onderwerp geldt tooAzure SQL server- en tooboth SQL-Database en SQL Data Warehouse databases die zijn gemaakt op Hallo Azure SQL-server. Eenvoud, SQL-Database gebruikt wanneer tooboth SQL-Database en SQL Data Warehouse wordt verwezen. 
>

> [!TIP]
> Zie voor een zelfstudie [beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).
>


## <a name="unrestricted-administrative-accounts"></a>Onbeperkte beheerdersaccounts
Er zijn twee beheerdersaccounts (**serverbeheerder** en **Active Directory-beheerder**) die als beheerder fungeren. tooidentify deze beheerdersaccounts voor uw SQL-server openen hello Azure-portal en navigeer toohello eigenschappen van uw SQL server.

![SQL Server-beheerders](./media/sql-database-manage-logins/sql-admins.png)

- **Serverbeheerder**   
Wanneer u een Azure SQL-server maakt, moet u de **aanmeldgegevens van de serverbeheerder** opgeven. SQL server maakt dat account als een aanmelding in de hoofddatabase Hallo. Dit account maakt verbinding met behulp van SQL Server-verificatie (gebruikersnaam en wachtwoord). Er kan slechts één van deze accounts bestaan.   
- **Azure Active Directory-beheerder**   
Ook één Azure Active Directory-account (een afzonderlijk account of het account van een beveiligingsgroep) kan als beheerder worden geconfigureerd. Het optionele tooconfigure een Azure AD-beheerder is, maar een Azure AD-beheerder als u wilt dat toouse Azure AD-accounts tooconnect tooSQL Database moet worden geconfigureerd. Zie voor meer informatie over het configureren van toegang tot Azure Active Directory [verbinding maakt met tooSQL Database of SQL Data Warehouse door met behulp van Azure Active Directory-verificatie](sql-database-aad-authentication.md) en [SSMS ondersteuning voor Azure AD MFA met behulp van SQL Database en SQL datawarehouse](sql-database-ssms-mfa-authentication.md).
 

Hallo **serverbeheerder** en **Azure AD-beheerder** accounts heeft Hallo volgende kenmerken:
- Dit zijn Hallo alleen accounts die automatisch verbinding van tooany SQL-Database op Hallo-server maken kunnen. (tooconnect tooa gebruikersdatabase, andere accounts moeten zijn van een eigenaar Hallo Hallo database of een gebruikersaccount hebben in de gebruikersdatabase Hallo.)
- Deze accounts gebruikersdatabases invoeren als Hallo `dbo` gebruiker en ze beschikken over alle Hallo machtigingen in Hallo gebruikersdatabases. (Hallo database Hallo eigenaar van een gebruikersdatabase ook ingevoerd als Hallo `dbo` gebruiker.) 
- Deze accounts voert geen Hallo `master` database als Hallo `dbo` gebruiker en ze beperkte machtigingen in master. 
- Deze accounts zijn geen leden Hallo standaard SQL Server `sysadmin` vaste serverrol die niet beschikbaar in SQL-database is.  
- Deze accounts kunnen databases, aanmeldingen en gebruikers in de hoofddatabase, en firewallregels op serverniveau maken, wijzigen en verwijderen.
- Deze accounts kunnen toevoegen en verwijderen van leden toohello `dbmanager` en `loginmanager` rollen.
- Deze accounts kunnen bekijken Hallo `sys.sql_logins` systeemtabel.

### <a name="configuring-hello-firewall"></a>Hallo firewall configureren
Wanneer Hallo serverniveau firewall is geconfigureerd voor een afzonderlijke IP-adres of een bereik, Hallo **SQL server-beheerder** en Hallo **Azure Active Directory-beheerder** toohello master-database en alle Hallo verbinding kunnen maken gebruikersdatabases. het eerste niveau van de server firewall Hallo kan worden geconfigureerd via Hallo [Azure-portal](sql-database-get-started-portal.md)met [PowerShell](sql-database-get-started-powershell.md) of met behulp van Hallo [REST-API](https://msdn.microsoft.com/library/azure/dn505712.aspx). Nadat er een verbinding tot stand is gebracht, kunnen er ook aanvullende firewallregels op serverniveau worden geconfigureerd met behulp van de [Transact-SQL](sql-database-configure-firewall-settings.md).

### <a name="administrator-access-path"></a>Toegangspad beheerder
Wanneer Hallo serverniveau firewall correct is geconfigureerd, Hallo **SQL server-beheerder** en Hallo **Azure Active Directory-beheerder** verbinding kan maken met clienttools, zoals SQL Server Management Studio of SQL Server Data Tools. Alleen Hallo nieuwste hulpprogramma's bieden alle Hallo functies en mogelijkheden. Hallo volgende diagram toont een typische configuratie voor Hallo twee beheerdersaccounts.

![Toegangspad beheerder](./media/sql-database-manage-logins/1sql-db-administrator-access.png)

Wanneer u een open poort in Hallo serverniveau firewall gebruikt, kunnen beheerders verbinding tooany SQL-Database maken.

### <a name="connecting-tooa-database-by-using-sql-server-management-studio"></a>Verbinding tooa database maken met behulp van SQL Server Management Studio
Zie voor een overzicht van het maken van een server, een database, firewallregels op serverniveau en het gebruik van SQL Server Management Studio tooquery een database, [aan de slag met Azure SQL Database-servers, databases en firewall-regels met behulp van hello Azure-portal en SQL Server Management Studio](sql-database-get-started-portal.md).

> [!IMPORTANT]
> Het verdient aanbeveling dat u altijd hello gebruiken meest recente versie van Management Studio tooremain gesynchroniseerd met updates tooMicrosoft Azure en SQL-Database. [SQL Server Management Studio bijwerken](https://msdn.microsoft.com/library/mt238290.aspx).


## <a name="additional-server-level-administrative-roles"></a>Aanvullende beheerdersrollen op serverniveau
Bovendien toohello serverniveau beheerdersrollen eerder besproken, SQL Database biedt twee beperkte beheerdersrollen in Hallo hoofddatabase toowhich gebruikersaccounts kunnen worden toegevoegd die machtigingen tooeither databases maken of beheren aanmeldingen.

### <a name="database-creators"></a>Databasemakers
Een van deze beheerderrollen Hallo is **dbmanager** rol. Leden van deze rol kunnen nieuwe databases maken. toouse deze rol, u een gebruiker maken in Hallo `master` database en voeg vervolgens Hallo gebruiker toohello **dbmanager** -databaserol. toocreate een database, Hallo gebruiker moet een gebruiker op basis van een SQL Server-aanmelding in de hoofddatabase Hallo of bevatte databasegebruiker op basis van een Azure Active Directory-gebruiker zijn.

1. Met behulp van een administrator-account verbinding toohello hoofddatabase maken.
2. Optionele stap: Maak een SQL Server-verificatie-aanmelding met Hallo [aanmelding maken](https://msdn.microsoft.com/library/ms189751.aspx) instructie. Voorbeeldinstructie:
   
   ```
   CREATE LOGIN Mary WITH PASSWORD = '<strong_password>';
   ```
   
   > [!NOTE]
   > Gebruik een sterk wachtwoord bij het maken van aanmeldgegevens of een ingesloten databasegebruiker. Zie [Sterke wachtwoorden](https://msdn.microsoft.com/library/ms161962.aspx) voor meer informatie.
    
   tooimprove prestaties aanmeldingen (serverniveau principals) tijdelijk worden opgeslagen op Hallo databaseniveau. toorefresh hello verificatiecache, Zie [DBCC FLUSHAUTHCACHE](https://msdn.microsoft.com/library/mt627793.aspx).

3. In de hoofddatabase hello, maakt u een gebruiker met behulp van Hallo [gebruiker maken](https://msdn.microsoft.com/library/ms173463.aspx) instructie. Hallo gebruiker kunnen worden een Azure Active Directory authentication opgenomen databasegebruiker (als u uw omgeving voor Azure AD-verificatie hebt geconfigureerd), of een databasegebruiker voor SQL Server-verificatie is opgenomen of een SQL Server authentication-gebruiker op basis van een SQL Aanmelding van Server-verificatie (gemaakt in de vorige stap Hallo.) Voorbeeldinstructies:
   
   ```
   CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
   CREATE USER Tran WITH PASSWORD = '<strong_password>';
   CREATE USER Mary FROM LOGIN Mary; 
   ```

4. Toevoegen van nieuwe gebruiker hello, toohello **dbmanager** databaserol via Hallo [ALTER ROLE](https://msdn.microsoft.com/library/ms189775.aspx) instructie. Voorbeeldinstructies:
   
   ```
   ALTER ROLE dbmanager ADD MEMBER Mary; 
   ALTER ROLE dbmanager ADD MEMBER [mike@contoso.com];
   ```
   
   > [!NOTE]
   > Hallo dbmanager is een databaserol in de database master, zodat u kunt alleen een database toohello dbmanager gebruikersrol toevoegen. U kunt een niveau van de server-aanmelding toodatabase rolgebaseerde niet toevoegen.
    
5. Configureer zo nodig een tooconnect firewall regel tooallow Hallo nieuwe gebruiker. (de nieuwe gebruiker Hallo mogelijk worden volstaan met een bestaande firewallregel.)

Hallo-gebruiker wordt nu verbinding kan maken van de hoofddatabase toohello en nieuwe databases kunt maken. Hallo-account maken Hallo-database wordt Hallo eigenaar van Hallo-database.

### <a name="login-managers"></a>Aanmelding managers
Hallo is andere administratieve rol Hallo aanmelding manager-rol. Leden van deze rol kunnen nieuwe aanmeldingen maken in de hoofddatabase Hallo. Als u wenst, kunt u dezelfde stappen Hallo (een aanmelding en de gebruiker maken en toevoegen van een gebruiker toohello **loginmanager** rol) tooenable een gebruiker toocreate nieuwe aanmeldingen in het Hallo-master. Aanmeldingen zijn meestal niet nodig als Microsoft adviseert het gebruik van ingesloten databasegebruikers die op Hallo verifiëren databaseniveau in plaats van gebruikers op basis van aanmeldingen. Zie [Ingesloten databasegebruikers: een draagbare database maken](https://msdn.microsoft.com/library/ff929188.aspx) voor meer informatie.

## <a name="non-administrator-users"></a>Niet-beheerders
In het algemeen moet niet beheerdersaccounts geen toegang toohello hoofddatabase. Ingesloten databasegebruikers maken op databaseniveau Hallo Hallo met [gebruiker maken (Transact-SQL)](https://msdn.microsoft.com/library/ms173463.aspx) instructie. Hallo gebruiker kunnen worden een Azure Active Directory authentication opgenomen databasegebruiker (als u uw omgeving voor Azure AD-verificatie hebt geconfigureerd), of een databasegebruiker voor SQL Server-verificatie is opgenomen of een SQL Server authentication-gebruiker op basis van een SQL Aanmelding van Server-verificatie (gemaakt in de vorige stap Hallo.) Zie [Ingesloten databasegebruikers: een draagbare database maken](https://msdn.microsoft.com/library/ff929188.aspx) voor meer informatie. 

toocreate gebruikers verbinding maken met database toohello en instructies vergelijkbare toohello volgen voorbeelden uitvoeren:

```
CREATE USER Mary FROM LOGIN Mary; 
CREATE USER [mike@contoso.com] FROM EXTERNAL PROVIDER;
```

In eerste instantie kunt slechts één van de Hallo beheerders of Hallo eigenaar van de database van de Hallo gebruikers maken. tooauthorize extra gebruikers toocreate nieuwe gebruikers, verlenen die Hallo geselecteerde gebruiker `ALTER ANY USER` toestemming hebben, met behulp van een instructie, zoals:

```
GRANT ALTER ANY USER tooMary;
```

toogive extra gebruikers volledig beheer van Hallo-database, zodat ze lid zijn van Hallo **db_owner** vaste databaserol Hallo met `ALTER ROLE` instructie.

> [!NOTE]
> Hallo meest voorkomende reden toocreate databasegebruikers op basis van aanmeldingen, is wanneer u SQL Server-verificatie gebruikers die toegang moeten hebben tot toomultiple databases hebt. Gebruikers op basis van aanmeldingen zijn gebonden toohello aanmelding en slechts één wachtwoord voor dat het aanmelden wordt bijgehouden. Ingesloten databasegebruikers in individuele databases zijn individuele entiteiten en hebben elk een eigen wachtwoord. Dit kan verwarrend zijn voor ingesloten databasegebruikers die hun wachtwoorden niet identiek hebben gehouden.

### <a name="configuring-hello-database-level-firewall"></a>Hallo firewallregel op databaseniveau configureren
Als een best practice mag niet-beheerders alleen hebben voor toegang via Hallo firewall toohello databases die ze gebruiken. In plaats van het autoriseren van hun IP-adressen via Hallo serverniveau firewall- en Hallo zodat ze toegang tooall databases, gebruik [sp_set_database_firewall_rule](https://msdn.microsoft.com/library/dn270010.aspx) instructie tooconfigure Hallo firewallregel op databaseniveau. Hallo firewallregel op databaseniveau kan niet worden geconfigureerd met behulp van Hallo-portal.

### <a name="non-administrator-access-path"></a>Toegangspad niet-beheerder
Wanneer Hallo firewallregel op databaseniveau correct is geconfigureerd, Hallo databasegebruikers verbinding kunnen maken met behulp van de client-hulpprogramma's, zoals SQL Server Management Studio of SQL Server Data Tools. Alleen Hallo nieuwste hulpprogramma's bieden alle Hallo functies en mogelijkheden. Hallo volgende diagram toont een typische niet-beheerders toegang tot het pad.

![Toegangspad niet-beheerder](./media/sql-database-manage-logins/2sql-db-nonadmin-access.png)

## <a name="groups-and-roles"></a>Groepen en rollen
Efficiënte toegangsbeheer maakt gebruik van machtigingen worden toegewezen toogroups en rollen in plaats van afzonderlijke gebruikers. 

- Als u Azure Active Directory-verificatie gebruikt, plaatst u Azure Active Directory-gebruikers in een Azure Active Directory-groep. Een ingesloten database-gebruiker voor Hallo groep maken. Plaats een of meer gebruikers in een [databaserol](https://msdn.microsoft.com/library/ms189121) en wijs [machtigingen](https://msdn.microsoft.com/library/ms191291.aspx) toohello-databaserol.

- Wanneer u SQL Server-verificatie gebruikt, maakt u ingesloten databasegebruikers in Hallo-database. Plaats een of meer gebruikers in een [databaserol](https://msdn.microsoft.com/library/ms189121) en wijs [machtigingen](https://msdn.microsoft.com/library/ms191291.aspx) toohello-databaserol.

Hallo databaserollen zoals Hallo ingebouwde rollen kunnen worden **db_owner**, **db_ddladmin**, **db_datawriter**, **db_datareader**, **db_denydatawriter**, en **db_denydatareader**. **db_owner** is vaak gebruikte toogrant machtiging Volledig tooonly enkele gebruikers. Hallo andere vaste databaserollen zijn nuttig voor het ophalen van een eenvoudige database in ontwikkeling snel, maar worden niet aanbevolen voor de meeste productiedatabases. Bijvoorbeeld, Hallo **db_datareader** vaste databaserol verleent leestoegang tooevery tabel in Hallo-database, die gewoonlijk meer dan strikt noodzakelijk is. Het is veel beter toouse hello [rol maken](https://msdn.microsoft.com/library/ms187936.aspx) instructie toocreate uw eigen door de gebruiker gedefinieerde databaserollen en elke rol Hallo zorgvuldig minimale machtigingen die nodig zijn voor Hallo zakelijke behoeften te verlenen. Wanneer een gebruiker lid is van meerdere rollen, samenvoegen ze Hallo machtigingen van alle.

## <a name="permissions"></a>Machtigingen
Er zijn meer dan 100 machtigingen die afzonderlijk kunnen worden verleend of geweigerd in SQL Database. Veel van deze machtigingen zijn genest. Bijvoorbeeld Hallo `UPDATE` machtiging op een schema bevat Hallo `UPDATE` machtiging voor elke tabel binnen dat het schema. Net zoals in de meeste machtiging systemen overschrijft Hallo denial-of een machtiging voor een verlenen. Vanwege Hallo genest aard en Hallo aantal machtigingen kan duren zorgvuldige onderzoek toodesign een juiste machtiging system tooproperly beveiliging van uw database. Beginnen met Hallo lijst met machtigingen op [machtigingen (Database-Engine)](https://msdn.microsoft.com/library/ms191291.aspx) en bekijk Hallo [poster grootte afbeelding](http://go.microsoft.com/fwlink/?LinkId=229142) Hallo machtigingen.


### <a name="considerations-and-restrictions"></a>Overwegingen en beperkingen
Bij het beheren van aanmeldingen en gebruikers in SQL-Database, houd rekening met de volgende Hallo:

* U moet verbonden toohello **master** database bij het uitvoeren van Hallo `CREATE/ALTER/DROP DATABASE` instructies.   
* Hallo database gebruiker bijbehorende toohello **serverbeheerder** aanmelding kan niet worden gewijzigd of verwijderd. 
* Amerikaans Engels is de standaardtaal Hallo Hallo **serverbeheerder** aanmelding.
* Alleen beheerders Hallo (**serverbeheerder** aanmelding of Azure AD-beheerder) en de leden van Hallo Hallo **dbmanager** databaserol in Hallo **master** database hebben machtiging tooexecute hello `CREATE DATABASE` en `DROP DATABASE` instructies.
* U moet de hoofddatabase verbonden toohello bij het uitvoeren van Hallo `CREATE/ALTER/DROP LOGIN` instructies. Het gebruik van aanmeldingen wordt echter afgeraden. Gebruik in plaats daarvan ingesloten databasegebruikers.
* tooconnect tooa gebruikersdatabase, moet u Hallo-naam van Hallo-database in de verbindingsreeks Hallo opgeven.
* Alleen Hallo niveau van de server principal-aanmelding en Hallo leden van Hallo **loginmanager** databaserol in Hallo **master** database hebben een machtiging tooexecute hello `CREATE LOGIN`, `ALTER LOGIN`, en `DROP LOGIN` instructies.
* Bij het uitvoeren van Hallo `CREATE/ALTER/DROP LOGIN` en `CREATE/ALTER/DROP DATABASE` -instructies in een toepassing ADO.NET geparametriseerde opdrachten is niet toegestaan. Zie [Opdrachten en parameters](https://msdn.microsoft.com/library/ms254953.aspx) voor meer informatie.
* Bij het uitvoeren van Hallo `CREATE/ALTER/DROP DATABASE` en `CREATE/ALTER/DROP LOGIN` instructies, elk van deze instructies moeten Hallo alleen instructie in een batch Transact-SQL. Als deze niet overeenkomen, treedt er een fout op. Bijvoorbeeld: hello die volgende Transact-SQL controleert of Hallo database bestaat. Als dit bestaat, een `DROP DATABASE` instructie tooremove Hallo database wordt aangeroepen. Omdat Hallo `DROP DATABASE` instructie is niet alleen Hallo-instructie in batch hello, uitvoeren van de volgende Hallo Transact-SQL-instructie in een fout resulteert.

  ```
  IF EXISTS (SELECT [name]
           FROM   [sys].[databases]
           WHERE  [name] = N'database_name')
  DROP DATABASE [database_name];
  GO
  ```

* Bij het uitvoeren van Hallo `CREATE USER` instructie Hello `FOR/FROM LOGIN` optie, moet Hallo alleen instructie in een batch Transact-SQL.
* Bij het uitvoeren van Hallo `ALTER USER` instructie Hello `WITH LOGIN` optie, moet Hallo alleen instructie in een batch Transact-SQL.
* te`CREATE/ALTER/DROP` vereist dat een gebruiker Hallo `ALTER ANY USER` machtiging op Hallo-database.
* Als eigenaar van een databaserol Hallo probeert tooadd of een andere database gebruiker tooor uit die database rol verwijderen, Hallo volgende fout kan zich voordoen: **gebruiker of rol 'Name' bestaat niet in deze database.** Deze fout treedt op omdat het Hallo-gebruiker is niet zichtbaar toohello eigenaar. tooresolve dit probleem grant Hallo rol eigenaar Hallo `VIEW DEFINITION` machtiging op Hallo-gebruiker. 


## <a name="next-steps"></a>Volgende stappen

- toolearn meer informatie over firewallregels, Zie [Azure SQL Database-Firewall](sql-database-firewall-configure.md).
- Zie voor een overzicht van alle functies van het SQL-Database beveiliging Hallo [beveiligingsoverzicht SQL](sql-database-security-overview.md).
- Zie voor een zelfstudie [beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).
- Zie [Weergaven en opgeslagen procedures maken](https://msdn.microsoft.com/library/ms365311.aspx) voor meer informatie over weergaven en opgeslagen procedures.
- Zie voor meer informatie over het verlenen van toegang tooa databaseobject [toegang verlenen tooa Database-Object](https://msdn.microsoft.com/library/ms365327.aspx)
