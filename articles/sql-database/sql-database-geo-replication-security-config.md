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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="720b9-103">Configureren en beheren van Azure SQL Database-beveiliging voor geo-herstel of failover</span><span class="sxs-lookup"><span data-stu-id="720b9-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="720b9-104">[Actieve geo-replicatie](sql-database-geo-replication-overview.md) is nu beschikbaar voor alle databases in alle Servicelagen.</span><span class="sxs-lookup"><span data-stu-id="720b9-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="720b9-105">Overzicht van de verificatievereisten voor herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="720b9-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="720b9-106">Dit onderwerp wordt beschreven Hallo verificatie vereisten tooconfigure en beheer [actieve geo-replicatie](sql-database-geo-replication-overview.md) en Hallo stappen vereist tooset van gebruiker toegang toohello secundaire database.</span><span class="sxs-lookup"><span data-stu-id="720b9-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="720b9-107">Ook wordt beschreven hoe toegang toohello herstelde database inschakelen na gebruik van [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="720b9-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="720b9-108">Zie voor meer informatie over opties voor Systeemherstel [Business Continuity Overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="720b9-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="720b9-109">Herstel na noodgevallen met ingesloten gebruikers</span><span class="sxs-lookup"><span data-stu-id="720b9-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="720b9-110">In tegenstelling tot traditionele gebruikers toologins in de hoofddatabase Hallo die moet worden toegewezen, een contained-gebruiker volledig wordt beheerd door Hallo-database zelf.</span><span class="sxs-lookup"><span data-stu-id="720b9-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="720b9-111">Dit heeft twee voordelen.</span><span class="sxs-lookup"><span data-stu-id="720b9-111">This has two benefits.</span></span> <span data-ttu-id="720b9-112">In Hallo noodherstelscenario blijven gebruikers Hallo tooconnect toohello nieuwe primaire database of Hallo-database herstellen met geo-herstel zonder extra configuratie, omdat database Hallo Hallo gebruikers beheert.</span><span class="sxs-lookup"><span data-stu-id="720b9-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="720b9-113">Er zijn ook potentiële schaalbaarheid en prestatievoordelen van deze configuratie vanuit het oogpunt van de aanmelding van.</span><span class="sxs-lookup"><span data-stu-id="720b9-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="720b9-114">Zie [Ingesloten databasegebruikers: een draagbare database maken](https://msdn.microsoft.com/library/ff929188.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="720b9-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="720b9-115">Hallo belangrijkste afweging is dat beheren Hallo noodherstelproces op grote schaal meer lastig.</span><span class="sxs-lookup"><span data-stu-id="720b9-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="720b9-116">Wanneer u meerdere databases die gebruik Hallo dezelfde aanmelding hebt, onderhouden Hallo-referenties met een opgenomen kunnen gebruikers in meerdere databases Hallo voordelen van het ingesloten gebruikers uitsluiten.</span><span class="sxs-lookup"><span data-stu-id="720b9-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="720b9-117">Hallo-wachtwoordbeleid rotatie vereist bijvoorbeeld dat wijzigingen worden aangebracht consistent in meerdere databases in plaats van veranderende Hallo wachtwoord voor aanmelding Hallo eenmaal in de hoofddatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="720b9-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="720b9-118">Om deze reden, als u meerdere databases die Hallo gebruik hebt dezelfde gebruikersnaam en het wachtwoord met behulp van de ingesloten gebruikers wordt niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="720b9-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="720b9-119">Hoe tooconfigure aanmeldingen en gebruikers</span><span class="sxs-lookup"><span data-stu-id="720b9-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="720b9-120">Als u aanmeldingen en gebruikers (in plaats van ingesloten gebruikers), moet u rekening houden tooinsure extra stappen die Hallo dezelfde aanmeldingen bestaan in de hoofddatabase Hallo.</span><span class="sxs-lookup"><span data-stu-id="720b9-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="720b9-121">Hallo volgende secties worden Hallo stappen die betrokken zijn en aanvullende overwegingen.</span><span class="sxs-lookup"><span data-stu-id="720b9-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="720b9-122">Gebruiker toegang tooa secundaire of door de herstelde database instellen</span><span class="sxs-lookup"><span data-stu-id="720b9-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="720b9-123">Hallo secundaire database toobe kan worden gebruikt als een alleen-lezen secundaire database en tooensure toegangsmachtigingen toohello nieuwe primaire database of Hallo-database herstellen met geo-restore master Hallo moet database van de doelserver Hallo hebben Hallo juiste beveiligingsconfiguratie aanwezig zijn vóór het Hallo-herstel.</span><span class="sxs-lookup"><span data-stu-id="720b9-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="720b9-124">Hallo specifieke machtigingen voor elke stap worden verderop in dit onderwerp beschreven.</span><span class="sxs-lookup"><span data-stu-id="720b9-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="720b9-125">Voorbereiden van de gebruiker toegang tooa moet secundaire geo-replicatie worden uitgevoerd als onderdeel geo-replicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="720b9-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="720b9-126">Voorbereiden van gebruikerstoegang toohello geo hersteld databases moet worden uitgevoerd op elk gewenst moment wanneer de oorspronkelijke server Hallo online is (bijvoorbeeld als onderdeel van Hallo DR-herstelanalyse).</span><span class="sxs-lookup"><span data-stu-id="720b9-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="720b9-127">Als u niet over of geo-restore tooa-server die geen correct geconfigureerde aanmeldingen toegang tooit worden beperkt toohello server-beheerdersaccount.</span><span class="sxs-lookup"><span data-stu-id="720b9-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="720b9-128">Instellen van aanmeldingen op de doelserver Hallo omvat drie stappen die hieronder worden beschreven:</span><span class="sxs-lookup"><span data-stu-id="720b9-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="720b9-129">1. Aanmeldingen met toegang toohello primaire database bepalen:</span><span class="sxs-lookup"><span data-stu-id="720b9-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="720b9-130">eerste stap van Hallo Hallo is toodetermine welke aanmeldingen op Hallo-doelserver moeten worden gedupliceerd.</span><span class="sxs-lookup"><span data-stu-id="720b9-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="720b9-131">Dit wordt bereikt met een SELECT-instructies, één in Hallo logische hoofddatabase op de bronserver Hallo en één in Hallo primaire database zelf.</span><span class="sxs-lookup"><span data-stu-id="720b9-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="720b9-132">Alleen Hallo serverbeheerder of een lid van Hallo **LoginManager** serverfunctie Hallo aanmeldingen op de bronserver Hallo kunt bepalen Hello SELECT-instructie te volgen.</span><span class="sxs-lookup"><span data-stu-id="720b9-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="720b9-133">Alleen een lid van de databaserol db_owner hello, Hallo dbo gebruiker of -serverbeheerder kan bepalen dat alle Hallo database gebruiker principals in Hallo primaire database.</span><span class="sxs-lookup"><span data-stu-id="720b9-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="720b9-134">2. Hallo beveiligings-id niet vinden voor Hallo aanmeldingen geïdentificeerd in stap 1:</span><span class="sxs-lookup"><span data-stu-id="720b9-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="720b9-135">Door het Hallo-uitvoer van Hallo query's van de vorige sectie Hallo en overeenkomende Hallo SID's te vergelijken, kunt u Hallo server aanmeldingsgebruiker toodatabase toewijzen.</span><span class="sxs-lookup"><span data-stu-id="720b9-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="720b9-136">Gebruiker toegang toothat database hebben aanmeldingen die een databasegebruiker met een overeenkomende beveiligings-id hebben als die databasegebruiker principal.</span><span class="sxs-lookup"><span data-stu-id="720b9-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="720b9-137">Hallo volgende query kan worden gebruikt toosee alle Hallo gebruiker principals en hun SID's in een database.</span><span class="sxs-lookup"><span data-stu-id="720b9-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="720b9-138">Alleen een lid van Hallo db_owner database functie of servergroep beheerder kunt u deze query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="720b9-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="720b9-139">Hallo **INFORMATION_SCHEMA** en **sys** gebruikers hebben *NULL* beveiligings-id's en Hallo **Gast** SID is **0x00**.</span><span class="sxs-lookup"><span data-stu-id="720b9-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="720b9-140">Hallo **dbo** SID mogen beginnen met *0x01060000000001648000000000048454*als Hallo database maken is Hallo-Serverbeheer in plaats van een lid van **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="720b9-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="720b9-141">3. Hallo-aanmeldingen maken op de doelserver Hallo:</span><span class="sxs-lookup"><span data-stu-id="720b9-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="720b9-142">Hallo laatste stap toogo toohello target server of servers en genereren Hallo aanmeldingen Hello SID's van toepassing.</span><span class="sxs-lookup"><span data-stu-id="720b9-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="720b9-143">Hallo basic syntaxis is als volgt.</span><span class="sxs-lookup"><span data-stu-id="720b9-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="720b9-144">Als u toogrant gebruiker toegang toohello secundaire, maar niet toohello primaire wilt, kunt u dat doen door Hallo gebruikersaanmelding op de primaire server Hallo wijzigen met behulp van de volgende syntaxis Hallo.</span><span class="sxs-lookup"><span data-stu-id="720b9-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="720b9-145">ALTER LOGIN <login name> UITSCHAKELEN</span><span class="sxs-lookup"><span data-stu-id="720b9-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="720b9-146">SCHAKEL niet Hallo wachtwoord wijzigt, zodat u deze altijd inschakelen kunt indien nodig.</span><span class="sxs-lookup"><span data-stu-id="720b9-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="720b9-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="720b9-147">Next steps</span></span>
* <span data-ttu-id="720b9-148">Zie voor meer informatie over het beheren van toegang tot de database en aanmeldingen [SQL Database-beveiliging: beveiliging van toegang en meld u aan de database beheren](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="720b9-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="720b9-149">Zie voor meer informatie over ingesloten databasegebruikers [opgenomen databasegebruikers: maken van uw Database draagbare](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="720b9-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="720b9-150">Zie voor meer informatie over het gebruik en actieve geo-replicatie configureren [actieve geo-replicatie](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="720b9-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="720b9-151">Zie voor meer informatie over het gebruik van geo-restore [geo-herstel](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="720b9-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

