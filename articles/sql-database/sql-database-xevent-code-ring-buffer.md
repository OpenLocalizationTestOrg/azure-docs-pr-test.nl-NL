---
title: XEvent-ringbuffer code voor de SQL-Database | Microsoft Docs
description: Biedt een Transact-SQL-codevoorbeeld die eenvoudig en snel door gebruik van het doel ringbuffer in Azure SQL Database is gemaakt.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: 2510fb3f-c8f2-437a-8f49-9d5f6c96e75b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: genemi
ms.openlocfilehash: 6fbefe151901ac3b15d93712422878fc4d6206f1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="2f843-103">Ring Buffer doel code voor uitgebreide gebeurtenissen in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="2f843-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="2f843-104">U wilt een compleet codevoorbeeld voor het snel eenvoudigst vastleggen en rapport-informatie voor een uitgebreide gebeurtenis tijdens een test.</span><span class="sxs-lookup"><span data-stu-id="2f843-104">You want a complete code sample for the easiest quick way to capture and report information for an extended event during a test.</span></span> <span data-ttu-id="2f843-105">De eenvoudigste doel voor uitgebreide gebeurtenisgegevens de [ringbuffer doel](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f843-105">The easiest target for extended event data is the [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="2f843-106">In dit onderwerp wordt een voorbeeld van Transact-SQL-code die:</span><span class="sxs-lookup"><span data-stu-id="2f843-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="2f843-107">Maakt een tabel met gegevens voor het demonstreren van met.</span><span class="sxs-lookup"><span data-stu-id="2f843-107">Creates a table with data to demonstrate with.</span></span>
2. <span data-ttu-id="2f843-108">Een sessie gemaakt voor een bestaande uitgebreide gebeurtenis, namelijk **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="2f843-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="2f843-109">De gebeurtenis is beperkt tot de SQL-instructies die een bepaalde Update tekenreeks bevatten: **instructie als '% UPDATE tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="2f843-109">The event is limited to SQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="2f843-110">Kiest voor het verzenden van de uitvoer van de gebeurtenis aan een doel van het type ringbuffer, namelijk **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="2f843-110">Chooses to send the output of the event to a target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="2f843-111">Start de gebeurtenissessie.</span><span class="sxs-lookup"><span data-stu-id="2f843-111">Starts the event session.</span></span>
4. <span data-ttu-id="2f843-112">Problemen met een paar eenvoudige UPDATE van SQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="2f843-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="2f843-113">Een SQL SELECT-instructie voor het ophalen van gebeurtenis uitvoer van de ringbuffer verstrekt.</span><span class="sxs-lookup"><span data-stu-id="2f843-113">Issues a SQL SELECT statement to retrieve event output from the Ring Buffer.</span></span>
   
   * <span data-ttu-id="2f843-114">**sys.dm_xe_database_session_targets** en lid zijn van andere dynamische beheerweergaven (DMV's).</span><span class="sxs-lookup"><span data-stu-id="2f843-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="2f843-115">Stopt de gebeurtenissessie.</span><span class="sxs-lookup"><span data-stu-id="2f843-115">Stops the event session.</span></span>
7. <span data-ttu-id="2f843-116">Het doel ringbuffer release van de resources verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2f843-116">Drops the Ring Buffer target, to release its resources.</span></span>
8. <span data-ttu-id="2f843-117">De gebeurtenissessie en de demo-tabel verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2f843-117">Drops the event session and the demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f843-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2f843-118">Prerequisites</span></span>

* <span data-ttu-id="2f843-119">Een Azure-account en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f843-119">An Azure account and subscription.</span></span> <span data-ttu-id="2f843-120">U  kunt zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). </span><span class="sxs-lookup"><span data-stu-id="2f843-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2f843-121">De database die kunt u een tabel in.</span><span class="sxs-lookup"><span data-stu-id="2f843-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="2f843-122">Desgewenst kunt u [maken een **AdventureWorksLT** demonstratiedatabase](sql-database-get-started.md) in minuten.</span><span class="sxs-lookup"><span data-stu-id="2f843-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="2f843-123">SQL Server Management Studio (ssms.exe) in het ideale geval de meest recente maandelijkse updateversie.</span><span class="sxs-lookup"><span data-stu-id="2f843-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="2f843-124">U kunt de meest recente ssms.exe van downloaden:</span><span class="sxs-lookup"><span data-stu-id="2f843-124">You can download the latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="2f843-125">Onderwerp [SQL Server Management Studio downloaden](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f843-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="2f843-126">Een directe koppeling naar de download.</span><span class="sxs-lookup"><span data-stu-id="2f843-126">A direct link to the download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="2f843-127">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="2f843-127">Code sample</span></span>

<span data-ttu-id="2f843-128">Met zeer kleine wijziging, kan het volgende codevoorbeeld van ringbuffer worden uitgevoerd op Azure SQL Database of Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2f843-128">With very minor modification, the following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="2f843-129">Het verschil is de aanwezigheid van het knooppunt '_database' in de naam van een dynamische beheerweergaven (DMV's), die wordt gebruikt in de component FROM in stap 5.</span><span class="sxs-lookup"><span data-stu-id="2f843-129">The difference is the presence of the node '_database' in the name of some dynamic management views (DMVs), used in the FROM clause in Step 5.</span></span> <span data-ttu-id="2f843-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f843-130">For example:</span></span>

* <span data-ttu-id="2f843-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="2f843-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="2f843-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="2f843-132">sys.dm_xe_session_targets</span></span>

&nbsp;

```sql
GO
----  Transact-SQL.
---- Step set 1.

SET NOCOUNT ON;
GO


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'tabEmployee')
BEGIN
    DROP TABLE tabEmployee;
END
GO


CREATE TABLE tabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO tabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO

---- Step set 2.


IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'eventsession_gm_azuresqldb51')
BEGIN
    DROP EVENT SESSION eventsession_gm_azuresqldb51
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE '%UPDATE tabEmployee%'
            )
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
GO

---- Step set 3.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = START;
GO

---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
GO

---- Step set 5.


SELECT
    se.name                      AS [session-name],
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source,
    st.target_data,
    CAST(st.target_data AS XML)  AS [target_data_XML]
FROM
               sys.dm_xe_database_session_event_actions  AS ac

    INNER JOIN sys.dm_xe_database_session_events         AS ev  ON ev.event_name = ac.event_name
        AND CAST(ev.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_object_columns AS oc
         ON CAST(oc.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_session_targets        AS st
         ON CAST(st.event_session_address AS BINARY(8)) = CAST(ac.event_session_address AS BINARY(8))

    INNER JOIN sys.dm_xe_database_sessions               AS se
         ON CAST(ac.event_session_address AS BINARY(8)) = CAST(se.address AS BINARY(8))
WHERE
        oc.column_name = 'occurrence_number'
    AND
        se.name        = 'eventsession_gm_azuresqldb51'
    AND
        ac.action_name = 'sql_text'
ORDER BY
    se.name,
    ev.event_name,
    ac.action_name,
    st.target_name,
    se.session_source
;
GO

---- Step set 6.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    STATE = STOP;
GO

---- Step set 7.


ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO

---- Step set 8.


DROP EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE;
GO

DROP TABLE tabEmployee;
GO
```


&nbsp;

## <a name="ring-buffer-contents"></a><span data-ttu-id="2f843-133">Ring Buffer inhoud</span><span class="sxs-lookup"><span data-stu-id="2f843-133">Ring Buffer contents</span></span>

<span data-ttu-id="2f843-134">We ssms.exe gebruikt voor het uitvoeren van het codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2f843-134">We used ssms.exe to run the code sample.</span></span>

<span data-ttu-id="2f843-135">U kunt de resultaten, we de cel onder de kolomkop geklikt **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="2f843-135">To view the results, we clicked the cell under the column header **target_data_XML**.</span></span>

<span data-ttu-id="2f843-136">Klik in het deelvenster met resultaten we de cel onder de kolomkop geklikt **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="2f843-136">Then in the results pane we clicked the cell under the column header **target_data_XML**.</span></span> <span data-ttu-id="2f843-137">Klikt u op een ander tabblad van het bestand in ssms.exe waarin de inhoud van de resultaatcel wordt weergegeven, als XML gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f843-137">This click created another file tab in ssms.exe in which the content of the result cell was displayed, as XML.</span></span>

<span data-ttu-id="2f843-138">De uitvoer wordt weergegeven in het volgende blok.</span><span class="sxs-lookup"><span data-stu-id="2f843-138">The output is shown in the following block.</span></span> <span data-ttu-id="2f843-139">Het lijkt erop lang, maar dit is slechts twee  **<event>**  elementen.</span><span class="sxs-lookup"><span data-stu-id="2f843-139">It looks long, but it is just two **<event>** elements.</span></span>

&nbsp;

```
<RingBufferTarget truncated="0" processingTime="0" totalEventsProcessed="2" eventCount="2" droppedCount="0" memoryUsed="1728">
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.317Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>7</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>184</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>328</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
  <event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T15:29:31.327Z">
    <data name="state">
      <type name="statement_starting_state" package="sqlserver" />
      <value>0</value>
      <text>Normal</text>
    </data>
    <data name="line_number">
      <type name="int32" package="package0" />
      <value>10</value>
    </data>
    <data name="offset">
      <type name="int32" package="package0" />
      <value>340</value>
    </data>
    <data name="offset_end">
      <type name="int32" package="package0" />
      <value>486</value>
    </data>
    <data name="statement">
      <type name="unicode_string" package="package0" />
      <value>UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015</value>
    </data>
    <action name="sql_text" package="sqlserver">
      <type name="unicode_string" package="package0" />
      <value>
---- Step set 4.


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM tabEmployee;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 102;

UPDATE tabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 1015;

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM tabEmployee;
</value>
    </action>
  </event>
</RingBufferTarget>
```


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="2f843-140">Bronnen vastgehouden door uw ringbuffer vrijgeven</span><span class="sxs-lookup"><span data-stu-id="2f843-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="2f843-141">Wanneer u klaar bent met uw ringbuffer, u kunt verwijderen en de daarbij behorende bronnen uitgeven release een **ALTER** als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f843-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like the following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="2f843-142">De definitie van de gebeurtenissessie is bijgewerkt, maar niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2f843-142">The definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="2f843-143">U kunt een ander exemplaar van de ringbuffer later toevoegen aan uw gebeurtenissessie:</span><span class="sxs-lookup"><span data-stu-id="2f843-143">Later you can add another instance of the Ring Buffer to your event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="2f843-144">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="2f843-144">More information</span></span>

<span data-ttu-id="2f843-145">Het primaire onderwerp voor uitgebreide gebeurtenissen op Azure SQL Database is:</span><span class="sxs-lookup"><span data-stu-id="2f843-145">The primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="2f843-146">[Overwegingen voor gebeurtenissen in SQL-Database uitgebreid](sql-database-xevent-db-diff-from-svr.md), dit in tegenstelling tot bepaalde aspecten van uitgebreide gebeurtenissen die tussen Azure SQL Database ten opzichte van Microsoft SQL Server verschillen.</span><span class="sxs-lookup"><span data-stu-id="2f843-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="2f843-147">Er zijn andere onderwerpen voor het voorbeeld van code voor uitgebreide gebeurtenissen beschikbaar op de volgende koppelingen.</span><span class="sxs-lookup"><span data-stu-id="2f843-147">Other code sample topics for extended events are available at the following links.</span></span> <span data-ttu-id="2f843-148">Echter, moet u een voorbeeld om te zien of het voorbeeld is bedoeld voor Microsoft SQL Server versus Azure SQL Database regelmatig controleren.</span><span class="sxs-lookup"><span data-stu-id="2f843-148">However, you must routinely check any sample to see whether the sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="2f843-149">U kunt vervolgens beslissen of kleine wijzigingen nodig zijn om uit te voeren van het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2f843-149">Then you can decide whether minor changes are needed to run the sample.</span></span>

* <span data-ttu-id="2f843-150">Voorbeeld van code voor Azure SQL Database: [gebeurtenisbestand doel code voor uitgebreide gebeurtenissen in SQL-Database](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="2f843-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find the Objects That Have the Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
