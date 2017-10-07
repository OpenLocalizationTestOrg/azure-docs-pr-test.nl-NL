---
title: beveiliging van de Azure SQL Database voor herstel na noodgevallen aaaConfigure | Microsoft Docs
description: Dit onderwerp wordt uitgelegd beveiligingsoverwegingen voor het configureren en beheren van de beveiliging na het terugzetten van een database of een failover-tooa secundaire server in geval van een datacentrum of andere calamiteit Hallo
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Configureren en beheren van Azure SQL Database-beveiliging voor geo-herstel of failover 

> [!NOTE]
> [Actieve geo-replicatie](sql-database-geo-replication-overview.md) is nu beschikbaar voor alle databases in alle Servicelagen.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Overzicht van de verificatievereisten voor herstel na noodgevallen
Dit onderwerp wordt beschreven Hallo verificatie vereisten tooconfigure en beheer [actieve geo-replicatie](sql-database-geo-replication-overview.md) en Hallo stappen vereist tooset van gebruiker toegang toohello secundaire database. Ook wordt beschreven hoe toegang toohello herstelde database inschakelen na gebruik van [geo-restore](sql-database-recovery-using-backups.md#geo-restore). Zie voor meer informatie over opties voor Systeemherstel [Business Continuity Overview](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Herstel na noodgevallen met ingesloten gebruikers
In tegenstelling tot traditionele gebruikers toologins in de hoofddatabase Hallo die moet worden toegewezen, een contained-gebruiker volledig wordt beheerd door Hallo-database zelf. Dit heeft twee voordelen. In Hallo noodherstelscenario blijven gebruikers Hallo tooconnect toohello nieuwe primaire database of Hallo-database herstellen met geo-herstel zonder extra configuratie, omdat database Hallo Hallo gebruikers beheert. Er zijn ook potentiële schaalbaarheid en prestatievoordelen van deze configuratie vanuit het oogpunt van de aanmelding van. Zie [Ingesloten databasegebruikers: een draagbare database maken](https://msdn.microsoft.com/library/ff929188.aspx) voor meer informatie. 

Hallo belangrijkste afweging is dat beheren Hallo noodherstelproces op grote schaal meer lastig. Wanneer u meerdere databases die gebruik Hallo dezelfde aanmelding hebt, onderhouden Hallo-referenties met een opgenomen kunnen gebruikers in meerdere databases Hallo voordelen van het ingesloten gebruikers uitsluiten. Hallo-wachtwoordbeleid rotatie vereist bijvoorbeeld dat wijzigingen worden aangebracht consistent in meerdere databases in plaats van veranderende Hallo wachtwoord voor aanmelding Hallo eenmaal in de hoofddatabase Hallo. Om deze reden, als u meerdere databases die Hallo gebruik hebt dezelfde gebruikersnaam en het wachtwoord met behulp van de ingesloten gebruikers wordt niet aanbevolen. 

## <a name="how-tooconfigure-logins-and-users"></a>Hoe tooconfigure aanmeldingen en gebruikers
Als u aanmeldingen en gebruikers (in plaats van ingesloten gebruikers), moet u rekening houden tooinsure extra stappen die Hallo dezelfde aanmeldingen bestaan in de hoofddatabase Hallo. Hallo volgende secties worden Hallo stappen die betrokken zijn en aanvullende overwegingen.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Gebruiker toegang tooa secundaire of door de herstelde database instellen
Hallo secundaire database toobe kan worden gebruikt als een alleen-lezen secundaire database en tooensure toegangsmachtigingen toohello nieuwe primaire database of Hallo-database herstellen met geo-restore master Hallo moet database van de doelserver Hallo hebben Hallo juiste beveiligingsconfiguratie aanwezig zijn vóór het Hallo-herstel.

Hallo specifieke machtigingen voor elke stap worden verderop in dit onderwerp beschreven.

Voorbereiden van de gebruiker toegang tooa moet secundaire geo-replicatie worden uitgevoerd als onderdeel geo-replicatie configureren. Voorbereiden van gebruikerstoegang toohello geo hersteld databases moet worden uitgevoerd op elk gewenst moment wanneer de oorspronkelijke server Hallo online is (bijvoorbeeld als onderdeel van Hallo DR-herstelanalyse).

> [!NOTE]
> Als u niet over of geo-restore tooa-server die geen correct geconfigureerde aanmeldingen toegang tooit worden beperkt toohello server-beheerdersaccount.
> 
> 

Instellen van aanmeldingen op de doelserver Hallo omvat drie stappen die hieronder worden beschreven:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Aanmeldingen met toegang toohello primaire database bepalen:
eerste stap van Hallo Hallo is toodetermine welke aanmeldingen op Hallo-doelserver moeten worden gedupliceerd. Dit wordt bereikt met een SELECT-instructies, één in Hallo logische hoofddatabase op de bronserver Hallo en één in Hallo primaire database zelf.

Alleen Hallo serverbeheerder of een lid van Hallo **LoginManager** serverfunctie Hallo aanmeldingen op de bronserver Hallo kunt bepalen Hello SELECT-instructie te volgen. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Alleen een lid van de databaserol db_owner hello, Hallo dbo gebruiker of -serverbeheerder kan bepalen dat alle Hallo database gebruiker principals in Hallo primaire database.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Hallo beveiligings-id niet vinden voor Hallo aanmeldingen geïdentificeerd in stap 1:
Door het Hallo-uitvoer van Hallo query's van de vorige sectie Hallo en overeenkomende Hallo SID's te vergelijken, kunt u Hallo server aanmeldingsgebruiker toodatabase toewijzen. Gebruiker toegang toothat database hebben aanmeldingen die een databasegebruiker met een overeenkomende beveiligings-id hebben als die databasegebruiker principal. 

Hallo volgende query kan worden gebruikt toosee alle Hallo gebruiker principals en hun SID's in een database. Alleen een lid van Hallo db_owner database functie of servergroep beheerder kunt u deze query uitvoeren.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Hallo **INFORMATION_SCHEMA** en **sys** gebruikers hebben *NULL* beveiligings-id's en Hallo **Gast** SID is **0x00**. Hallo **dbo** SID mogen beginnen met *0x01060000000001648000000000048454*als Hallo database maken is Hallo-Serverbeheer in plaats van een lid van **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Hallo-aanmeldingen maken op de doelserver Hallo:
Hallo laatste stap toogo toohello target server of servers en genereren Hallo aanmeldingen Hello SID's van toepassing. Hallo basic syntaxis is als volgt.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Als u toogrant gebruiker toegang toohello secundaire, maar niet toohello primaire wilt, kunt u dat doen door Hallo gebruikersaanmelding op de primaire server Hallo wijzigen met behulp van de volgende syntaxis Hallo.
> 
> ALTER LOGIN <login name> UITSCHAKELEN
> 
> SCHAKEL niet Hallo wachtwoord wijzigt, zodat u deze altijd inschakelen kunt indien nodig.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het beheren van toegang tot de database en aanmeldingen [SQL Database-beveiliging: beveiliging van toegang en meld u aan de database beheren](sql-database-manage-logins.md).
* Zie voor meer informatie over ingesloten databasegebruikers [opgenomen databasegebruikers: maken van uw Database draagbare](https://msdn.microsoft.com/library/ff929188.aspx).
* Zie voor meer informatie over het gebruik en actieve geo-replicatie configureren [actieve geo-replicatie](sql-database-geo-replication-overview.md)
* Zie voor meer informatie over het gebruik van geo-restore [geo-herstel](sql-database-recovery-using-backups.md#geo-restore)

