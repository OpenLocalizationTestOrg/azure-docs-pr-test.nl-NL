---
title: aaaSecuring PaaS-Databases in Azure | Microsoft Docs
description: " Meer informatie over Azure SQL Database en SQL Data Warehouse security best practices voor het beveiligen van uw PaaS-web- en mobiele toepassingen. "
services: security
documentationcenter: na
author: techlake
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: terrylan
ms.openlocfilehash: a7f9a2846b59dcb05e82f2ad88b41c5213295603
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-paas-databases-in-azure"></a>PaaS-databases in Azure beveiligen

In dit artikel bespreken we een verzameling van [Azure SQL Database](https://azure.microsoft.com/services/sql-database/) en [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/) aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. Deze aanbevolen procedures zijn afgeleid van onze ervaring met Azure en Hallo ervaringen van klanten, zoals zelf.

## <a name="azure-sql-database-and-sql-data-warehouse"></a>Azure SQL Database en SQL datawarehouse
[Azure SQL Database](../sql-database/sql-database-technical-overview.md) en [SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) een relationele database-service voor uw internetgebaseerde toepassingen bieden. Bekijk de services die u uw toepassingen en gegevens beschermen helpen wanneer u Azure SQL Database en SQL Data Warehouse in een PaaS-implementatie:

- Azure Active Directory-verificatie (in plaats van SQL Server-verificatie)
- Azure SQL-firewall
- Transparante gegevensversleuteling (TDE)

## <a name="best-practices"></a>Aanbevolen procedures

### <a name="use-a-centralized-identity-repository-for-authentication-and-authorization"></a>Een gecentraliseerde identiteitsopslagplaats gebruiken voor verificatie en autorisatie

Azure SQL-databases zijn geconfigureerd toouse een van twee typen verificatie:

- **SQL-verificatie** maakt gebruik van een gebruikersnaam en wachtwoord. Wanneer u de logische server Hallo voor uw database gemaakt, moet u een aanmelding 'serverbeheerder' met een gebruikersnaam en wachtwoord opgegeven. U kunt met deze referenties, tooany database op die server verifiëren als de eigenaar van de Hallo-database.

- **Azure Active Directory-verificatie** identiteiten die worden beheerd door Azure Active Directory gebruikt en wordt ondersteund voor beheerde en geïntegreerde domeinen. toouse Azure Active Directory-verificatie, moet u een andere server admin aangeroepen Hallo 'Azure AD-beheerder,' Wat is toegestaan tooadminister Azure AD-gebruikers en groepen maken. Deze beheerder kan ook alle bewerkingen uitvoeren die reguliere serverbeheerders kunnen uitvoeren.

[Azure Active Directory-verificatie](../active-directory/develop/active-directory-authentication-scenarios.md) is een mechanisme voor verbinding te maken met tooAzure SQL-Database en SQL Data Warehouse met behulp van identiteiten in Azure Active Directory (AD). Azure AD levert een alternatieve tooSQL Server-verificatie, zodat u Hallo verspreiding van gebruikersidentiteiten over databaseservers stoppen kunt. Azure AD authentication schakelt u toocentrally Hallo identiteiten van databasegebruikers en andere Microsoft-services op één locatie beheren. Centrale ID-beheer biedt één plaats toomanage databasegebruikers en vereenvoudigt het beheer van machtigingen.  

Voordelen van het gebruik van Azure AD-verificatie in plaats van de SQL-verificatie zijn:

- Kan wachtwoord draaien op één plaats.
- Beheert de databasemachtigingen met externe Azure AD-groepen.
- Elimineert wachtwoorden moet opslaan door het inschakelen van geïntegreerde Windows-verificatie en andere soorten authenticatie wordt ondersteund door Azure AD.
- Maakt gebruik van database gebruikers tooauthenticate identiteiten op Hallo databaseniveau bevat.
- Biedt ondersteuning voor verificatie op basis van tokens voor toepassingen die verbinding maken met tooSQL Database.
- Biedt ondersteuning voor AD FS (domeinfederatie) of systeemeigen gebruikerswachtwoord verificatie voor een lokale Azure AD zonder Domeinsynchronisatie.
- Ondersteunt verbindingen van SQL Server Management Studio die gebruikmaken van Universal verificatie van Active Directory, waaronder [multi-factor Authentication (MFA)](../multi-factor-authentication/multi-factor-authentication.md). MFA sterke verificatie met een bereik van eenvoudige verificatie-opties bevat: telefoonoproep, tekstbericht, smartcards en pincode of mobiele app-melding. Zie voor meer informatie [SSMS ondersteuning voor Azure AD MFA met SQL-Database en SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).

toolearn meer informatie over Azure AD-verificatie, Zie:

- [Verbinding maken met tooSQL Database of SQL Data Warehouse door met behulp van Azure Active Directory-verificatie](../sql-database/sql-database-aad-authentication.md)
- [Verificatie tooAzure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-authentication.md)
- [Ondersteuning voor verificatie op basis van tokens voor Azure SQL DB met Azure AD-verificatie](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/)

> [!NOTE]
> tooensure Azure Active Directory is geschikt voor uw omgeving, Zie [Azure AD-functies en beperkingen](../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations), specifiek Hallo aanvullende overwegingen.
>
>

### <a name="restrict-access-based-on-ip-address"></a>Toegang beperken op basis van IP-adres
U kunt firewallregels die aanvaardbaar IP-adresbereiken opgeven. Deze regels kunnen worden gericht op het Hallo-server en databaseniveaus. Aangeraden databaseniveau firewallregels wanneer mogelijke tooenhance beveiligings- en toomake uw meer draagbare database. Firewallregels op serverniveau beste kunnen worden gebruikt voor beheerders en wanneer er veel databases die Hallo hebben dezelfde vereisten voor toegang, maar u niet wilt dat toospend tijd elke database afzonderlijk configureren.

SQL-Database standaard bron IP-adresbeperkingen toestaan toegang van elk Azure-adres (inclusief andere abonnementen en tenants). U kunt deze tooonly beperken toestaan van uw IP-adressen tooaccess Hallo-exemplaar. Zelfs met uw SQL-firewall en IP-adresbeperkingen sterke authenticatie nog steeds vereist. Zie Hallo aanbevelingen eerder in dit artikel.

toolearn meer informatie over Azure SQL-Firewall en IP-beperkingen, Zie:

- [Toegangsbeheer voor Azure SQL Database](../sql-database/sql-database-control-access.md)
- [Configureren van Azure SQL Database-firewallregels - overzicht](../sql-database/sql-database-firewall-configure.md)
- [Een Azure SQL Database serverniveau firewallregel met hello Azure-portal configureren](../sql-database/sql-database-configure-firewall-settings.md)

### <a name="encryption-of-data-at-rest"></a>Versleuteling van data-at-rest
[Transparent Data Encryption (TDE)](https://msdn.microsoft.com/library/azure/bb934049) is standaard ingeschakeld. TDE versleutelt transparant SQL Server, Azure SQL Database en Azure SQL Data Warehouse-gegevens en logboekbestanden bestanden. TDE beschermd tegen inbreuk directe toegang toohello bestanden of hun back-up. Hiermee kunt u gegevens in rust tooencrypt zonder te wijzigen van bestaande toepassingen. TDE moet altijd blijven ingeschakeld; Hierdoor wordt een aanvaller met behulp van de normale toegangspad Hallo echter niet gestopt. TDE biedt Hallo mogelijkheid toocomply met veel wettelijke, en tot stand gebracht in verschillende branches richtlijnen.

Azure SQL beheert sleutel toegangsproblemen voor TDE. Zoals met TDE, on-premises extra moet op worden gelet tooensure herstelmogelijkheden en bij het verplaatsen van databases. In meer geavanceerde scenario's, Hallo-sleutels kunnen worden expliciet beheerd in Azure Key Vault via extensible key management (Zie [TDE inschakelen op de SQL Server met behulp van EKM](/security/encryption/enable-tde-on-sql-server-using-ekm)). Hierdoor kunnen ook voor Bring Your Own Key (BYOK) via Azure sleutel kluizen BYOK-mogelijkheden.

Azure SQL biedt versleuteling voor de kolommen via [altijd versleuteld](/sql/relational-databases/security/encryption/always-encrypted-database-engine). Hierdoor kan alleen geautoriseerde toepassingen toegang toosensitive kolommen. SQL-query's voor versleutelde kolommen tooequality gebaseerde waarden met behulp van deze versleuteling worden beperkt.

Versleuteling van toepassing op moet ook worden gebruikt voor de geselecteerde gegevens. Gegevens onafhankelijkheid problemen kunnen soms worden voorkomen door gegevens te coderen met een sleutel die wordt opgeslagen in de juiste land Hallo. Dit voorkomt dat zelfs onbedoeld gegevensoverdracht een probleem veroorzaken, omdat het onmogelijk toodecrypt Hallo gegevens zonder Hallo-sleutel, ervan uitgaande dat een sterke-algoritme wordt gebruikt (zoals AES 256).

U kunt aanvullende voorzorgsmaatregelen toohelp beveiligde Hallo database zoals ontwerpen van een beveiligde systeem, vertrouwelijk assets coderen en bouwen van een firewall rond Hallo databaseservers gebruiken.

## <a name="next-steps"></a>Volgende stappen
In dit artikel geïntroduceerd u tooa verzameling SQL-Database en SQL Data Warehouse aanbevolen beveiligingsprocedures voor het beveiligen van uw PaaS-webtoepassingen en mobiele toepassingen. toolearn meer informatie over het beveiligen van uw PaaS-implementaties, Zie:

- [PaaS-implementaties beveiligen](security-paas-deployments.md)
- [PaaS-webtoepassingen en mobiele toepassingen met Azure App Services beveiligen](security-paas-applications-using-app-services.md)
