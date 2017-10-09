---
title: aaaMulti-Factor authentication - Azure SQL | Microsoft Docs
description: Gebruik Multi meeberekend verificatie met SSMS voor SQL-Database en SQL datawarehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: fbd6e644-0520-439c-8304-2e4fb6d6eb91
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/19/2017
ms.author: rickbyh
ms.openlocfilehash: 57ef63b7c7f2c5cf64c3e1ee194d865ee5b14177
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="universal-authentication-with-sql-database-and-sql-data-warehouse-ssms-support-for-mfa"></a>Universele verificatie met SQL-Database en SQL Data Warehouse (SSMS ondersteuning voor MFA)
Azure SQL Database en Azure SQL Data Warehouse ondersteunen verbindingen van het gebruik van SQL Server Management Studio (SSMS) *Universal verificatie van Active Directory*. 
**Download nieuwste SSMS Hallo** : klik op de clientcomputer Hallo Hallo meest recente versie van SSMS, downloaden van [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Voor alle Hallo-functies in dit onderwerp, gebruikt u ten minste versie 17,2 juli 2017.  Hallo meest recente verbinding in het dialoogvenster ziet er als volgt: ![1mfa universal verbinding](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png "Completes vak Gebruikersnaam Hallo.")  

## <a name="hello-five-authentication-options"></a>Hallo vijf verificatieopties  
- Universele verificatie van Active Directory ondersteunt Hallo twee niet-interactieve verificatiemethoden (`Active Directory - Password` verificatie en `Active Directory - Integrated` verificatie). Niet-interactieve `Active Directory - Password` en `Active Directory - Integrated` verificatiemethoden kunnen worden gebruikt in veel verschillende toepassingen (ADO.NET, JDBC, ODBC, enzovoort). Deze twee methoden worden nooit leiden tot pop-dialoogvensters.

- `Active Directory - Universal with MFA`verificatie is een interactieve methode die ook ondersteunt *Azure multi-factor Authentication* (MFA). Azure MFA helpt beveiliging toegang toodata en toepassingen en te voldoen aan de behoeften van de gebruiker voor een eenvoudig proces aanmelden. Sterke verificatie met een bereik van eenvoudige verificatie-opties (telefoongesprek, tekstbericht, smartcards en pincode of mobiele-appmelding), waardoor gebruikers toochoose Hallo wijze levert. Interactieve MFA met Azure AD kan resulteren in een pop-dialoogvenster voor validatie.

Zie voor een beschrijving van multi-factor Authentication [multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication.md).
Zie voor configuratiestappen [Azure SQL-Database configureren multi-factor authentication voor SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).

### <a name="azure-ad-domain-name-or-tenant-id-parameter"></a>Azure AD domain parameter name of tenant-ID   

Beginnen met [SSMS versie 17](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), gebruikers die worden geïmporteerd in Hallo huidige Active Directory van andere Azure Active Directory's als gastgebruikers kunnen hello Azure AD-domeinnaam opgeven of tenant-ID wanneer ze verbinding maken. Gastgebruikers bevatten de gebruikers van andere Azure-advertenties, Microsoft-accounts, zoals outlook.com, hotmail.com, live.com of andere accounts, zoals gmail.com uitgenodigd. Deze informatie kan **Active Directory Universal met MFA verificatie** tooidentify Hallo juiste verificatie-instantie. Deze optie is ook vereist toosupport Microsoft-accounts (MSA) zoals outlook.com, hotmail.com, live.com of niet-mailaccount. Deze gebruikers willen toobe geverifieerd met behulp van universele verificatie moet invoeren hun Azure AD-domeinnaam of de tenant-id. Deze parameter geeft Hallo huidige Azure AD-domein naam/tenant-ID hello die Azure-Server is gekoppeld aan. Bijvoorbeeld, als Azure-Server is gekoppeld aan Azure AD-domein `contosotest.onmicrosoft.com` waar gebruiker `joe@contosodev.onmicrosoft.com` wordt gehost als een geïmporteerde gebruiker in Azure AD-domein `contosodev.onmicrosoft.com`, domain name vereist tooauthenticate deze gebruiker is Hallo `contosotest.onmicrosoft.com`. Wanneer gebruiker Hallo een systeemeigen hello Azure AD gekoppeld tooAzure Server-gebruiker en niet een MSA-account is, is geen domein naam of het tenant-ID vereist. tooenter hello parameter (begin met SSMS versie 17,2) in Hallo **tooDatabase verbinding** dialoogvenster, volledige Hallo dialoogvenster selecteren **Active Directory - Universal met MFA** -verificatie Klik op **opties**, volledige Hallo **gebruikersnaam** vak en klik vervolgens op Hallo **verbindingseigenschappen** tabblad. Controleer Hallo **AD-domein naam of het tenant-ID** vak en bieden verificatieautoriteit zoals Hallo domeinnaam (**contosotest.onmicrosoft.com**) of Hallo GUID van Hallo tenant-ID.  
   ![MFA-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   

### <a name="azure-ad-business-toobusiness-support"></a>Ondersteuning voor Azure AD business toobusiness   
Azure AD-gebruikers ondersteund voor Azure AD B2B-scenario's als gastgebruikers (Zie [wat is Azure B2B-samenwerking](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md)) verbinding kunnen maken tooSQL Database en SQL Data Warehouse uitsluitend als onderdeel van de leden van een groep gemaakt in huidige Azure AD en handmatig toegewezen met behulp van Transact-SQL Hallo `CREATE USER` -instructie in een bepaalde database. Bijvoorbeeld, als `steve@gmail.com` uitgenodigde tooAzure AD is `contosotest` (met Azure Ad-domein Hallo `contosotest.onmicrosoft.com`), een Azure AD-groep, zoals `usergroup` moeten worden gemaakt in Azure AD met Hallo Hallo `steve@gmail.com` lid. Vervolgens deze groep moet worden gemaakt voor een specifieke database (dat wil zeggen MijnDatabase) door Azure AD-SQL-beheerder of Azure AD DBO door het uitvoeren van een Transact-SQL `CREATE USER [usergroup] FROM EXTERNAL PROVIDER` instructie. Nadat het Hallo-databasegebruiker is gemaakt, klikt u vervolgens gebruiker Hallo `steve@gmail.com` te kunnen aanmelden`MyDatabase` met behulp van SSMS-verificatieoptie Hallo `Active Directory – Universal with MFA support`. Hallo usergroup, standaard heeft alleen Hallo verbinding maken met de machtiging en eventuele verdere gegevenstoegang die toobe verleend in Hallo moet normale wijze. Houd rekening met die gebruiker `steve@gmail.com` als gastgebruiker moet Hallo selectievakje en Hallo AD domeinnaam toevoegen `contosotest.onmicrosoft.com` in Hallo SSMS **verbindingseigenschap** in het dialoogvenster. Hallo **AD-domein naam of het tenant-ID** optie wordt alleen ondersteund voor Hallo Universal met MFA verbindingsopties, anders het wordt grijs.

## <a name="universal-authentication-limitations-for-sql-database-and-sql-data-warehouse"></a>Universele verificatie beperkingen voor de SQL-Database en SQL Data Warehouse
* SSMS en SqlPackage.exe zijn Hallo alleen extra momenteel ingeschakeld voor MFA via universele verificatie van Active Directory.
* SSMS versie 17,2, ondersteunt gelijktijdige toegang door meerdere gebruikers met Universal verificatie met MFA. Een logboek in beperkt versie 17,0 en 17.1, voor een exemplaar van SSMS met Universal verificatie tooa enkele Azure Active Directory-account. toolog in als een andere Azure AD-account, moet u een ander exemplaar van SSMS. (Deze beperking is beperkt tooActive Universal Directory-verificatie; u kunt aanmelden met toodifferent servers met Active Directory-wachtwoordverificatie of geïntegreerde verificatie van Active Directory SQL Server-verificatie).
* SSMS ondersteunt Universal verificatie van Active Directory voor Object Explorer, Query-Editor en Query Store visualisatie.
* SSMS versie 17,2 biedt DacFx Wizard ondersteuning voor de database van de gegevens uitpakken-Export/implementeren. Als een specifieke gebruiker is geverifieerd via Hallo eerste verificatiedialoogvenster Universal-verificatie, hello DacFx Wizard functies Hallo dezelfde manier als bij alle andere verificatiemethoden te gebruiken.
* Hallo SSMS ontwerpfunctie ondersteunt geen universele verificatie.
* Er zijn geen extra software-vereisten voor universele verificatie van Active Directory, behalve dat u een ondersteunde versie van SSMS moet gebruiken.  
* Hallo Active Directory Authentication Library (ADAL) versie voor universele verificatie is bijgewerkte tooits nieuwste ADAL.dll 3.13.9 beschikbaar vrijgegeven versie. Zie [Active Directory Authentication Library 3.14.1](http://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/).


## <a name="next-steps"></a>Volgende stappen

- Zie voor configuratiestappen [Azure SQL-Database configureren multi-factor authentication voor SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).
- Anderen tooyour database toegang kunt krijgen: [SQL Database-verificatie en autorisatie: toegang verlenen](sql-database-manage-logins.md)  
- Zorg ervoor dat anderen verbinding kunnen maken via de firewall Hallo: [configureren een Azure SQL Database serverniveau firewall regel met hello Azure-portal](sql-database-configure-firewall-settings.md)  
- [Configureren en beheren van Azure Active Directory-verificatie met SQL-Database of SQL Data Warehouse](sql-database-aad-authentication-configure.md)  
- [Framework voor Microsoft SQL Server-Gegevenslaagtoepassingen (17.0.0 GA)](https://www.microsoft.com/download/details.aspx?id=55088)  
- [SQLPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)  
- [Een Bacpac-bestand tooa importeren nieuwe Azure SQL Database](../sql-database/sql-database-import.md)  
- [Een Azure SQL database tooa Bacpac-bestand exporteren](../sql-database/sql-database-export.md)  
- C#-interface [IUniversalAuthProvider-Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx)  
