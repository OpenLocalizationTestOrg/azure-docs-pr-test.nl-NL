---
title: aaaExtended gebeurtenissen in SQL-Database | Microsoft Docs
description: Beschrijft uitgebreide gebeurtenissen (XEvents) in Azure SQL Database en hoe gebeurtenissessies kunnen enigszins verschillen van de event-sessies in Microsoft SQL Server.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 3b28cf15-f820-4b3c-8310-908d6d5b9d0c
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 8c966a84412aa561c92b16e5c6902102483eb1bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extended-events-in-sql-database"></a><span data-ttu-id="3f940-103">Uitgebreide gebeurtenissen in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="3f940-103">Extended events in SQL Database</span></span>
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="3f940-104">Dit onderwerp wordt uitgelegd hoe Hallo-implementatie van uitgebreide gebeurtenissen in Azure SQL Database iets anders dan tooextended gebeurtenissen in Microsoft SQL Server is.</span><span class="sxs-lookup"><span data-stu-id="3f940-104">This topic explains how hello implementation of extended events in Azure SQL Database is slightly different compared tooextended events in Microsoft SQL Server.</span></span>

- <span data-ttu-id="3f940-105">SQL Database V12 die is opgedaan Hallo uitgebreide gebeurtenissen functie in Hallo tweede helft van de kalender 2015.</span><span class="sxs-lookup"><span data-stu-id="3f940-105">SQL Database V12 gained hello extended events feature in hello second half of calendar 2015.</span></span>
- <span data-ttu-id="3f940-106">SQL Server heeft uitgebreide gebeurtenissen sinds 2008.</span><span class="sxs-lookup"><span data-stu-id="3f940-106">SQL Server has had extended events since 2008.</span></span>
- <span data-ttu-id="3f940-107">Hallo-functieset van uitgebreide gebeurtenissen op de SQL-Database is een robuuste subset van Hallo-functies op SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f940-107">hello feature set of extended events on SQL Database is a robust subset of hello features on SQL Server.</span></span>

<span data-ttu-id="3f940-108">*XEvents* is een informele bijnaam die soms wordt gebruikt voor 'uitgebreide gebeurtenissen' in blogs en andere informele locaties.</span><span class="sxs-lookup"><span data-stu-id="3f940-108">*XEvents* is an informal nickname that is sometimes used for 'extended events' in blogs and other informal locations.</span></span>

<span data-ttu-id="3f940-109">Meer informatie over uitgebreide gebeurtenissen voor Azure SQL Database en Microsoft SQL Server, is beschikbaar op:</span><span class="sxs-lookup"><span data-stu-id="3f940-109">Additional information about extended events, for Azure SQL Database and Microsoft SQL Server, is available at:</span></span>

