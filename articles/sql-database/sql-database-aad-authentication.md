---
title: aaaAzure Active Directory auth - Azure SQL (overzicht) | Microsoft Docs
description: Meer informatie over het toouse Azure Active Directory voor verificatie bij SQL-Database en SQL Data Warehouse
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 08/11/2017
ms.author: rickbyh
ms.openlocfilehash: 7a63a162653b65294e11d3fa5bf39c320e742854
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-active-directory-authentication-for-authentication-with-sql-database-or-sql-data-warehouse"></a>Azure Active Directory-verificatie gebruiken voor verificatie met SQL-Database of SQL Data Warehouse
Azure Active Directory-verificatie is een mechanisme voor verbinding te maken met Azure SQL Database tooMicrosoft en [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) met behulp van identiteiten in Azure Active Directory (Azure AD). Azure AD-verificatie, kunt u Hallo identiteiten van databasegebruikers en andere Microsoft-services op één centrale locatie centraal beheren. Centrale ID-beheer biedt één plaats toomanage databasegebruikers en vereenvoudigt het beheer van machtigingen. Voordelen zijn Hallo volgende:

* Het biedt een alternatieve tooSQL Server-verificatie.
* Helpt bij het stoppen Hallo verspreiding van gebruikersidentiteiten voor databaseservers.
* Hiermee kunt wachtwoord draaien op één plaats
* Klanten kunnen met behulp van externe (AAD) groepen databasemachtigingen beheren.
* Deze kunt wachtwoorden moet opslaan voorkomen door het inschakelen van geïntegreerde Windows-verificatie en andere soorten authenticatie wordt ondersteund door Azure Active Directory.
* Azure AD-verificatie gebruikt ingesloten database gebruikers tooauthenticate identiteiten op Hallo databaseniveau.
* Azure AD biedt ondersteuning voor verificatie op basis van tokens voor toepassingen die verbinding maken met tooSQL Database.
* Azure AD-verificatie ondersteunt AD FS (domeinfederatie) of systeemeigen gebruikerswachtwoord verificatie voor een lokale Azure Active Directory zonder Domeinsynchronisatie.  
* Azure AD ondersteunt verbindingen van SQL Server Management Studio die gebruikmaken van Universal verificatie van Active Directory, waaronder de multi-factor Authentication (MFA).  MFA sterke verificatie met een bereik van eenvoudige verificatie-opties bevat: telefoonoproep, tekstbericht, smartcards en pincode of mobiele app-melding. Zie voor meer informatie [SSMS ondersteuning voor Azure AD MFA met SQL-Database en SQL Data Warehouse](sql-database-ssms-mfa-authentication.md).  

>  [!NOTE]  
>  Verbinding maken met tooSQL-Server op een virtuele machine in Azure wordt niet ondersteund met een Azure Active Directory-account. Gebruik in plaats daarvan de Active Directory-account van een domein.  

Hallo configuratiestappen bevatten Hallo tooconfigure procedures te volgen en gebruiken van Azure Active Directory-verificatie.

