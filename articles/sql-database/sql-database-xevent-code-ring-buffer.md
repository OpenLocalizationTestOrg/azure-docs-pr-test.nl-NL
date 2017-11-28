---
title: aaaXEvent code ringbuffer voor SQL-Database | Microsoft Docs
description: Biedt een Transact-SQL-codevoorbeeld die eenvoudig en snel door gebruik van Hallo ringbuffer doel in Azure SQL Database is gemaakt.
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
ms.openlocfilehash: 21df748d9999d6837d2b5bbe4a3f47fb351b4633
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="ring-buffer-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="88244-103">Ring Buffer doel code voor uitgebreide gebeurtenissen in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="88244-103">Ring Buffer target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="88244-104">U wilt een compleet codevoorbeeld voor Hallo eenvoudigste snel toocapture en rapport-informatie voor een uitgebreide gebeurtenis tijdens een test.</span><span class="sxs-lookup"><span data-stu-id="88244-104">You want a complete code sample for hello easiest quick way toocapture and report information for an extended event during a test.</span></span> <span data-ttu-id="88244-105">Hallo eenvoudigste doel voor uitgebreide gebeurtenisgegevens is Hallo [ringbuffer doel](http://msdn.microsoft.com/library/ff878182.aspx).</span><span class="sxs-lookup"><span data-stu-id="88244-105">hello easiest target for extended event data is hello [Ring Buffer target](http://msdn.microsoft.com/library/ff878182.aspx).</span></span>

<span data-ttu-id="88244-106">In dit onderwerp wordt een voorbeeld van Transact-SQL-code die:</span><span class="sxs-lookup"><span data-stu-id="88244-106">This topic presents a Transact-SQL code sample that:</span></span>

1. <span data-ttu-id="88244-107">Maakt een tabel met toodemonstrate met gegevens.</span><span class="sxs-lookup"><span data-stu-id="88244-107">Creates a table with data toodemonstrate with.</span></span>
2. <span data-ttu-id="88244-108">Een sessie gemaakt voor een bestaande uitgebreide gebeurtenis, namelijk **sqlserver.sql_statement_starting**.</span><span class="sxs-lookup"><span data-stu-id="88244-108">Creates a session for an existing extended event, namely **sqlserver.sql_statement_starting**.</span></span>
   
   * <span data-ttu-id="88244-109">Hallo gebeurtenis is beperkt tooSQL instructies die een bepaalde Update tekenreeks bevatten: **instructie als '% UPDATE tabEmployee %'**.</span><span class="sxs-lookup"><span data-stu-id="88244-109">hello event is limited tooSQL statements that contain a particular Update string: **statement LIKE '%UPDATE tabEmployee%'**.</span></span>
   * <span data-ttu-id="88244-110">Toosend hello uitvoer van Hallo gebeurtenis tooa doel van het type ringbuffer, namelijk kiest **package0.ring_buffer**.</span><span class="sxs-lookup"><span data-stu-id="88244-110">Chooses toosend hello output of hello event tooa target of type Ring Buffer, namely  **package0.ring_buffer**.</span></span>
