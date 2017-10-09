---
title: aaaAzure beveiligingsoverzicht van SQL Database | Microsoft Docs
description: Meer informatie over Azure SQL Database en SQL Server-beveiliging, waaronder een Hallo verschillen tussen Hallo cloud- en SQL Server on-premises wanneer deze tooauthentication, autorisatie verbindingsbeveiliging, versleuteling en naleving wordt.
services: sql-database
documentationcenter: 
author: tmullaney
manager: jhubbard
editor: 
ms.assetid: a012bb85-7fb4-4fde-a2fc-cf426c0a56bb
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 07/05/2017
ms.author: thmullan;jackr
ms.openlocfilehash: 7b0b0d1b59ec4018d9fb668bc8b6b56c9907e982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-your-sql-database"></a>Uw SQL Database beveiligen

In dit artikel wordt uitgelegd Hallo basisprincipes van beveiliging gegevenslaag Hallo van een toepassing met Azure SQL Database. Dit artikel helpt u in het bijzonder om aan de slag te gaan met resources voor gegevensbeveiliging, toegangsbeheer en proactieve controle. 

Zie voor een volledig overzicht van beveiligingsfuncties die beschikbaar zijn op alle versies van SQL, Hallo [Beveiligingscentrum voor SQL Server Database Engine en Azure SQL Database](https://msdn.microsoft.com/library/bb510589). Aanvullende informatie is ook beschikbaar in Hallo [beveiligings- en Azure SQL Database technisch rapport](https://download.microsoft.com/download/A/C/3/AC305059-2B3F-4B08-9952-34CDCA8115A9/Security_and_Azure_SQL_Database_White_paper.pdf) (PDF).

## <a name="protect-data"></a>Gegevens beveiligen
Uw gegevens worden beveiligd met SQL Database via gegevensversleuteling. Voor gegevens die in beweging zijn, wordt [Transport Layer Security](https://support.microsoft.com/kb/3135244) gebruikt, voor data-at-rest [Transparent Data Encryption](http://go.microsoft.com/fwlink/?LinkId=526242) en voor gebruikte gegevens [Altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx). 

> [!IMPORTANT]
>Alle verbindingen tooAzure SQL-Database versleuteling vereisen (SSL/TLS) op alle tijden als gegevens 'in transit' tooand uit Hallo-database. In de verbindingsreeks van uw toepassing, moet u parameters tooencrypt Hallo verbinding opgeven en *niet* tootrust Hallo servercertificaat (dit wordt gedaan voor u als u de verbindingsreeks van kopieert Hallo klassieke Azure-Portal) anders is Hallo verbinding wordt Hallo identiteit van Hallo-server niet controleren en vatbaar te 'man-in-the-middle'-aanvallen. Voor Hallo ADO.NET stuurprogramma, bijvoorbeeld deze parameters voor de verbindingsreeks zijn **versleutelen = True** en **TrustServerCertificate = False**. 

Voor andere manieren tooencrypt kunt uw gegevens:

* [-Celcodering](https://msdn.microsoft.com/library/ms179331.aspx) tooencrypt bepaalde kolommen of zelfs cellen van gegevens met verschillende versleutelingssleutels.
* Als u een Hardware Security Module of centraal beheer van uw versleutelingssleutelhiërarchie nodig heeft, kunt u overwegen om [Azure Key Vault met SQL Server in een virtuele Azure-machine](http://blogs.technet.com/b/kv/archive/2015/01/12/using-the-key-vault-for-sql-server-encryption.aspx) te gebruiken.

## <a name="control-access"></a>Toegang beheren
SQL-Database beveiligt uw gegevens door te beperken van toegang tooyour database met behulp van firewallregels, verificatiemechanismen vereisen tooprove gebruikers hun identiteit en autorisatie toodata via lidmaatschappen op basis van rollen en machtigingen, evenals via beveiliging en dynamische gegevensmaskering. Zie voor een beschrijving van Hallo gebruik van de access control-functies in SQL-Database [toegangsbeheer](sql-database-control-access.md).

> [!IMPORTANT]
> Het beheer van databases en logische servers in Azure wordt bepaald door de roltoewijzingen voor uw Portal-gebruikersaccount. Zie [Op rollen gebaseerd toegangsbeheer in Azure Portal](../active-directory/role-based-access-control-what-is.md) voor meer informatie over dit onderwerp.
>

### <a name="firewall-and-firewall-rules"></a>Firewall en firewallregels
toohelp uw gegevens beschermen, firewalls te voorkomen dat alle toegang tooyour-databaseserver totdat u opgeven welke computers zijn met behulp van machtiging [firewall-regels](sql-database-firewall-configure.md). Hallo firewall verleent toegang toodatabases op basis van Hallo IP-adres van elke aanvraag die afkomstig zijn.

### <a name="authentication"></a>Authentication
SQL database-verificatie verwijst toohow u uw identiteit bewijzen bij het verbinden van toohello database. SQL Database ondersteunt twee typen verificatie:

* **SQL-verificatie**, waarbij een gebruikersnaam en wachtwoord worden gebruikt. Wanneer u de logische server Hallo voor uw database gemaakt, moet u een aanmelding 'serverbeheerder' met een gebruikersnaam en wachtwoord opgegeven. Met deze referenties, kunt u verifiëren tooany database op die server als Hallo database-eigenaar of "dbo." 
* **Azure Active Directory-verificatie**, waarbij identiteiten worden gebruikt die worden beheerd in Azure Active Directory. Deze methode wordt ondersteund voor beheerde en geïntegreerde domeinen. Gebruik [waar mogelijk](https://msdn.microsoft.com/library/ms144284.aspx) Active Directory-verificatie (geïntegreerde beveiliging). Als u toouse Azure Active Directory-verificatie wilt, moet u een andere server admin aangeroepen Hallo 'Azure AD-beheerder,' Wat is toegestaan tooadminister Azure AD-gebruikers en groepen maken. Deze beheerder kan ook alle bewerkingen uitvoeren die reguliere serverbeheerders kunnen uitvoeren. Zie [tooSQL Database met behulp van Azure Active Directory-verificatie verbinding te maken](sql-database-aad-authentication.md) voor een overzicht van hoe toocreate een Azure AD-beheerder tooenable Azure Active Directory-verificatie.

### <a name="authorization"></a>Autorisatie
Autorisatie verwijst toowhat een gebruiker binnen een Azure SQL Database kunt uitvoeren en dit wordt beheerd door uw gebruikersaccount database rollidmaatschappen en op objectniveau machtigingen. Als een best practice moet u gebruikers Hallo verlenen minimaal benodigde bevoegdheden nodig zijn. Hallo beheerder serveraccount die u verbinding met maakt is lid van db_owner autoriteit toodo met Alles binnen het Hallo-database. Gebruik dit account voor het implementeren van schema-updates en andere beheerbewerkingen. Hallo 'ApplicationUser' account gebruiken met meer beperkte machtigingen tooconnect uit de database van uw toepassing toohello Hello minimaal benodigde bevoegdheden die nodig is voor uw toepassing.

### <a name="row-level-security"></a>Beveiliging op rijniveau
Beveiliging op rijniveau kunt klanten toocontrol toegang toorows in een databasetabel op basis van kenmerken Hallo van Hallo gebruiker (bijv, groep lidmaatschap of -uitvoering context) van een query uit te voeren. Zie [Beveiliging op rijniveau](https://msdn.microsoft.com/library/dn765131) voor meer informatie.

### <a name="data-masking"></a>Gegevensmaskering 
Gevoelige gegevens blootstelling SQL-Database dynamische-gegevensmaskering beperkt door het toonon beheerdersmogelijkheden maskeren. Dynamische-gegevensmaskering automatisch gedetecteerd potentieel gevoelige gegevens in Azure SQL Database en uitvoerbare aanbevelingen toomask van deze velden met minimale gevolgen voor de toepassingslaag Hallo biedt. Hierbij worden obfuscating Hallo gevoelige gegevens in de resultatenset Hallo van een query over aangewezen databasevelden, terwijl het Hallo-gegevens in Hallo-database wordt niet gewijzigd. Zie voor meer informatie [aan de slag met SQL-Database dynamische-gegevensmaskering](sql-database-dynamic-data-masking-get-started.md) gebruikte toolimit blootstelling van gevoelige gegevens kunnen worden.

## <a name="proactive-monitoring"></a>Proactieve controle
Uw gegevens worden beveiligd met SQL Database met behulp van mogelijkheden voor controle en detectie van dreigingen. 

### <a name="auditing"></a>Controleren
SQL Database Auditing databaseactiviteiten houdt en helpt u toomaintain naleving van regelgeving, door het vastleggen van gebeurtenissen tooan audit databaselogboek in uw Azure Storage-account. Controle kunt u toounderstand database lopende activiteiten, evenals analyseren en onderzoeken van mogelijke bedreigingen van historische activiteit tooidentify of verdachte schendingen van misbruik en beveiliging. Zie [Get started with SQL Database Auditing](sql-database-auditing.md) (Aan de slag met SQL Database Auditing) voor aanvullende informatie.  

### <a name="threat-detection"></a>Detectie van bedreigingen
Detectie van dreigingen is een aanvulling op controle, dankzij een extra laag van beveiliging intelligence ingebouwd in hello Azure SQL Database-service die ongebruikelijke en potentieel schadelijke aanvallen tooaccess of misbruik databases is gedetecteerd. U wordt gewaarschuwd over verdachte activiteiten, potentiële beveiligingslekken naar voren SQL-injectieaanvallen en database afwijkende toegangspatronen. Dagelijks geconstateerde waarschuwingen kunnen bekeken worden vanuit [Azure Security Center](https://azure.microsoft.com/services/security-center/) en Geef details op van de verdachte activiteit en de aanbevolen actie voor het tooinvestigate en Hallo bedreigingen te verhelpen. Detectie van dreigingen kosten $15/server/maand. Dit is gratis voor Hallo eerste 60 dagen. Zie [Aan de slag met SQL Database Threat Detection](sql-database-threat-detection.md) voor meer informatie.
 
### <a name="data-masking"></a>Gegevensmaskering 
Gevoelige gegevens blootstelling SQL-Database dynamische-gegevensmaskering beperkt door het toonon beheerdersmogelijkheden maskeren. Dynamische-gegevensmaskering automatisch gedetecteerd potentieel gevoelige gegevens in Azure SQL Database en uitvoerbare aanbevelingen toomask van deze velden met minimale gevolgen voor de toepassingslaag Hallo biedt. Hierbij worden obfuscating Hallo gevoelige gegevens in de resultatenset Hallo van een query over aangewezen databasevelden, terwijl het Hallo-gegevens in Hallo-database wordt niet gewijzigd. Voor meer informatie Zie aan de slag met [SQL-Database dynamische gegevens maskeren](sql-database-dynamic-data-masking-get-started.md)
 
## <a name="compliance"></a>Naleving
Bovendien toohello hierboven functies en functionaliteit die kan helpen bij uw toepassing ook voorzien van verschillende beveiligingsvereisten, Azure SQL Database deel uitmaakt van reguliere audits en tegen een aantal nalevingsstandaards is gecertificeerd. Zie voor meer informatie, Hallo [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/), waarbij u de meest recente lijst Hallo van vindt [SQL-Database naleving certificeringen](https://azure.microsoft.com/support/trust-center/services/).

## <a name="next-steps"></a>Volgende stappen

- Zie voor een beschrijving van Hallo gebruik van de access control-functies in SQL-Database [toegangsbeheer](sql-database-control-access.md).
- Zie voor een beschrijving van de Databasecontrole, [SQL Database auditing](sql-database-auditing.md).
- Zie voor een beschrijving van de detectie van dreigingen [SQL-Database de detectie van dreigingen](sql-database-threat-detection.md).
