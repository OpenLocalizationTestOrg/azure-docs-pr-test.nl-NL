---
title: aaaGranting toegang tooAzure SQL-Database | Microsoft Docs
description: Meer informatie over het verlenen van toegang tooMicrosoft Azure SQL Database.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 8e71b04c-bc38-4153-8f83-f2b14faa31d9
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/06/2017
ms.author: rickbyh
ms.openlocfilehash: 4c32fafa7e98b731ff2f9bf4666da7e4a3145286
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-access-control"></a>Toegangsbeheer voor Azure SQL Database
tooprovide beveiligingsmaatregelen, SQL Database toegang met firewallregels connectiviteit beperken door IP-adres, verificatiemechanismen vereisen tooprove gebruikers hun identiteit en autorisatiemechanismen gebruikers toospecific acties en gegevens te beperken. 

> [!IMPORTANT]
> Zie voor een overzicht van beveiligingsfuncties van Hallo SQL-Database [beveiligingsoverzicht SQL](sql-database-security-overview.md). Zie voor een zelfstudie [beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).

## <a name="firewall-and-firewall-rules"></a>Firewall en firewallregels
Microsoft Azure SQL Database levert een relationele-databaseservice voor Azure en andere op internet gebaseerde toepassingen. toohelp uw gegevens beschermen, firewalls te voorkomen dat alle toegang tooyour-databaseserver totdat u opgeven welke computers over machtigingen beschikken. Hallo firewall verleent toegang toodatabases op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn. Zie [Overzicht van de firewallregels voor SQL Database](sql-database-firewall-configure.md) voor meer informatie.

Hello Azure SQL Database-service is alleen beschikbaar via TCP-poort 1433. tooaccess een SQL-Database van uw computer, zorg ervoor dat de firewall van uw client-computer uitgaande TCP-communicatie op TCP-poort 1433 toestaat. Blokkeer binnenkomende verbindingen op TCP-poort 1433 als u deze niet nodig hebt voor andere toepassingen. 

Als onderdeel van het verbindingsproces hello zijn de verbindingen van virtuele machines in Azure omgeleide tooa verschillende IP-adres en poort, uniek zijn voor elke worker-rol. Hallo-poortnummer is Hallo tussen 11000 too11999 liggen. Zie voor meer informatie over de TCP-poorten, [poorten buiten 1433 voor ADO.NET 4.5 en SQL Database2](sql-database-develop-direct-route-ports-adonet-v12.md).

## <a name="authentication"></a>Authentication

SQL Database ondersteunt twee typen verificatie:

* **SQL-verificatie**, waarbij een gebruikersnaam en wachtwoord worden gebruikt. Wanneer u de logische server Hallo voor uw database gemaakt, moet u een aanmelding 'serverbeheerder' met een gebruikersnaam en wachtwoord opgegeven. Met deze referenties, kunt u verifiëren tooany database op die server als Hallo database-eigenaar of "dbo." 
* **Azure Active Directory-verificatie**, waarbij identiteiten worden gebruikt die worden beheerd in Azure Active Directory. Deze methode wordt ondersteund voor beheerde en geïntegreerde domeinen. Gebruik [waar mogelijk](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) Active Directory-verificatie (geïntegreerde beveiliging). Als u toouse Azure Active Directory-verificatie wilt, moet u een andere server admin aangeroepen Hallo 'Azure AD-beheerder,' Wat is toegestaan tooadminister Azure AD-gebruikers en groepen maken. Deze beheerder kan ook alle bewerkingen uitvoeren die reguliere serverbeheerders kunnen uitvoeren. Zie [tooSQL Database met behulp van Azure Active Directory-verificatie verbinding te maken](sql-database-aad-authentication.md) voor een overzicht van hoe toocreate een Azure AD-beheerder tooenable Azure Active Directory-verificatie.