3. <span data-ttu-id="88244-111">Hallo event-sessie begint.</span><span class="sxs-lookup"><span data-stu-id="88244-111">Starts hello event session.</span></span>
4. <span data-ttu-id="88244-112">Problemen met een paar eenvoudige UPDATE van SQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="88244-112">Issues a couple of simple SQL UPDATE statements.</span></span>
5. <span data-ttu-id="88244-113">Een SQL SELECT-instructie tooretrieve gebeurtenis uitvoer van Hallo ringbuffer verstrekt.</span><span class="sxs-lookup"><span data-stu-id="88244-113">Issues a SQL SELECT statement tooretrieve event output from hello Ring Buffer.</span></span>
   
   * <span data-ttu-id="88244-114">**sys.dm_xe_database_session_targets** en lid zijn van andere dynamische beheerweergaven (DMV's).</span><span class="sxs-lookup"><span data-stu-id="88244-114">**sys.dm_xe_database_session_targets** and other dynamic management views (DMVs) are joined.</span></span>
6. <span data-ttu-id="88244-115">Hallo gebeurtenissessie stopt.</span><span class="sxs-lookup"><span data-stu-id="88244-115">Stops hello event session.</span></span>
7. <span data-ttu-id="88244-116">Verwijdert Hallo ringbuffer doel, toorelease de daarbij behorende bronnen.</span><span class="sxs-lookup"><span data-stu-id="88244-116">Drops hello Ring Buffer target, toorelease its resources.</span></span>
8. <span data-ttu-id="88244-117">Hallo event-sessie en Hallo demo tabel verwijderd.</span><span class="sxs-lookup"><span data-stu-id="88244-117">Drops hello event session and hello demo table.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88244-118">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88244-118">Prerequisites</span></span>

* <span data-ttu-id="88244-119">Een Azure-account en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="88244-119">An Azure account and subscription.</span></span> <span data-ttu-id="88244-120">U  kunt zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). </span><span class="sxs-lookup"><span data-stu-id="88244-120">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="88244-121">De database die kunt u een tabel in.</span><span class="sxs-lookup"><span data-stu-id="88244-121">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="88244-122">Desgewenst kunt u [maken een **AdventureWorksLT** demonstratiedatabase](sql-database-get-started.md) in minuten.</span><span class="sxs-lookup"><span data-stu-id="88244-122">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="88244-123">SQL Server Management Studio (ssms.exe) in het ideale geval de meest recente maandelijkse updateversie.</span><span class="sxs-lookup"><span data-stu-id="88244-123">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="88244-124">U kunt de meest recente ssms.exe Hallo van downloaden:</span><span class="sxs-lookup"><span data-stu-id="88244-124">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="88244-125">Onderwerp [SQL Server Management Studio downloaden](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="88244-125">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="88244-126">Een directe koppeling toohello downloaden.</span><span class="sxs-lookup"><span data-stu-id="88244-126">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)

## <a name="code-sample"></a><span data-ttu-id="88244-127">Codevoorbeeld</span><span class="sxs-lookup"><span data-stu-id="88244-127">Code sample</span></span>