- [<span data-ttu-id="3f940-110">Snelstartgids: Uitgebreide gebeurtenissen in SQL Server</span><span class="sxs-lookup"><span data-stu-id="3f940-110">Quick Start: Extended events in SQL Server</span></span>](http://msdn.microsoft.com/library/mt733217.aspx)
- [<span data-ttu-id="3f940-111">Uitgebreide gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="3f940-111">Extended Events</span></span>](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a><span data-ttu-id="3f940-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3f940-112">Prerequisites</span></span>

<span data-ttu-id="3f940-113">In dit onderwerp wordt ervan uitgegaan dat u al enige kennis hebt van:</span><span class="sxs-lookup"><span data-stu-id="3f940-113">This topic assumes you already have some knowledge of:</span></span>

- <span data-ttu-id="3f940-114">[Azure SQL Database-service](https://azure.microsoft.com/services/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="3f940-114">[Azure SQL Database service](https://azure.microsoft.com/services/sql-database/).</span></span>
- <span data-ttu-id="3f940-115">[Uitgebreide gebeurtenissen](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="3f940-115">[Extended events](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.</span></span>

- <span data-ttu-id="3f940-116">Hallo bulksgewijs van onze documentatie over uitgebreide gebeurtenissen geldt tooboth SQL Server en SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="3f940-116">hello bulk of our documentation about extended events applies tooboth SQL Server and SQL Database.</span></span>

<span data-ttu-id="3f940-117">Eerdere blootstelling toohello volgende items is handig bij het kiezen van de gebeurtenisbestand als Hallo Hallo [doel](#AzureXEventsTargets):</span><span class="sxs-lookup"><span data-stu-id="3f940-117">Prior exposure toohello following items is helpful when choosing hello Event File as hello [target](#AzureXEventsTargets):</span></span>

- [<span data-ttu-id="3f940-118">Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="3f940-118">Azure Storage service</span></span>](https://azure.microsoft.com/services/storage/)


- <span data-ttu-id="3f940-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f940-119">PowerShell</span></span>
    - <span data-ttu-id="3f940-120">[Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) -bevat uitgebreide informatie over PowerShell en hello Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="3f940-120">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>

## <a name="code-samples"></a><span data-ttu-id="3f940-121">Codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="3f940-121">Code samples</span></span>

<span data-ttu-id="3f940-122">Verwante onderwerpen bieden twee codevoorbeelden:</span><span class="sxs-lookup"><span data-stu-id="3f940-122">Related topics provide two code samples:</span></span>


- [<span data-ttu-id="3f940-123">Ring Buffer doel code voor uitgebreide gebeurtenissen in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="3f940-123">Ring Buffer target code for extended events in SQL Database</span></span>](sql-database-xevent-code-ring-buffer.md)
    - <span data-ttu-id="3f940-124">Korte eenvoudig Transact-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="3f940-124">Short simple Transact-SQL script.</span></span>
    - <span data-ttu-id="3f940-125">We benadrukken in Hallo code voorbeeldonderwerp dat, wanneer u klaar bent met een doel ringbuffer, u de bronnen vrijgeven moet door het uitvoeren van een alter neerzetten `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instructie.</span><span class="sxs-lookup"><span data-stu-id="3f940-125">We emphasize in hello code sample topic that, when you are done with a Ring Buffer target, you should release its resources by executing an alter-drop `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` statement.</span></span> <span data-ttu-id="3f940-126">Later kunt u een ander exemplaar van ringbuffer door toevoegen `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span><span class="sxs-lookup"><span data-stu-id="3f940-126">Later you can add another instance of Ring Buffer by `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.</span></span>


- [<span data-ttu-id="3f940-127">Bestand doel gebeurteniscode voor uitgebreide gebeurtenissen in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="3f940-127">Event File target code for extended events in SQL Database</span></span>](sql-database-xevent-code-event-file.md)
    - <span data-ttu-id="3f940-128">Fase 1 is PowerShell toocreate een Azure Storage-container.</span><span class="sxs-lookup"><span data-stu-id="3f940-128">Phase 1 is PowerShell toocreate an Azure Storage container.</span></span>
    - <span data-ttu-id="3f940-129">Fase 2 is Transact-SQL die gebruikmaakt van hello Azure Storage-container.</span><span class="sxs-lookup"><span data-stu-id="3f940-129">Phase 2 is Transact-SQL that uses hello Azure Storage container.</span></span>

## <a name="transact-sql-differences"></a><span data-ttu-id="3f940-130">Verschillen Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="3f940-130">Transact-SQL differences</span></span>


- <span data-ttu-id="3f940-131">Bij het uitvoeren van Hallo [maken GEBEURTENIS sessie](http://msdn.microsoft.com/library/bb677289.aspx) opdracht op SQL Server u Hallo gebruikt **ON SERVER** component.</span><span class="sxs-lookup"><span data-stu-id="3f940-131">When you execute hello [CREATE EVENT SESSION](http://msdn.microsoft.com/library/bb677289.aspx) command on SQL Server, you use hello **ON SERVER** clause.</span></span> <span data-ttu-id="3f940-132">Maar op de SQL-Database gebruikt u Hallo **ON DATABASE** component in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="3f940-132">But on SQL Database you use hello **ON DATABASE** clause instead.</span></span>


- <span data-ttu-id="3f940-133">Hallo **ON DATABASE** component is ook van toepassing toohello [ALTER GEBEURTENIS sessie](http://msdn.microsoft.com/library/bb630368.aspx) en [DROP GEBEURTENIS sessie](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="3f940-133">hello **ON DATABASE** clause also applies toohello [ALTER EVENT SESSION](http://msdn.microsoft.com/library/bb630368.aspx) and [DROP EVENT SESSION](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL commands.</span></span>


- <span data-ttu-id="3f940-134">Is een best practice tooinclude Hallo gebeurtenis sessieoptie van **STARTUP_STATE = ON** in uw **maken GEBEURTENIS sessie** of **ALTER GEBEURTENIS sessie** instructies.</span><span class="sxs-lookup"><span data-stu-id="3f940-134">A best practice is tooinclude hello event session option of **STARTUP_STATE = ON** in your **CREATE EVENT SESSION**  or **ALTER EVENT SESSION** statements.</span></span>
    - <span data-ttu-id="3f940-135">Hallo **= ON** waarde ondersteunt automatisch opnieuw opstarten na een herconfiguratie van logische Hallo-database vanwege tooa failover.</span><span class="sxs-lookup"><span data-stu-id="3f940-135">hello **= ON** value supports an automatic restart after a reconfiguration of hello logical database due tooa failover.</span></span>

## <a name="new-catalog-views"></a><span data-ttu-id="3f940-136">Nieuwe catalogusweergaven</span><span class="sxs-lookup"><span data-stu-id="3f940-136">New catalog views</span></span>

<span data-ttu-id="3f940-137">Hallo uitgebreide gebeurtenissen functie wordt ondersteund door verschillende [catalogus weergaven](http://msdn.microsoft.com/library/ms174365.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f940-137">hello extended events feature is supported by several [catalog views](http://msdn.microsoft.com/library/ms174365.aspx).</span></span> <span data-ttu-id="3f940-138">Catalogusweergaven vertellen u *metagegevens of definities* van gebeurtenissessies in de huidige database Hallo gebruiker gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f940-138">Catalog views tell you about *metadata or definitions* of user-created event sessions in hello current database.</span></span> <span data-ttu-id="3f940-139">Hallo weergaven retourneren informatie over exemplaren van actieve gebeurtenissessies kunnen niet.</span><span class="sxs-lookup"><span data-stu-id="3f940-139">hello views do not return information about instances of active event sessions.</span></span>

| <span data-ttu-id="3f940-140">Naam van</span><span class="sxs-lookup"><span data-stu-id="3f940-140">Name of</span></span><br/><span data-ttu-id="3f940-141">catalogusweergave</span><span class="sxs-lookup"><span data-stu-id="3f940-141">catalog view</span></span> | <span data-ttu-id="3f940-142">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3f940-142">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3f940-143">**sys.database_event_session_actions**</span><span class="sxs-lookup"><span data-stu-id="3f940-143">**sys.database_event_session_actions**</span></span> |<span data-ttu-id="3f940-144">Retourneert een rij voor elke actie op elke gebeurtenis van de gebeurtenissessie van een.</span><span class="sxs-lookup"><span data-stu-id="3f940-144">Returns a row for each action on each event of an event session.</span></span> |
| <span data-ttu-id="3f940-145">**sys.database_event_session_events**</span><span class="sxs-lookup"><span data-stu-id="3f940-145">**sys.database_event_session_events**</span></span> |<span data-ttu-id="3f940-146">Retourneert een rij voor elke gebeurtenis in een event-sessie.</span><span class="sxs-lookup"><span data-stu-id="3f940-146">Returns a row for each event in an event session.</span></span> |
| <span data-ttu-id="3f940-147">**sys.database_event_session_fields**</span><span class="sxs-lookup"><span data-stu-id="3f940-147">**sys.database_event_session_fields**</span></span> |<span data-ttu-id="3f940-148">Retourneert een rij voor elke aanpassen kunnen kolom die expliciet is ingesteld op gebeurtenissen en doelen.</span><span class="sxs-lookup"><span data-stu-id="3f940-148">Returns a row for each customize-able column that was explicitly set on events and targets.</span></span> |
| <span data-ttu-id="3f940-149">**sys.database_event_session_targets**</span><span class="sxs-lookup"><span data-stu-id="3f940-149">**sys.database_event_session_targets**</span></span> |<span data-ttu-id="3f940-150">Retourneert een rij voor elk gebeurtenisdoel voor een event-sessie.</span><span class="sxs-lookup"><span data-stu-id="3f940-150">Returns a row for each event target for an event session.</span></span> |
| <span data-ttu-id="3f940-151">**sys.database_event_sessions**</span><span class="sxs-lookup"><span data-stu-id="3f940-151">**sys.database_event_sessions**</span></span> |<span data-ttu-id="3f940-152">Retourneert een rij voor elke gebeurtenissessie in Hallo SQL Database-database.</span><span class="sxs-lookup"><span data-stu-id="3f940-152">Returns a row for each event session in hello SQL Database database.</span></span> |

<span data-ttu-id="3f940-153">In Microsoft SQL Server, vergelijkbare catalogusweergaven hebben namen die zijn *.server\_*  in plaats van *.database\_*.</span><span class="sxs-lookup"><span data-stu-id="3f940-153">In Microsoft SQL Server, similar catalog views have names that include *.server\_* instead of *.database\_*.</span></span> <span data-ttu-id="3f940-154">Hallo naampatroon is vergelijkbaar met **sys.server_event_%**.</span><span class="sxs-lookup"><span data-stu-id="3f940-154">hello name pattern is like **sys.server_event_%**.</span></span>

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a><span data-ttu-id="3f940-155">Nieuwe dynamische beheerweergaven [(DMV's)](http://msdn.microsoft.com/library/ms188754.aspx)</span><span class="sxs-lookup"><span data-stu-id="3f940-155">New dynamic management views [(DMVs)](http://msdn.microsoft.com/library/ms188754.aspx)</span></span>

<span data-ttu-id="3f940-156">Azure SQL-Database heeft [dynamische beheerweergaven (DMV's)](http://msdn.microsoft.com/library/bb677293.aspx) die ondersteuning bieden voor uitgebreide gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3f940-156">Azure SQL Database has [dynamic management views (DMVs)](http://msdn.microsoft.com/library/bb677293.aspx) that support extended events.</span></span> <span data-ttu-id="3f940-157">DMV's informatie over de *active* event-sessies.</span><span class="sxs-lookup"><span data-stu-id="3f940-157">DMVs tell you about *active* event sessions.</span></span>

| <span data-ttu-id="3f940-158">Naam van de DMV</span><span class="sxs-lookup"><span data-stu-id="3f940-158">Name of DMV</span></span> | <span data-ttu-id="3f940-159">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3f940-159">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3f940-160">**sys.dm_xe_database_session_event_actions**</span><span class="sxs-lookup"><span data-stu-id="3f940-160">**sys.dm_xe_database_session_event_actions**</span></span> |<span data-ttu-id="3f940-161">Retourneert informatie over de gebeurtenis sessie acties.</span><span class="sxs-lookup"><span data-stu-id="3f940-161">Returns information about event session actions.</span></span> |
| <span data-ttu-id="3f940-162">**sys.dm_xe_database_session_events**</span><span class="sxs-lookup"><span data-stu-id="3f940-162">**sys.dm_xe_database_session_events**</span></span> |<span data-ttu-id="3f940-163">Retourneert informatie over sessiegebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="3f940-163">Returns information about session events.</span></span> |
| <span data-ttu-id="3f940-164">**sys.dm_xe_database_session_object_columns**</span><span class="sxs-lookup"><span data-stu-id="3f940-164">**sys.dm_xe_database_session_object_columns**</span></span> |<span data-ttu-id="3f940-165">Hallo configuratiewaarden voor objecten die gebonden tooa sessie zijn ziet.</span><span class="sxs-lookup"><span data-stu-id="3f940-165">Shows hello configuration values for objects that are bound tooa session.</span></span> |
| <span data-ttu-id="3f940-166">**sys.dm_xe_database_session_targets**</span><span class="sxs-lookup"><span data-stu-id="3f940-166">**sys.dm_xe_database_session_targets**</span></span> |<span data-ttu-id="3f940-167">Retourneert informatie over de doelen van de sessie.</span><span class="sxs-lookup"><span data-stu-id="3f940-167">Returns information about session targets.</span></span> |
| <span data-ttu-id="3f940-168">**sys.dm_xe_database_sessions**</span><span class="sxs-lookup"><span data-stu-id="3f940-168">**sys.dm_xe_database_sessions**</span></span> |<span data-ttu-id="3f940-169">Retourneert een rij voor elke gebeurtenissessie die is de huidige database scoped toohello.</span><span class="sxs-lookup"><span data-stu-id="3f940-169">Returns a row for each event session that is scoped toohello current database.</span></span> |

<span data-ttu-id="3f940-170">In Microsoft SQL Server, catalogusweergaven vergelijkbaar zijn met de naam zonder Hallo  *\_database* gedeelte van het Hallo-naam, zoals:</span><span class="sxs-lookup"><span data-stu-id="3f940-170">In Microsoft SQL Server, similar catalog views are named without hello *\_database* portion of hello name, such as:</span></span>

- <span data-ttu-id="3f940-171">**sys.dm_xe_sessions**, in plaats van naam</span><span class="sxs-lookup"><span data-stu-id="3f940-171">**sys.dm_xe_sessions**, instead of name</span></span><br/><span data-ttu-id="3f940-172">**sys.dm_xe_database_sessions**.</span><span class="sxs-lookup"><span data-stu-id="3f940-172">**sys.dm_xe_database_sessions**.</span></span>

### <a name="dmvs-common-tooboth"></a><span data-ttu-id="3f940-173">Algemene tooboth DMV 's</span><span class="sxs-lookup"><span data-stu-id="3f940-173">DMVs common tooboth</span></span>
<span data-ttu-id="3f940-174">Voor uitgebreide gebeurtenissen er zijn aanvullende DMV's die algemene tooboth Azure SQL Database zijn en Microsoft SQL Server:</span><span class="sxs-lookup"><span data-stu-id="3f940-174">For extended events there are additional DMVs that are common tooboth Azure SQL Database and Microsoft SQL Server:</span></span>

- <span data-ttu-id="3f940-175">**sys.dm_xe_map_values**</span><span class="sxs-lookup"><span data-stu-id="3f940-175">**sys.dm_xe_map_values**</span></span>
- <span data-ttu-id="3f940-176">**sys.dm_xe_object_columns**</span><span class="sxs-lookup"><span data-stu-id="3f940-176">**sys.dm_xe_object_columns**</span></span>
- <span data-ttu-id="3f940-177">**sys.dm_xe_objects**</span><span class="sxs-lookup"><span data-stu-id="3f940-177">**sys.dm_xe_objects**</span></span>
- <span data-ttu-id="3f940-178">**sys.dm_xe_packages**</span><span class="sxs-lookup"><span data-stu-id="3f940-178">**sys.dm_xe_packages**</span></span>

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a><span data-ttu-id="3f940-179">Zoeken naar beschikbare uitgebreide gebeurtenissen hello, acties en doelen</span><span class="sxs-lookup"><span data-stu-id="3f940-179">Find hello available extended events, actions, and targets</span></span>

<span data-ttu-id="3f940-180">U kunt een eenvoudige SQL uitvoeren **Selecteer** tooobtain een lijst met beschikbare gebeurtenissen hello, acties en doel.</span><span class="sxs-lookup"><span data-stu-id="3f940-180">You can run a simple SQL **SELECT** tooobtain a list of hello available events, actions, and target.</span></span>

```sql
SELECT
        o.object_type,
        p.name         AS [package_name],
        o.name         AS [db_object_name],
        o.description  AS [db_obj_description]
    FROM
                   sys.dm_xe_objects  AS o
        INNER JOIN sys.dm_xe_packages AS p  ON p.guid = o.package_guid
    WHERE
        o.object_type in
            (
            'action',  'event',  'target'
            )
    ORDER BY
        o.object_type,
        p.name,
        o.name;
```


<span data-ttu-id="3f940-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span><span class="sxs-lookup"><span data-stu-id="3f940-181"><a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;</span></span>

## <a name="targets-for-your-sql-database-event-sessions"></a><span data-ttu-id="3f940-182">Doelen voor uw SQL-Database event-sessies</span><span class="sxs-lookup"><span data-stu-id="3f940-182">Targets for your SQL Database event sessions</span></span>

<span data-ttu-id="3f940-183">Hier volgen doelen die de resultaten van uw event-sessies op SQL-Database kunnen vastleggen:</span><span class="sxs-lookup"><span data-stu-id="3f940-183">Here are targets that can capture results from your event sessions on SQL Database:</span></span>

- <span data-ttu-id="3f940-184">[Ring Buffer doel](http://msdn.microsoft.com/library/ff878182.aspx) -kort bevat gegevens van gebeurtenissen in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="3f940-184">[Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx) - Briefly holds event data in memory.</span></span>
- <span data-ttu-id="3f940-185">[Gebeurtenis teller doel](http://msdn.microsoft.com/library/ff878025.aspx) -telt alle gebeurtenissen die zich tijdens een extended events-sessie voordoen.</span><span class="sxs-lookup"><span data-stu-id="3f940-185">[Event Counter target](http://msdn.microsoft.com/library/ff878025.aspx) - Counts all events that occur during an extended events session.</span></span>
- <span data-ttu-id="3f940-186">[Doel voor het bestand gebeurtenis](http://msdn.microsoft.com/library/ff878115.aspx) -schrijfbewerkingen voltooid buffers tooan Azure Storage-container.</span><span class="sxs-lookup"><span data-stu-id="3f940-186">[Event File target](http://msdn.microsoft.com/library/ff878115.aspx) - Writes complete buffers tooan Azure Storage container.</span></span>

<span data-ttu-id="3f940-187">Hallo [Event Tracing voor Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is niet beschikbaar voor uitgebreide gebeurtenissen op de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="3f940-187">hello [Event Tracing for Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is not available for extended events on SQL Database.</span></span>

## <a name="restrictions"></a><span data-ttu-id="3f940-188">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="3f940-188">Restrictions</span></span>

<span data-ttu-id="3f940-189">Er zijn een aantal betrekking hebben op beveiliging verschillen befitting hello cloudomgeving van SQL-Database:</span><span class="sxs-lookup"><span data-stu-id="3f940-189">There are a couple of security-related differences befitting hello cloud environment of SQL Database:</span></span>

- <span data-ttu-id="3f940-190">Uitgebreide gebeurtenissen zijn gevonden op Hallo één tenantisolatie model.</span><span class="sxs-lookup"><span data-stu-id="3f940-190">Extended events are founded on hello single-tenant isolation model.</span></span> <span data-ttu-id="3f940-191">Een event-sessie in de ene database geen toegang tot gegevens of gebeurtenissen uit een andere database.</span><span class="sxs-lookup"><span data-stu-id="3f940-191">An event session in one database cannot access data or events from another database.</span></span>
- <span data-ttu-id="3f940-192">U het niet mogelijk om een **maken GEBEURTENIS sessie** instructie in de context van Hallo Hallo **master** database.</span><span class="sxs-lookup"><span data-stu-id="3f940-192">You cannot issue a **CREATE EVENT SESSION** statement in hello context of hello **master** database.</span></span>

## <a name="permission-model"></a><span data-ttu-id="3f940-193">Machtiging model</span><span class="sxs-lookup"><span data-stu-id="3f940-193">Permission model</span></span>

<span data-ttu-id="3f940-194">U moet hebben **besturingselement** machtiging op Hallo database tooissue een **maken GEBEURTENIS sessie** instructie.</span><span class="sxs-lookup"><span data-stu-id="3f940-194">You must have **Control** permission on hello database tooissue a **CREATE EVENT SESSION** statement.</span></span> <span data-ttu-id="3f940-195">Hallo database-eigenaar (dbo) heeft **besturingselement** machtiging.</span><span class="sxs-lookup"><span data-stu-id="3f940-195">hello database owner (dbo) has **Control** permission.</span></span>

### <a name="storage-container-authorizations"></a><span data-ttu-id="3f940-196">Storage-container autorisaties</span><span class="sxs-lookup"><span data-stu-id="3f940-196">Storage container authorizations</span></span>

<span data-ttu-id="3f940-197">Hallo SAS-token u genereren voor uw Azure Storage-container moet opgeven **rwl** voor Hallo machtigingen.</span><span class="sxs-lookup"><span data-stu-id="3f940-197">hello SAS token you generate for your Azure Storage container must specify **rwl** for hello permissions.</span></span> <span data-ttu-id="3f940-198">Hallo **rwl** waarde biedt Hallo volgende machtigingen:</span><span class="sxs-lookup"><span data-stu-id="3f940-198">hello **rwl** value provides hello following permissions:</span></span>

- <span data-ttu-id="3f940-199">Lezen</span><span class="sxs-lookup"><span data-stu-id="3f940-199">Read</span></span>
- <span data-ttu-id="3f940-200">Schrijven</span><span class="sxs-lookup"><span data-stu-id="3f940-200">Write</span></span>
- <span data-ttu-id="3f940-201">Lijst</span><span class="sxs-lookup"><span data-stu-id="3f940-201">List</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="3f940-202">Prestatieoverwegingen</span><span class="sxs-lookup"><span data-stu-id="3f940-202">Performance considerations</span></span>

<span data-ttu-id="3f940-203">Er zijn scenario's waar intensief gebruik van uitgebreide gebeurtenissen verzamelen actievere geheugen hebben dan is in orde voor Hallo van het hele systeem.</span><span class="sxs-lookup"><span data-stu-id="3f940-203">There are scenarios where intensive use of extended events can accumulate more active memory than is healthy for hello overall system.</span></span> <span data-ttu-id="3f940-204">Daarom hello Azure SQL Database system dynamisch wordt ingesteld en past u limieten op Hallo hoeveelheid active geheugen die door een gebeurtenissessie kan worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="3f940-204">Therefore hello Azure SQL Database system dynamically sets and adjusts limits on hello amount of active memory that can be accumulated by an event session.</span></span> <span data-ttu-id="3f940-205">Veel factoren gaat u naar Hallo dynamische berekening.</span><span class="sxs-lookup"><span data-stu-id="3f940-205">Many factors go into hello dynamic calculation.</span></span>

<span data-ttu-id="3f940-206">Als u een foutbericht dat een maximum geheugen is afgedwongen ontvangt, zijn sommige corrigerende acties die u kunt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3f940-206">If you receive an error message that says a memory maximum was enforced, some corrective actions you can take are:</span></span>

- <span data-ttu-id="3f940-207">Minder gelijktijdige gebeurtenissessies kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f940-207">Run fewer concurrent event sessions.</span></span>
- <span data-ttu-id="3f940-208">Via uw **maken** en **ALTER** -instructies voor de event-sessies verlagen Hallo en de hoeveelheid geheugen die u op Hallo opgeeft **MAX\_geheugen** component.</span><span class="sxs-lookup"><span data-stu-id="3f940-208">Through your **CREATE** and **ALTER** statements for event sessions, reduce hello amount of memory you specify on hello **MAX\_MEMORY** clause.</span></span>

### <a name="network-latency"></a><span data-ttu-id="3f940-209">Netwerklatentie</span><span class="sxs-lookup"><span data-stu-id="3f940-209">Network latency</span></span>

<span data-ttu-id="3f940-210">Hallo **gebeurtenisbestand** doel tegenkomen netwerklatentie of fouten bij het persistente gegevens tooAzure Storage-blobs.</span><span class="sxs-lookup"><span data-stu-id="3f940-210">hello **Event File** target might experience network latency or failures while persisting data tooAzure Storage blobs.</span></span> <span data-ttu-id="3f940-211">Andere gebeurtenissen in SQL-Database kunnen worden uitgesteld, terwijl ze Hallo netwerk communicatie toocomplete wachten.</span><span class="sxs-lookup"><span data-stu-id="3f940-211">Other events in SQL Database might be delayed while they wait for hello network communication toocomplete.</span></span> <span data-ttu-id="3f940-212">Deze vertraging kan uw werkbelasting vertragen.</span><span class="sxs-lookup"><span data-stu-id="3f940-212">This delay can slow your workload.</span></span>

- <span data-ttu-id="3f940-213">toomitigate deze prestaties risico, Vermijd de instelling Hallo **EVENT_RETENTION_MODE** te optie**NO_EVENT_LOSS** in uw sessie gebeurtenisdefinities.</span><span class="sxs-lookup"><span data-stu-id="3f940-213">toomitigate this performance risk, avoid setting hello **EVENT_RETENTION_MODE** option too**NO_EVENT_LOSS** in your event session definitions.</span></span>

## <a name="related-links"></a><span data-ttu-id="3f940-214">Verwante koppelingen</span><span class="sxs-lookup"><span data-stu-id="3f940-214">Related links</span></span>

- <span data-ttu-id="3f940-215">[Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="3f940-215">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md).</span></span>
- [<span data-ttu-id="3f940-216">Azure-opslag-Cmdlets</span><span class="sxs-lookup"><span data-stu-id="3f940-216">Azure Storage Cmdlets</span></span>](http://msdn.microsoft.com/library/dn806401.aspx)
- <span data-ttu-id="3f940-217">[Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) -bevat uitgebreide informatie over PowerShell en hello Azure Storage-service.</span><span class="sxs-lookup"><span data-stu-id="3f940-217">[Using Azure PowerShell with Azure Storage](../storage/common/storage-powershell-guide-full.md) - Provides comprehensive information about PowerShell and hello Azure Storage service.</span></span>
- [<span data-ttu-id="3f940-218">Hoe toouse .NET Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="3f940-218">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [<span data-ttu-id="3f940-219">CREATE CREDENTIAL (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="3f940-219">CREATE CREDENTIAL (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/ms189522.aspx)
- [<span data-ttu-id="3f940-220">MAKEN van de EVENT-sessie (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="3f940-220">CREATE EVENT SESSION (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/bb677289.aspx)
- [<span data-ttu-id="3f940-221">De Jonathan Kehayias blogberichten over uitgebreide gebeurtenissen in Microsoft SQL Server</span><span class="sxs-lookup"><span data-stu-id="3f940-221">Jonathan Kehayias' blog posts about extended events in Microsoft SQL Server</span></span>](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- <span data-ttu-id="3f940-222">Hello Azure *Service-Updates* webpagina, teruggebracht door parameter tooAzure SQL-Database:</span><span class="sxs-lookup"><span data-stu-id="3f940-222">hello Azure *Service Updates* webpage, narrowed by parameter tooAzure SQL Database:</span></span>
    - [<span data-ttu-id="3f940-223">https://Azure.Microsoft.com/updates/?service=SQL-database</span><span class="sxs-lookup"><span data-stu-id="3f940-223">https://azure.microsoft.com/updates/?service=sql-database</span></span>](https://azure.microsoft.com/updates/?service=sql-database)


<span data-ttu-id="3f940-224">Andere onderwerpen voor het voorbeeld van code voor uitgebreide gebeurtenissen zijn beschikbaar op Hallo koppelingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="3f940-224">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="3f940-225">Echter, moet u eventuele toosee voorbeeld regelmatig controleren of Hallo voorbeeld is bedoeld voor Microsoft SQL Server versus Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3f940-225">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="3f940-226">U kunt vervolgens beslissen of kleine wijzigingen nodig toorun Hallo voorbeeld zijn.</span><span class="sxs-lookup"><span data-stu-id="3f940-226">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