1. Maken en Azure AD te vullen.
2. Optioneel: Koppelen of Hallo active directory die is gekoppeld aan uw Azure-abonnement wijzigen.
3. Een Azure Active Directory-beheerder voor Azure SQL-server maken of [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
4. De clientcomputers configureren.
5. Ingesloten databasegebruikers in uw database toegewezen tooAzure AD identiteiten maken.
6. Verbinding maken met tooyour database met behulp van Azure AD-identiteiten.

> [!NOTE]
> toolearn hoe toocreate en Azure AD te vullen en vervolgens Azure AD configureren met Azure SQL Database en SQL Data Warehouse, Zie [configureren Azure AD met Azure SQL Database](sql-database-aad-authentication-configure.md).
>

## <a name="trust-architecture"></a>Architectuur van vertrouwensrelatie
Hallo volgen op hoog niveau diagram geeft een overzicht van Hallo oplossingsarchitectuur van het gebruik van Azure AD-verificatie met Azure SQL Database. Hallo gelden dezelfde concepten tooSQL Data Warehouse. toosupport Azure AD systeemeigen gebruikerswachtwoord, alleen Hallo Cloud gedeelte en Azure AD/Azure SQL Database wordt beschouwd. toosupport federatieve verificatie (of gebruikerswachtwoord voor Windows-referenties) Hallo communicatie met AD FS-blok is vereist. Hallo pijlen geven communicatiepaden.

![AAD auth-diagram][1]

Hallo geeft volgende diagram Hallo federatieve vertrouwensrelatie en hosting-relaties waarmee een client tooconnect tooa database door het indienen van een token. Hallo-token is geverifieerd door een Azure AD en wordt vertrouwd door het Hallo-database. Klant 1 kan een Azure Active Directory met systeemeigen gebruikers of een Azure AD bij federatieve gebruikers vertegenwoordigen. Klant 2 vertegenwoordigt een mogelijke oplossing, inclusief geïmporteerde gebruikers. in dit voorbeeld afkomstig is van een federatieve Azure Active Directory met AD FS worden gesynchroniseerd met Azure Active Directory. Het is belangrijk toounderstand die toegang hebben tot tooa database met behulp van Azure AD-verificatie is vereist dat Hallo hosting-abonnement is gekoppeld toohello Azure AD. Hallo moet hetzelfde abonnement gebruikte toocreate Hallo SQL Server hosting hello Azure SQL Database of SQL Data Warehouse.

![abonnement-relatie][2]

## <a name="administrator-structure"></a>Structuur van de beheerder
Wanneer u Azure AD-verificatie, zijn er twee beheerdersaccounts voor Hallo SQL Database-server; Hallo oorspronkelijke SQL Server-beheerder en hello Azure AD-beheerder. Hallo gelden dezelfde concepten tooSQL Data Warehouse. Alleen Hallo beheerder is op basis van een Azure AD-account kunt Hallo eerste Azure AD opgenomen databasegebruiker maken in een gebruikersdatabase. aanmeldingsnaam van de beheerder Hello Azure AD is een Azure AD-gebruiker of een Azure AD-groep. Wanneer Hallo beheerder een groepsaccount is, kan deze worden gebruikt door een groepslid, waardoor meerdere Azure AD-beheerders voor Hallo SQL Server-exemplaar. Met behulp van de groepsaccount als een beheerder worden beheerbaarheid doordat u toocentrally toevoegen en verwijderen van leden van de beveiligingsgroep in Azure AD zonder Hallo gebruikers of machtigingen in SQL-Database te wijzigen. Slechts één Azure AD-beheerder (een gebruiker of groep) kan op elk gewenst moment worden geconfigureerd.

![structuur van de beheerder][3]

## <a name="permissions"></a>Machtigingen
nieuwe gebruikers toocreate, hebt u Hallo `ALTER ANY USER` machtiging in Hallo-database. Hallo `ALTER ANY USER` machtiging databasegebruiker tooany kan worden verleend. Hallo `ALTER ANY USER` machtiging is ook waarover beheerdersaccounts Hallo-server en databasegebruikers Hello `CONTROL ON DATABASE` of `ALTER ON DATABASE` machtigingen nodig voor deze database en door leden van Hallo `db_owner` -databaserol.

de gebruiker van een ingesloten database in Azure SQL Database of SQL Data Warehouse toocreate, moet u toohello database met de identiteit van een Azure AD verbinden. toocreate hello eerste ingesloten databasegebruiker, moet u toohello database verbinden met behulp van een Azure AD-beheerder (die eigenaar is van de database Hallo Hallo). Dit wordt geïllustreerd in stap 4 en 5 hieronder. Elke Azure AD-verificatie is alleen mogelijk als Hallo Azure AD-beheerder voor Azure SQL Database of SQL Data Warehouse-server is gemaakt. Als hello Azure Active Directory-beheerder is verwijderd uit het Hallo-server, kunnen bestaande Azure Active Directory-gebruikers die eerder is gemaakt in SQL Server niet meer verbinding maken met toohello database met behulp van de Azure Active Directory-referenties.

## <a name="azure-ad-features-and-limitations"></a>Azure AD-functies en beperkingen
Hallo volgende leden van Azure AD kan worden ingericht in Azure SQL-server of SQL Data Warehouse:

* Systeemeigen leden: lid gemaakt in Azure AD in Hallo beheerde domein of in een domein van de klant. Zie voor meer informatie [toevoegen van uw eigen domein naam tooAzure AD](../active-directory/active-directory-add-domain.md).
* Federatieve domeinleden: lid gemaakt in Azure AD met een federatieve domein. Zie voor meer informatie [Microsoft Azure biedt nu ondersteuning voor federatie met Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/).
* Geïmporteerde leden van andere Azure AD die systeemeigen of federatieve domeinleden zijn.
* Active Directory-groepen als beveiligingsgroepen worden gemaakt.

Microsoft-accounts (zoals outlook.com, hotmail.com, live.com) of andere gastaccounts (bijvoorbeeld gmail.com, yahoo.com) worden niet ondersteund. Als u te kan aanmelden[https://login.live.com](https://login.live.com) met Hallo-account en wachtwoord, en u een Microsoft-account gebruikt, die niet wordt ondersteund voor Azure AD-verificatie voor Azure SQL Database- of Azure SQL Data Warehouse.

## <a name="connecting-using-azure-ad-identities"></a>Verbinding maken met behulp van Azure AD-identiteiten

Azure Active Directory-verificatie ondersteunt de volgende methoden van verbindende tooa database met behulp van Azure AD-identiteiten Hallo:

* Met behulp van geïntegreerde Windows-verificatie
* Met behulp van een Azure AD-principal-naam en een wachtwoord
* Met behulp van de toepassing tokenverificatie

### <a name="additional-considerations"></a>Aanvullende overwegingen

* tooenhance beheerbaarheid, raden we u een specifieke Azure AD inrichten als een beheerder een groep.   
* Slechts één Azure AD-beheerder (een gebruiker of groep) kan worden geconfigureerd voor een Azure SQL-server of Azure SQL Data Warehouse op elk gewenst moment.   
* Alleen een Azure AD-beheerder voor SQL Server kan in eerste instantie verbinding maken met toohello Azure SQL-server of Azure SQL Data Warehouse met een Azure Active Directory-account. Hallo Active Directory-beheerder kan daaropvolgende Azure AD configureren gebruikers van de database.   
* Het is raadzaam om de instelling Hallo too30 verbinding out in seconden.   
* Azure Active Directory-verificatie wordt ondersteund door SQL Server 2016 Management Studio en SQL Server Data Tools voor Visual Studio 2015 (versie 14.0.60311.1April 2016 of hoger). (Azure AD-verificatie wordt ondersteund door Hallo **.NET Framework-gegevensprovider voor SqlServer**; ten minste versie .NET Framework 4.6). Daarom Hallo nieuwste versies van deze hulpprogramma's en -gegevenslaagtoepassingen (DAC en Bacpac) Azure AD-verificatie kunnen gebruiken.   
* [ODBC versie 13,1](https://www.microsoft.com/download/details.aspx?id=53339) biedt echter ondersteuning voor Azure Active Directory-verificatie `bcp.exe` kan geen verbinding maken met Azure Active Directory-verificatie, omdat deze gebruikmaakt van een oudere ODBC-provider.   
* `sqlcmd`biedt ondersteuning voor Azure Active Directory-verificatie die begint met versie beschikbaar is via Hallo 13,1 [Downloadcentrum](http://go.microsoft.com/fwlink/?LinkID=825643).   
* SQL Server Data Tools voor Visual Studio 2015 moet ten minste Hallo April 2016-versie van Hallo Data Tools (versie 14.0.60311.1). Azure AD-gebruikers worden momenteel niet weergegeven in de Objectverkenner SSDT. Als tijdelijke oplossing weergeven Hallo gebruikers in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).   
* [Microsoft JDBC-stuurprogramma 6.0 voor SQL Server](https://www.microsoft.com/download/details.aspx?id=11774) ondersteunt Azure AD-verificatie. Zie ook [instelling Hallo verbindingseigenschappen](https://msdn.microsoft.com/library/ms378988.aspx).   
* PolyBase kan niet verifiëren met behulp van Azure AD-verificatie.   
* Azure AD-verificatie voor SQL-Database wordt ondersteund door hello Azure-portal **Database importeren** en **Database exporteren** blades. Importeren en exporteren met behulp van Azure AD-verificatie wordt ook ondersteund van Hallo PowerShell-opdracht.   
* Azure AD-verificatie wordt ondersteund voor SQL-Database en SQL Data Warehouse door gebruik CLI. Zie voor meer informatie [configureren en beheren van Azure Active Directory-verificatie met SQL-Database of SQL Data Warehouse](sql-database-aad-authentication-configure.md) en [SQL Server - az sql server](https://docs.microsoft.com/en-us/cli/azure/sql/server).

## <a name="next-steps"></a>Volgende stappen
- toolearn hoe toocreate en Azure AD te vullen en vervolgens Azure AD configureren met Azure SQL Database- of Azure SQL Data Warehouse, Zie [configureren en beheren van Azure Active Directory-verificatie met SQL-Database of SQL Data Warehouse](sql-database-aad-authentication-configure.md).
- Zie [SQL Database-toegang en -beheer](sql-database-control-access.md) voor een overzicht van toegang en beheer in SQL Database.
- Zie [Aanmeldingen, gebruikers en databaserollen](sql-database-manage-logins.md) voor een overzicht van aanmeldingen, gebruikers en databaserollen in SQL Database.
- Zie [Principals](https://msdn.microsoft.com/library/ms181127.aspx) voor meer informatie over database-principals.
- Zie [Databaserollen](https://msdn.microsoft.com/library/ms189121.aspx) voor meer informatie over databaserollen.
- Zie [SQL Database-firewallregels](sql-database-firewall-configure.md) voor meer informatie over de firewallregels in SQL Database.

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[9]: ./media/sql-database-aad-authentication/9ad-settings.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/11connect-using-int-auth.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db.png