<span data-ttu-id="88244-128">Met zeer kleine wijziging kan hello codevoorbeeld ringbuffer worden uitgevoerd op Azure SQL Database of Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="88244-128">With very minor modification, hello following Ring Buffer code sample can be run on either Azure SQL Database or Microsoft SQL Server.</span></span> <span data-ttu-id="88244-129">Hallo verschil is Hallo aanwezigheid van Hallo knooppunt '_database' Hallo-naam van een dynamische beheerweergaven (DMV's), die wordt gebruikt in hello FROM-component in stap 5.</span><span class="sxs-lookup"><span data-stu-id="88244-129">hello difference is hello presence of hello node '_database' in hello name of some dynamic management views (DMVs), used in hello FROM clause in Step 5.</span></span> <span data-ttu-id="88244-130">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="88244-130">For example:</span></span>

* <span data-ttu-id="88244-131">sys.dm_xe**_database**_session_targets</span><span class="sxs-lookup"><span data-stu-id="88244-131">sys.dm_xe**_database**_session_targets</span></span>
* <span data-ttu-id="88244-132">sys.dm_xe_session_targets</span><span class="sxs-lookup"><span data-stu-id="88244-132">sys.dm_xe_session_targets</span></span>

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

## <a name="ring-buffer-contents"></a><span data-ttu-id="88244-133">Ring Buffer inhoud</span><span class="sxs-lookup"><span data-stu-id="88244-133">Ring Buffer contents</span></span>

<span data-ttu-id="88244-134">We ssms.exe toorun Hallo codevoorbeeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="88244-134">We used ssms.exe toorun hello code sample.</span></span>

<span data-ttu-id="88244-135">tooview hello resultaten geklikt we Hallo cel onder de kolomkop Hallo **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="88244-135">tooview hello results, we clicked hello cell under hello column header **target_data_XML**.</span></span>

<span data-ttu-id="88244-136">Klik in het resultatenvenster Hallo we Hallo cel onder de kolomkop Hallo geklikt **target_data_XML**.</span><span class="sxs-lookup"><span data-stu-id="88244-136">Then in hello results pane we clicked hello cell under hello column header **target_data_XML**.</span></span> <span data-ttu-id="88244-137">Klikt u op een ander tabblad van het bestand in ssms.exe in welke Hallo inhoud van Hallo resultaatcel wordt weergegeven, als XML gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88244-137">This click created another file tab in ssms.exe in which hello content of hello result cell was displayed, as XML.</span></span>

<span data-ttu-id="88244-138">Hallo-uitvoer wordt weergegeven in Hallo blok te volgen.</span><span class="sxs-lookup"><span data-stu-id="88244-138">hello output is shown in hello following block.</span></span> <span data-ttu-id="88244-139">Het lijkt erop lang, maar dit is slechts twee  **<event>**  elementen.</span><span class="sxs-lookup"><span data-stu-id="88244-139">It looks long, but it is just two **<event>** elements.</span></span>

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


#### <a name="release-resources-held-by-your-ring-buffer"></a><span data-ttu-id="88244-140">Bronnen vastgehouden door uw ringbuffer vrijgeven</span><span class="sxs-lookup"><span data-stu-id="88244-140">Release resources held by your Ring Buffer</span></span>

<span data-ttu-id="88244-141">Wanneer u klaar bent met uw ringbuffer, u kunt verwijderen en de daarbij behorende bronnen uitgeven release een **ALTER** Hallo volgende, zoals:</span><span class="sxs-lookup"><span data-stu-id="88244-141">When you are done with your Ring Buffer, you can remove it and release its resources issuing an **ALTER** like hello following:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    DROP TARGET package0.ring_buffer;
GO
```


<span data-ttu-id="88244-142">Hallo-definitie van de gebeurtenissessie is bijgewerkt, maar niet verwijderd.</span><span class="sxs-lookup"><span data-stu-id="88244-142">hello definition of your event session is updated, but not dropped.</span></span> <span data-ttu-id="88244-143">Later kunt u een ander exemplaar van Hallo ringbuffer tooyour gebeurtenissessie toevoegen:</span><span class="sxs-lookup"><span data-stu-id="88244-143">Later you can add another instance of hello Ring Buffer tooyour event session:</span></span>

```sql
ALTER EVENT SESSION eventsession_gm_azuresqldb51
    ON DATABASE
    ADD TARGET
        package0.ring_buffer
            (SET
                max_memory = 500   -- Units of KB.
            );
```


## <a name="more-information"></a><span data-ttu-id="88244-144">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="88244-144">More information</span></span>

<span data-ttu-id="88244-145">Hallo primaire onderwerp voor uitgebreide gebeurtenissen op Azure SQL Database is:</span><span class="sxs-lookup"><span data-stu-id="88244-145">hello primary topic for extended events on Azure SQL Database is:</span></span>

* <span data-ttu-id="88244-146">[Overwegingen voor gebeurtenissen in SQL-Database uitgebreid](sql-database-xevent-db-diff-from-svr.md), dit in tegenstelling tot bepaalde aspecten van uitgebreide gebeurtenissen die tussen Azure SQL Database ten opzichte van Microsoft SQL Server verschillen.</span><span class="sxs-lookup"><span data-stu-id="88244-146">[Extended event considerations in SQL Database](sql-database-xevent-db-diff-from-svr.md), which contrasts some aspects of extended events that differ between Azure SQL Database versus Microsoft SQL Server.</span></span>

<span data-ttu-id="88244-147">Andere onderwerpen voor het voorbeeld van code voor uitgebreide gebeurtenissen zijn beschikbaar op Hallo koppelingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="88244-147">Other code sample topics for extended events are available at hello following links.</span></span> <span data-ttu-id="88244-148">Echter, moet u eventuele toosee voorbeeld regelmatig controleren of Hallo voorbeeld is bedoeld voor Microsoft SQL Server versus Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="88244-148">However, you must routinely check any sample toosee whether hello sample targets Microsoft SQL Server versus Azure SQL Database.</span></span> <span data-ttu-id="88244-149">U kunt vervolgens beslissen of kleine wijzigingen nodig toorun Hallo voorbeeld zijn.</span><span class="sxs-lookup"><span data-stu-id="88244-149">Then you can decide whether minor changes are needed toorun hello sample.</span></span>

* <span data-ttu-id="88244-150">Voorbeeld van code voor Azure SQL Database: [gebeurtenisbestand doel code voor uitgebreide gebeurtenissen in SQL-Database](sql-database-xevent-code-event-file.md)</span><span class="sxs-lookup"><span data-stu-id="88244-150">Code sample for Azure SQL Database: [Event File target code for extended events in SQL Database](sql-database-xevent-code-event-file.md)</span></span>

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