Hallo Database-Engine wordt gesloten verbindingen die gedurende meer dan 30 minuten inactief. Hallo verbinding aanmelding opnieuw moet voordat deze kan worden gebruikt. Continu actieve verbindingen tooSQL Database opnieuw autoriseren (uitgevoerd door database-engine Hallo) vereist ten minste elke 10 uur. Hallo database-engine probeert opnieuw autoriseren hello oorspronkelijk verzonden wachtwoord en geen invoer van gebruiker is vereist. Voor betere prestaties wanneer een wachtwoordherstel in SQL-Database, Hallo verbinding is niet geverifieerd, zelfs als Hallo verbinding wordt hersteld vanwege tooconnection groeperen. Dit wijkt af van Hallo gedrag van lokale SQL Server. Hallo-wachtwoord is gewijzigd sinds het Hallo-verbinding in eerste instantie is geautoriseerd, Hallo verbinding moet worden afgesloten als een nieuwe verbinding gemaakt met behulp van het nieuwe wachtwoord Hallo. Een gebruiker met Hallo `KILL DATABASE CONNECTION` machtiging kunt expliciet afsluiten van een verbinding tooSQL Database met behulp van Hallo [KILL](https://docs.microsoft.com/sql/t-sql/language-elements/kill-transact-sql) opdracht.

Gebruikersaccounts kunnen worden gemaakt in de hoofddatabase Hallo en machtigingen in alle databases op Hallo server kunnen worden verleend, of ze kunnen worden gemaakt in het Hallo-database zelf (ook wel ingesloten gebruikers genoemd). Zie [Aanmeldingen beheren](sql-database-manage-logins.md) voor informatie over het maken en beheren van aanmeldingen. tooenhance draagbaarheid en schaalbaarheid, gebruikt de ingesloten database gebruikers tooenhance schaalbaarheid. Zie [Contained Database Users - Making Your Database Portable](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) (Ingesloten databasegebruikers: een draagbare database maken), [CREATE USER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-user-transact-sql) (GEBRUIKER MAKEN (Transact-SQL)) en [Contained Databases](https://docs.microsoft.com/sql/relational-databases/databases/contained-databases) (Ingesloten databases) voor meer informatie.

Als een best practice moet toepassingen gebruikmaken van een specifiek account tooauthenticate--deze manier kunt u Hallo machtigingen verleend toohello toepassing beperken en Hallo risico's van schadelijke activiteiten te verminderen voor het geval de toepassingscode kwetsbaar tooa SQL-injectie is aanval. Hallo aanbevolen aanpak is toocreate een [ingesloten databasegebruiker](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable), waarmee uw app tooauthenticate rechtstreeks toohello database. 

## <a name="authorization"></a>Autorisatie

Autorisatie toowhat verwijst een gebruiker binnen een Azure SQL Database kunt uitvoeren, en dit wordt bepaald door uw gebruikersaccount database [rollidmaatschappen](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) en [op objectniveau machtigingen](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine). Als een best practice moet u gebruikers Hallo verlenen minimaal benodigde bevoegdheden nodig zijn. Hallo beheerder serveraccount die u verbinding met maakt is lid van db_owner autoriteit toodo met Alles binnen het Hallo-database. Gebruik dit account voor het implementeren van schema-updates en andere beheerbewerkingen. Hallo 'ApplicationUser' account gebruiken met meer beperkte machtigingen tooconnect uit de database van uw toepassing toohello Hello minimaal benodigde bevoegdheden die nodig is voor uw toepassing. Zie [Aanmeldingen beheren](sql-database-manage-logins.md) voor meer informatie.

Normaal gesproken alleen beheerders moeten toegang tot toohello `master` database. Routinematig toegang tooeach gebruikersdatabase moet via niet-beheerders ingesloten databasegebruikers in elke database gemaakt. Wanneer u ingesloten databasegebruikers gebruikt, hoeft u niet toocreate-aanmeldingen in Hallo `master` database. Zie [Ingesloten databasegebruikers: een draagbare database maken](https://docs.microsoft.com/sql/relational-databases/security/contained-database-users-making-your-database-portable) voor meer informatie.

U moet vertrouwd raken met de volgende kenmerken die kunnen worden gebruikt toolimit of machtigingen verhogen Hallo:   
* [Imitatie](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server) en [ondertekening van de module](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/signing-stored-procedures-in-sql-server) kunnen worden gebruikt toosecurely machtigingen verhogen tijdelijk.
* [Beveiliging op rijniveau](https://docs.microsoft.com/sql/relational-databases/security/row-level-security) kan worden gebruikt om de rijen waartoe een gebruiker toegang heeft te beperken.
* [De Gegevensmaskeringsfunctie](sql-database-dynamic-data-masking-get-started.md) gebruikte toolimit blootstelling van gevoelige gegevens kunnen worden.
* [Opgeslagen procedures](https://docs.microsoft.com/sql/relational-databases/stored-procedures/stored-procedures-database-engine) gebruikte toolimit Hallo-acties die kunnen worden uitgevoerd op Hallo-database kan worden.

## <a name="next-steps"></a>Volgende stappen

- Zie voor een overzicht van beveiligingsfuncties van Hallo SQL-Database [beveiligingsoverzicht SQL](sql-database-security-overview.md).
- toolearn meer informatie over firewallregels, Zie [Firewall-regels](sql-database-firewall-configure.md).
- toolearn over gebruikers en -aanmeldingen, Zie [aanmeldingen beheren](sql-database-manage-logins.md). 
- Zie voor een beschrijving van de proactieve controle, [Database Auditing](sql-database-auditing.md) en [SQL Database met detectie van dreigingen](sql-database-threat-detection.md).
- Zie voor een zelfstudie [beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).
