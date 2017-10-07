---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: Azure Active Directory (AAD) en SQL Server-verificatie tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a>Verificatie tooAzure SQL Data Warehouse
> [!div class="op_single_selector"]
> * [Overzicht van beveiliging](sql-data-warehouse-overview-manage-security.md)
> * [Verificatie](sql-data-warehouse-authentication.md)
> * [Versleuteling (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Versleuteling (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

tooconnect tooSQL Data Warehouse, u moet doorgeven beveiligingsreferenties voor verificatiedoeleinden. Bij het maken van een verbinding, worden bepaalde verbindingsinstellingen geconfigureerd als onderdeel van uw query-sessie tot stand brengen.  

Voor meer informatie over beveiliging en hoe tooenable verbindingen tooyour datawarehouse Zie [beveiligen van een database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].

## <a name="sql-authentication"></a>SQL-verificatie
tooconnect tooSQL Data Warehouse, moet u Hallo volgende informatie opgeven:

* Volledig gekwalificeerde servernaam
* Geef de SQL-verificatie
* Gebruikersnaam
* Wachtwoord
* Standaard-database (optioneel)

Standaard uw verbinding toohello *master* database en niet de gebruikersdatabase. tooconnect tooyour gebruikersdatabase, kunt u toodo twee dingen:

* Geef de standaarddatabase Hallo bij het registreren van uw server met SQL Server-Objectverkenner in SSDT, SSMS, of in de verbindingsreeks voor de toepassing hello. Zo bevatten Hallo InitialCatalog, is de parameter voor een ODBC-verbinding.
* Markeer de gebruikersdatabase Hallo voordat het maken van een sessie in SSDT.

> [!NOTE]
> Hallo Transact-SQL-instructie **gebruik MijnDatabase;** wordt niet ondersteund voor het Hallo-database voor een verbinding te wijzigen. Zie voor instructies over het verbinden van tooSQL Data Warehouse met SSDT toohello [Query met Visual Studio] [ Query with Visual Studio] artikel.
> 
> 

## <a name="azure-active-directory-aad-authentication"></a>Verificatie met Azure Active Directory (AAD)
[Azure Active Directory] [ What is Azure Active Directory] verificatie is een mechanisme voor verbinding te maken met tooMicrosoft Azure SQL Data Warehouse met behulp van identiteiten in Azure Active Directory (Azure AD). Azure Active Directory-verificatie, kunt u Hallo identiteiten van databasegebruikers en andere Microsoft-services op één centrale locatie centraal beheren. Centrale ID-beheer biedt één plaats toomanage SQL Data Warehouse-gebruikers en vereenvoudigt het beheer van machtigingen. 

### <a name="benefits"></a>Voordelen
Azure Active Directory-voordelen zijn:

* Biedt een alternatieve tooSQL Server-verificatie.
* Helpt bij het stoppen Hallo verspreiding van gebruikersidentiteiten voor databaseservers.
* Hiermee kunt wachtwoord draaien op één plaats
* Databasemachtigingen met behulp van externe (AAD)-groepen beheren.
* Elimineert wachtwoorden moet opslaan door het inschakelen van geïntegreerde Windows-verificatie en andere soorten authenticatie wordt ondersteund door Azure Active Directory.
* Maakt gebruik van database gebruikers tooauthenticate identiteiten op Hallo databaseniveau bevat.
* Biedt ondersteuning voor verificatie op basis van tokens voor toepassingen die verbinding maken met tooSQL Data Warehouse.
* Ondersteunt multi-factor authentication via universele verificatie van Active Directory voor SQL Server Management Studio. Zie voor een beschrijving van multi-factor Authentication [SSMS ondersteuning voor Azure AD MFA met SQL-Database en SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

> [!NOTE]
> Azure Active Directory is nog relatief nieuw en bevat enkele beperkingen. tooensure Azure Active Directory is geschikt voor uw omgeving, Zie [Azure AD-functies en beperkingen][Azure AD features and limitations], specifiek Hallo aanvullende overwegingen.
> 
> 

### <a name="configuration-steps"></a>Configuratiestappen
Volg deze stappen tooconfigure Azure Active Directory-verificatie.

1. U maakt en vult u een Azure Active Directory
2. Optioneel: Koppelen of Hallo active directory die is gekoppeld aan uw Azure-abonnement wijzigen
3. Een Azure Active Directory-beheerder voor Azure SQL Data Warehouse maken.
4. De clientcomputers configureren
5. Ingesloten databasegebruikers in uw database toegewezen tooAzure AD identiteiten maken
6. Verbinding maken met DataWarehouse tooyour met behulp van Azure AD-identiteiten

Azure Active Directory-gebruikers worden momenteel niet weergegeven in de Objectverkenner SSDT. Als tijdelijke oplossing weergeven Hallo gebruikers in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).

### <a name="find-hello-details"></a>Hallo-informatie
* Hallo stappen tooconfigure en gebruik Azure Active Directory-verificatie zijn bijna identiek zijn voor Azure SQL Database en Azure SQL Data Warehouse. Ga als volgt Hallo gedetailleerde stappen in Hallo onderwerp [verbinding maakt met tooSQL Database of SQL Data Warehouse door met behulp van Azure Active Directory-verificatie](../sql-database/sql-database-aad-authentication.md).
* Aangepaste databaserollen maken en toevoegen van gebruikers toohello rollen. Verleen gedetailleerde machtigingen toohello rollen. Zie voor meer informatie [aan de slag met machtigingen voor Database-Engine](https://msdn.microsoft.com/library/mt667986.aspx).

## <a name="next-steps"></a>Volgende stappen
toostart opvragen van uw datawarehouse met Visual Studio en andere toepassingen, Zie [Query met Visual Studio][Query with Visual Studio].

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
