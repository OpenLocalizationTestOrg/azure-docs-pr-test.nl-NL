---
title: Beveiliging van de Azure SQL Database voor herstel na noodgevallen configureren | Microsoft Docs
description: Dit onderwerp wordt uitgelegd beveiligingsoverwegingen voor het configureren en beheren van de beveiliging na het terugzetten van een database of een failover naar een secundaire server in het geval van een datacentrum of andere noodgeval
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
ms.openlocfilehash: de5e1732dab570b80692efcdd08e4ed2d8c98800
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="a347a-103">Configureren en beheren van Azure SQL Database-beveiliging voor geo-herstel of failover</span><span class="sxs-lookup"><span data-stu-id="a347a-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="a347a-104">[Actieve geo-replicatie](sql-database-geo-replication-overview.md) is nu beschikbaar voor alle databases in alle Servicelagen.</span><span class="sxs-lookup"><span data-stu-id="a347a-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="a347a-105">Overzicht van de verificatievereisten voor herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="a347a-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="a347a-106">Dit onderwerp beschrijft de verificatievereisten voor het configureren en beheren van [actieve geo-replicatie](sql-database-geo-replication-overview.md) en de stappen die nodig zijn voor het instellen van de gebruikerstoegang tot de secundaire database.</span><span class="sxs-lookup"><span data-stu-id="a347a-106">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="a347a-107">Ook wordt beschreven hoe de toegang tot de herstelde database inschakelen na gebruik van [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="a347a-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="a347a-108">Zie voor meer informatie over opties voor Systeemherstel [Business Continuity Overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="a347a-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="a347a-109">Herstel na noodgevallen met ingesloten gebruikers</span><span class="sxs-lookup"><span data-stu-id="a347a-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="a347a-110">In tegenstelling tot traditionele gebruikers dat moeten worden toegewezen aan aanmeldingen in de database master, een contained-gebruiker volledig beheerd door de database zelf.</span><span class="sxs-lookup"><span data-stu-id="a347a-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="a347a-111">Dit heeft twee voordelen.</span><span class="sxs-lookup"><span data-stu-id="a347a-111">This has two benefits.</span></span> <span data-ttu-id="a347a-112">De gebruikers verbinding maken met de nieuwe primaire database kunnen blijven in de noodherstelscenario of de database hersteld met behulp van geo-herstel zonder extra configuratie, omdat de database de gebruikers beheert.</span><span class="sxs-lookup"><span data-stu-id="a347a-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="a347a-113">Er zijn ook potentiële schaalbaarheid en prestatievoordelen van deze configuratie vanuit het oogpunt van de aanmelding van.</span><span class="sxs-lookup"><span data-stu-id="a347a-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="a347a-114">Zie [Ingesloten databasegebruikers: een draagbare database maken](https://msdn.microsoft.com/library/ff929188.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a347a-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="a347a-115">De belangrijkste afweging is dat het proces van het herstel na noodgevallen op grote schaal beheren hoe moeilijker.</span><span class="sxs-lookup"><span data-stu-id="a347a-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="a347a-116">Onderhoud van de referenties met een ingesloten gebruikers in meerdere databases mogelijk wanneer er meerdere databases die gebruikmaken van dezelfde aanmeldingsnaam, de voordelen van het ingesloten gebruikers uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="a347a-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span></span> <span data-ttu-id="a347a-117">Bijvoorbeeld, het wachtwoordbeleid rotatie vereist wijzigingen consistent worden aangebracht in meerdere databases in plaats van het wijzigen van het wachtwoord voor de aanmelding eenmaal in de database master.</span><span class="sxs-lookup"><span data-stu-id="a347a-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="a347a-118">Om deze reden als er meerdere databases die gebruikmaken van dezelfde gebruikersnaam en wachtwoord, wordt met behulp van de ingesloten gebruikers niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="a347a-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="a347a-119">Het configureren van aanmeldingen en gebruikers</span><span class="sxs-lookup"><span data-stu-id="a347a-119">How to configure logins and users</span></span>
<span data-ttu-id="a347a-120">Als u aanmeldingen en gebruikers (in plaats van ingesloten gebruikers), moet u extra stappen om ervoor te zorgen dat de dezelfde aanmeldingen bestaan in de database master uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a347a-120">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="a347a-121">De volgende secties worden de stappen die betrokken zijn en aanvullende overwegingen.</span><span class="sxs-lookup"><span data-stu-id="a347a-121">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="a347a-122">Gebruikerstoegang tot een secundaire of door de herstelde database instellen</span><span class="sxs-lookup"><span data-stu-id="a347a-122">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="a347a-123">In de volgorde voor de secundaire database om te worden gebruikt als een secundaire database alleen-lezen en om te controleren of de juiste toegang heeft tot de nieuwe primaire database of de database herstellen met geo-herstel de hoofddatabase van de doelserver moet beschikken over de juiste beveiligingsconfiguratie voordat het herstel.</span><span class="sxs-lookup"><span data-stu-id="a347a-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="a347a-124">De specifieke machtigingen voor elke stap worden verderop in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="a347a-124">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="a347a-125">Voorbereiden van de gebruikerstoegang tot een secundaire geo-replicatie moet worden uitgevoerd als onderdeel geo-replicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="a347a-125">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="a347a-126">Voorbereiden van de gebruikerstoegang tot de databases geo hersteld moet worden uitgevoerd op elk gewenst moment wanneer de oorspronkelijke server online is (bijvoorbeeld als onderdeel van de details voor Dr).</span><span class="sxs-lookup"><span data-stu-id="a347a-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="a347a-127">Als u een failover of geo-herstel naar een server waarop geen correct geconfigureerde aanmeldingen, toegang tot deze beperkt tot de server admin-account zijn.</span><span class="sxs-lookup"><span data-stu-id="a347a-127">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="a347a-128">Instellen van aanmeldingen op de doelserver omvat drie stappen die hieronder worden beschreven:</span><span class="sxs-lookup"><span data-stu-id="a347a-128">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="a347a-129">1. Aanmeldingen met toegang tot de primaire database bepalen:</span><span class="sxs-lookup"><span data-stu-id="a347a-129">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="a347a-130">De eerste stap van het proces is om te bepalen welke aanmeldingen op de doelserver moeten worden gedupliceerd.</span><span class="sxs-lookup"><span data-stu-id="a347a-130">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="a347a-131">Dit wordt bereikt met een SELECT-instructies, één in de logische hoofddatabase op de bronserver en één in de primaire database zelf.</span><span class="sxs-lookup"><span data-stu-id="a347a-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="a347a-132">Alleen de serverbeheerder of een lid van de **LoginManager** serverfunctie kunt bepalen de aanmeldingen op de bronserver met de volgende SELECT-instructie.</span><span class="sxs-lookup"><span data-stu-id="a347a-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="a347a-133">Alleen een lid van de databaserol db_owner, de gebruiker dbo of serverbeheerder kan bepalen dat alle van de database gebruiker principals in de primaire database.</span><span class="sxs-lookup"><span data-stu-id="a347a-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="a347a-134">2. De beveiligings-id niet vinden voor de aanmeldingen geïdentificeerd in stap 1:</span><span class="sxs-lookup"><span data-stu-id="a347a-134">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="a347a-135">Door het vergelijken van de uitvoer van de query's uit de vorige sectie en die overeenkomt met de SID's, kunt u de server-aanmelding toewijzen aan databasegebruiker.</span><span class="sxs-lookup"><span data-stu-id="a347a-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="a347a-136">Aanmeldingen die een databasegebruiker met een overeenkomende SID hebben gebruikerstoegang hebben tot die database als die databasegebruiker principal.</span><span class="sxs-lookup"><span data-stu-id="a347a-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="a347a-137">De volgende query kan worden gebruikt om alle van de gebruiker principals en hun SID's in een database te zien.</span><span class="sxs-lookup"><span data-stu-id="a347a-137">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="a347a-138">Alleen een lid van de functie of servergroep-beheerder voor de database voor db_owner deze query uitvoeren kan.</span><span class="sxs-lookup"><span data-stu-id="a347a-138">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="a347a-139">De **INFORMATION_SCHEMA** en **sys** gebruikers hebben *NULL* SID's, en de **Gast** SID is **0x00**.</span><span class="sxs-lookup"><span data-stu-id="a347a-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="a347a-140">De **dbo** SID mogen beginnen met *0x01060000000001648000000000048454*als maker van de database is de serverbeheerder in plaats van een lid van **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="a347a-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="a347a-141">3. Maak de aanmeldingen op de doelserver:</span><span class="sxs-lookup"><span data-stu-id="a347a-141">3. Create the logins on the target server:</span></span>
<span data-ttu-id="a347a-142">Er is de laatste stap gaat u naar de doelserver of servers en de aanmeldingen met de juiste beveiligings-id's genereren.</span><span class="sxs-lookup"><span data-stu-id="a347a-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="a347a-143">De basis-syntaxis is als volgt.</span><span class="sxs-lookup"><span data-stu-id="a347a-143">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="a347a-144">Als u wilt dat gebruikerstoegang verlenen tot de secundaire, maar niet naar de primaire, u dat doen kunt door het wijzigen van de gebruikersaanmelding op de primaire server met behulp van de volgende syntaxis.</span><span class="sxs-lookup"><span data-stu-id="a347a-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="a347a-145">ALTER LOGIN <login name> UITSCHAKELEN</span><span class="sxs-lookup"><span data-stu-id="a347a-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="a347a-146">UITSCHAKELEN wordt niet het wachtwoord wijzigen zodat u deze altijd inschakelen kunt indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a347a-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a347a-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a347a-147">Next steps</span></span>
* <span data-ttu-id="a347a-148">Zie voor meer informatie over het beheren van toegang tot de database en aanmeldingen [SQL Database-beveiliging: beveiliging van toegang en meld u aan de database beheren](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="a347a-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="a347a-149">Zie voor meer informatie over ingesloten databasegebruikers [opgenomen databasegebruikers: maken van uw Database draagbare](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="a347a-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="a347a-150">Zie voor meer informatie over het gebruik en actieve geo-replicatie configureren [actieve geo-replicatie](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a347a-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="a347a-151">Zie voor meer informatie over het gebruik van geo-restore [geo-herstel](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="a347a-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

