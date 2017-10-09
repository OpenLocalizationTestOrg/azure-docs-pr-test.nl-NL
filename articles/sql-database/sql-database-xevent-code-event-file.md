---
title: aaaXEvent gebeurtenisbestand code voor de SQL-Database | Microsoft Docs
description: PowerShell en Transact-SQL biedt voor een in twee fasen voorbeeldcode die laat Hallo gebeurtenisbestand doel in een uitgebreide gebeurtenis op Azure SQL Database zien. Azure Storage is een vereist onderdeel van dit scenario.
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
tags: 
ms.assetid: bbb10ecc-739f-4159-b844-12b4be161231
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: genemi
ms.openlocfilehash: 4457bd3250f4644b54da2f7daddb9da12070e93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a><span data-ttu-id="c3ad9-104">Bestand doel gebeurteniscode voor uitgebreide gebeurtenissen in SQL-Database</span><span class="sxs-lookup"><span data-stu-id="c3ad9-104">Event File target code for extended events in SQL Database</span></span>

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

<span data-ttu-id="c3ad9-105">U wilt een compleet codevoorbeeld voor een robuuste manier toocapture en rapport de informatie voor een uitgebreide gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-105">You want a complete code sample for a robust way toocapture and report information for an extended event.</span></span>

<span data-ttu-id="c3ad9-106">In Microsoft SQL Server, Hallo [gebeurtenisbestand doel](http://msdn.microsoft.com/library/ff878115.aspx) gebruikte toostore gebeurtenis uitvoer naar een lokale vaste schijf-bestand is.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-106">In Microsoft SQL Server, hello [Event File target](http://msdn.microsoft.com/library/ff878115.aspx) is used toostore event outputs into a local hard drive file.</span></span> <span data-ttu-id="c3ad9-107">Maar deze bestanden zijn niet beschikbaar tooAzure SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-107">But such files are not available tooAzure SQL Database.</span></span> <span data-ttu-id="c3ad9-108">We gebruiken in plaats daarvan hello Azure Storage-service toosupport Hallo gebeurtenis doel voor het bestand.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-108">Instead we use hello Azure Storage service toosupport hello Event File target.</span></span>

<span data-ttu-id="c3ad9-109">In dit onderwerp wordt een codevoorbeeld in twee fasen:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-109">This topic presents a two-phase code sample:</span></span>

* <span data-ttu-id="c3ad9-110">PowerShell toocreate een Azure Storage-container in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-110">PowerShell, toocreate an Azure Storage container in hello cloud.</span></span>
* <span data-ttu-id="c3ad9-111">Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-111">Transact-SQL:</span></span>
  
  * <span data-ttu-id="c3ad9-112">tooassign hello Azure Storage-container tooan gebeurtenisbestand doel.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-112">tooassign hello Azure Storage container tooan Event File target.</span></span>
  * <span data-ttu-id="c3ad9-113">gebeurtenissessie toocreate en begin hello, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-113">toocreate and start hello event session, and so on.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3ad9-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c3ad9-114">Prerequisites</span></span>

* <span data-ttu-id="c3ad9-115">Een Azure-account en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-115">An Azure account and subscription.</span></span> <span data-ttu-id="c3ad9-116">U  kunt zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). </span><span class="sxs-lookup"><span data-stu-id="c3ad9-116">You can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c3ad9-117">De database die kunt u een tabel in.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-117">Any database you can create a table in.</span></span>
  
  * <span data-ttu-id="c3ad9-118">Desgewenst kunt u [maken een **AdventureWorksLT** demonstratiedatabase](sql-database-get-started.md) in minuten.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-118">Optionally you can [create an **AdventureWorksLT** demonstration database](sql-database-get-started.md) in minutes.</span></span>
* <span data-ttu-id="c3ad9-119">SQL Server Management Studio (ssms.exe) in het ideale geval de meest recente maandelijkse updateversie.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-119">SQL Server Management Studio (ssms.exe), ideally its latest monthly update version.</span></span> 
  <span data-ttu-id="c3ad9-120">U kunt de meest recente ssms.exe Hallo van downloaden:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-120">You can download hello latest ssms.exe from:</span></span>
  
  * <span data-ttu-id="c3ad9-121">Onderwerp [SQL Server Management Studio downloaden](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3ad9-121">Topic titled [Download SQL Server Management Studio](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>
  * [<span data-ttu-id="c3ad9-122">Een directe koppeling toohello downloaden.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-122">A direct link toohello download.</span></span>](http://go.microsoft.com/fwlink/?linkid=616025)
* <span data-ttu-id="c3ad9-123">U moet hebben Hallo [Azure PowerShell-modules](http://go.microsoft.com/?linkid=9811175) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-123">You must have hello [Azure PowerShell modules](http://go.microsoft.com/?linkid=9811175) installed.</span></span>
  
  * <span data-ttu-id="c3ad9-124">Hallo-modules bieden opdrachten zoals - **nieuw AzureStorageAccount**.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-124">hello modules provide commands such as - **New-AzureStorageAccount**.</span></span>

## <a name="phase-1-powershell-code-for-azure-storage-container"></a><span data-ttu-id="c3ad9-125">Fase 1: PowerShell-code voor Azure Storage-container</span><span class="sxs-lookup"><span data-stu-id="c3ad9-125">Phase 1: PowerShell code for Azure Storage container</span></span>

<span data-ttu-id="c3ad9-126">Deze PowerShell is de fase 1 van Hallo in twee fasen codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-126">This PowerShell is phase 1 of hello two-phase code sample.</span></span>

<span data-ttu-id="c3ad9-127">Hallo-script wordt gestart met opdrachten tooclean nadat een vorige mogelijk uitgevoerd en is rerunnable.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-127">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

1. <span data-ttu-id="c3ad9-128">Hallo PowerShell-script in een teksteditor zoals Notepad.exe plakken en Hallo script opslaan als een bestand met extensie Hallo **.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-128">Paste hello PowerShell script into a simple text editor such as Notepad.exe, and save hello script as a file with hello extension **.ps1**.</span></span>
2. <span data-ttu-id="c3ad9-129">Start PowerShell ISE als beheerder.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-129">Start PowerShell ISE as an Administrator.</span></span>
3. <span data-ttu-id="c3ad9-130">Typ achter Hallo</span><span class="sxs-lookup"><span data-stu-id="c3ad9-130">At hello prompt, type</span></span><br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/><span data-ttu-id="c3ad9-131">en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-131">and then press Enter.</span></span>
4. <span data-ttu-id="c3ad9-132">Open in PowerShell ISE uw **.ps1** bestand.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-132">In PowerShell ISE, open your **.ps1** file.</span></span> <span data-ttu-id="c3ad9-133">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-133">Run hello script.</span></span>
5. <span data-ttu-id="c3ad9-134">Hallo-script voor het eerst een nieuw venster waarin u zich aanmeldt tooAzure opstart.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-134">hello script first starts a new window in which you log in tooAzure.</span></span>
   
   * <span data-ttu-id="c3ad9-135">Als u opnieuw Hallo-script uitvoeren zonder uw sessie verstoren, hebt u Hallo handige optie commentaarteken Hallo **Add-AzureAccount** opdracht.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-135">If you rerun hello script without disrupting your session, you have hello convenient option of commenting out hello **Add-AzureAccount** command.</span></span>

![PowerShell ISE met Azure-module is geïnstalleerd, klaar toorun script.][30_powershell_ise]


### <a name="powershell-code"></a><span data-ttu-id="c3ad9-137">PowerShell-code</span><span class="sxs-lookup"><span data-stu-id="c3ad9-137">PowerShell code</span></span>

```powershell
## TODO: Before running, find all 'TODO' and make each edit!!

#--------------- 1 -----------------------


# You can comment out or skip this Add-AzureAccount
# command after hello first run.
# Current PowerShell environment retains hello successful outcome.

'Expect a pop-up window in which you log in tooAzure.'


Add-AzureAccount

#-------------- 2 ------------------------


'
TODO: Edit hello values assigned toothese variables, especially hello first few!
'

# Ensure hello current date is between
# hello Expiry and Start time values that you edit here.

$subscriptionName    = 'YOUR_SUBSCRIPTION_NAME'
$policySasExpiryTime = '2016-01-28T23:44:56Z'
$policySasStartTime  = '2015-08-01'


$storageAccountName     = 'gmstorageaccountxevent'
$storageAccountLocation = 'West US'
$contextName            = 'gmcontext'
$containerName          = 'gmcontainerxevent'
$policySasToken         = 'gmpolicysastoken'


# Leave this value alone, as 'rwl'.
$policySasPermission = 'rwl'

#--------------- 3 -----------------------


# hello ending display lists your Azure subscriptions.
# One should match hello $subscriptionName value you assigned
#   earlier in this PowerShell script. 

'Choose an existing subscription for hello current PowerShell environment.'


Select-AzureSubscription -SubscriptionName $subscriptionName


#-------------- 4 ------------------------


'
Clean up hello old Azure Storage Account after any previous run, 
before continuing this new run.'


If ($storageAccountName)
{
    Remove-AzureStorageAccount -StorageAccountName $storageAccountName
}

#--------------- 5 -----------------------

[System.DateTime]::Now.ToString()

'
Create a storage account. 
This might take several minutes, will beep when ready.
  ...PLEASE WAIT...'

New-AzureStorageAccount `
    -StorageAccountName $storageAccountName `
    -Location           $storageAccountLocation

[System.DateTime]::Now.ToString()

[System.Media.SystemSounds]::Beep.Play()


'
Get hello primary access key for your storage account.
'


$primaryAccessKey_ForStorageAccount = `
    (Get-AzureStorageKey `
        -StorageAccountName $storageAccountName).Primary

"`$primaryAccessKey_ForStorageAccount = $primaryAccessKey_ForStorageAccount"

'Azure Storage Account cmdlet completed.
Remainder of PowerShell .ps1 script continues.
'

#--------------- 6 -----------------------


# hello context will be needed toocreate a container within hello storage account.

'Create a context object from hello storage account and its primary access key.
'

$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey  $primaryAccessKey_ForStorageAccount


'Create a container within hello storage account.
'


$containerObjectInStorageAccount = New-AzureStorageContainer `
    -Name    $containerName `
    -Context $context


'Create a security policy toobe applied toohello SAS token.
'

New-AzureStorageContainerStoredAccessPolicy `
    -Container  $containerName `
    -Context    $context `
    -Policy     $policySasToken `
    -Permission $policySasPermission `
    -ExpiryTime $policySasExpiryTime `
    -StartTime  $policySasStartTime 

'
Generate a SAS token for hello container.
'
Try
{
    $sasTokenWithPolicy = New-AzureStorageContainerSASToken `
        -Name    $containerName `
        -Context $context `
        -Policy  $policySasToken
}
Catch 
{
    $Error[0].Exception.ToString()
}

#-------------- 7 ------------------------


'Display hello values that YOU must edit into hello Transact-SQL script next!:
'

"storageAccountName: $storageAccountName"
"containerName:      $containerName"
"sasTokenWithPolicy: $sasTokenWithPolicy"

'
REMINDER: sasTokenWithPolicy here might start with "?" character, which you must exclude from Transact-SQL.
'

'
(Later, return here toodelete your Azure Storage account. See hello preceding - Remove-AzureStorageAccount -StorageAccountName $storageAccountName)'

'
Now shift toohello Transact-SQL portion of hello two-part code sample!'

# EOFile
```


<span data-ttu-id="c3ad9-138">Let op Hallo enkele naamwaarden die Hallo PowerShell-script wordt afgedrukt wanneer deze wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-138">Take note of hello few named values that hello PowerShell script prints when it ends.</span></span> <span data-ttu-id="c3ad9-139">U moet deze waarden bewerken in Hallo Transact-SQL-script dat volgt op fase 2.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-139">You must edit those values into hello Transact-SQL script that follows as phase 2.</span></span>

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a><span data-ttu-id="c3ad9-140">Fase 2: Transact-SQL-code die gebruikmaakt van Azure Storage-container</span><span class="sxs-lookup"><span data-stu-id="c3ad9-140">Phase 2: Transact-SQL code that uses Azure Storage container</span></span>

* <span data-ttu-id="c3ad9-141">In stap 1 van dit voorbeeld hebt u een PowerShell-script toocreate een Azure Storage-container.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-141">In phase 1 of this code sample, you ran a PowerShell script toocreate an Azure Storage container.</span></span>
* <span data-ttu-id="c3ad9-142">Naast in fase 2 hello volgende Transact-SQL-script moet Hallo container gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-142">Next in phase 2, hello following Transact-SQL script must use hello container.</span></span>

<span data-ttu-id="c3ad9-143">Hallo-script wordt gestart met opdrachten tooclean nadat een vorige mogelijk uitgevoerd en is rerunnable.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-143">hello script starts with commands tooclean up after a possible previous run, and is rerunnable.</span></span>

<span data-ttu-id="c3ad9-144">Hallo PowerShell-script afgedrukt enkele naamwaarden geëindigd.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-144">hello PowerShell script printed a few named values when it ended.</span></span> <span data-ttu-id="c3ad9-145">Deze waarden, moet u Hallo Transact-SQL-script toouse bewerken.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-145">You must edit hello Transact-SQL script toouse those values.</span></span> <span data-ttu-id="c3ad9-146">Zoeken naar **TODO** in Hallo Transact-SQL-script toolocate Hallo punten bewerken.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-146">Find **TODO** in hello Transact-SQL script toolocate hello edit points.</span></span>

1. <span data-ttu-id="c3ad9-147">Open SQL Server Management Studio (ssms.exe).</span><span class="sxs-lookup"><span data-stu-id="c3ad9-147">Open SQL Server Management Studio (ssms.exe).</span></span>
2. <span data-ttu-id="c3ad9-148">Verbinding maken met tooyour Azure SQL Database database.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-148">Connect tooyour Azure SQL Database database.</span></span>
3. <span data-ttu-id="c3ad9-149">Klik op een nieuwe Querydeelvenster tooopen.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-149">Click tooopen a new query pane.</span></span>
4. <span data-ttu-id="c3ad9-150">Plak de volgende Transact-SQL-script op in het Querydeelvenster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-150">Paste hello following Transact-SQL script into hello query pane.</span></span>
5. <span data-ttu-id="c3ad9-151">Zoeken naar elke **TODO** in script Hallo en relevante Hallo-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-151">Find every **TODO** in hello script and make hello appropriate edits.</span></span>
6. <span data-ttu-id="c3ad9-152">Opslaan en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-152">Save, and then run hello script.</span></span>


> [!WARNING]
> <span data-ttu-id="c3ad9-153">Hallo SAS-sleutelwaarde is gegenereerd door Hallo voorafgaand aan de PowerShell-script kan beginnen met een '?' (vraagteken).</span><span class="sxs-lookup"><span data-stu-id="c3ad9-153">hello SAS key value generated by hello preceding PowerShell script might begin with a '?' (question mark).</span></span> <span data-ttu-id="c3ad9-154">Wanneer u Hallo SAS-sleutel in de volgende T-SQL-script hello gebruikt, moet u *Hallo voorloopspaties verwijderen '?'* .</span><span class="sxs-lookup"><span data-stu-id="c3ad9-154">When you use hello SAS key in hello following T-SQL script, you must *remove hello leading '?'*.</span></span> <span data-ttu-id="c3ad9-155">Anders wordt uw inspanningen mogelijk geblokkeerd door security.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-155">Otherwise your efforts might be blocked by security.</span></span>


### <a name="transact-sql-code"></a><span data-ttu-id="c3ad9-156">Transact-SQL-code</span><span class="sxs-lookup"><span data-stu-id="c3ad9-156">Transact-SQL code</span></span>

```sql
---- TODO: First, run hello PowerShell portion of this two-part code sample.
---- TODO: Second, find every 'TODO' in this Transact-SQL file, and edit each.

---- Transact-SQL code for Event File target on Azure SQL Database.


SET NOCOUNT ON;
GO


----  Step 1.  Establish one little table, and  ---------
----  insert one row of data.


IF EXISTS
    (SELECT * FROM sys.objects
        WHERE type = 'U' and name = 'gmTabEmployee')
BEGIN
    DROP TABLE gmTabEmployee;
END
GO


CREATE TABLE gmTabEmployee
(
    EmployeeGuid         uniqueIdentifier   not null  default newid()  primary key,
    EmployeeId           int                not null  identity(1,1),
    EmployeeKudosCount   int                not null  default 0,
    EmployeeDescr        nvarchar(256)          null
);
GO


INSERT INTO gmTabEmployee ( EmployeeDescr )
    VALUES ( 'Jane Doe' );
GO


------  Step 2.  Create key, and  ------------
------  Create credential (your Azure Storage container must already exist).


IF NOT EXISTS
    (SELECT * FROM sys.symmetric_keys
        WHERE symmetric_key_id = 101)
BEGIN
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '0C34C960-6621-4682-A123-C7EA08E3FC46' -- Or any newid().
END
GO


IF EXISTS
    (SELECT * FROM sys.database_scoped_credentials
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        WHERE name = 'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent')
BEGIN
    DROP DATABASE SCOPED CREDENTIAL
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent] ;
END
GO


CREATE
    DATABASE SCOPED
    CREDENTIAL
        -- use '.blob.',   and not '.queue.' or '.table.' etc.
        -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
        [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    WITH
        IDENTITY = 'SHARED ACCESS SIGNATURE',  -- "SAS" token.
        -- TODO: Paste in hello long SasToken string here for Secret, but exclude any leading '?'.
        SECRET = 'sv=2014-02-14&sr=c&si=gmpolicysastoken&sig=EjAqjo6Nu5xMLEZEkMkLbeF7TD9v1J8DNB2t8gOKTts%3D'
    ;
GO


------  Step 3.  Create (define) an event session.  --------
------  hello event session has an event with an action,
------  and a has a target.

IF EXISTS
    (SELECT * from sys.database_event_sessions
        WHERE name = 'gmeventsessionname240b')
BEGIN
    DROP
        EVENT SESSION
            gmeventsessionname240b
        ON DATABASE;
END
GO


CREATE
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE

    ADD EVENT
        sqlserver.sql_statement_starting
            (
            ACTION (sqlserver.sql_text)
            WHERE statement LIKE 'UPDATE gmTabEmployee%'
            )
    ADD TARGET
        package0.event_file
            (
            -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
            -- Also, tweak hello .xel file name at end, if you like.
            SET filename =
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b.xel'
            )
    WITH
        (MAX_MEMORY = 10 MB,
        MAX_DISPATCH_LATENCY = 3 SECONDS)
    ;
GO


------  Step 4.  Start hello event session.  ----------------
------  Issue hello SQL Update statements that will be traced.
------  Then stop hello session.

------  Note: If hello target fails tooattach,
------  hello session must be stopped and restarted.

ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = START;
GO


SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
GO


ALTER
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE
    STATE = STOP;
GO


-------------- Step 5.  Select hello results. ----------

SELECT
        *, 'CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS!' as [CLICK_NEXT_CELL_TO_BROWSE_ITS_RESULTS],
        CAST(event_data AS XML) AS [event_data_XML]  -- TODO: In ssms.exe results grid, double-click this cell!
    FROM
        sys.fn_xe_file_target_read_file
            (
                -- TODO: Fill in Storage Account name, and hello associated Container name.
                'https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent/anyfilenamexel242b',
                null, null, null
            );
GO


-------------- Step 6.  Clean up. ----------

DROP
    EVENT SESSION
        gmeventsessionname240b
    ON DATABASE;
GO

DROP DATABASE SCOPED CREDENTIAL
    -- TODO: Assign AzureStorageAccount name, and hello associated Container name.
    [https://gmstorageaccountxevent.blob.core.windows.net/gmcontainerxevent]
    ;
GO

DROP TABLE gmTabEmployee;
GO

PRINT 'Use PowerShell Remove-AzureStorageAccount toodelete your Azure Storage account!';
GO
```


<span data-ttu-id="c3ad9-157">Als doel Hallo tooattach mislukt wanneer u uitvoert, moet u stoppen en opnieuw Hallo event-sessie:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-157">If hello target fails tooattach when you run, you must stop and restart hello event session:</span></span>

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a><span data-ttu-id="c3ad9-158">Uitvoer</span><span class="sxs-lookup"><span data-stu-id="c3ad9-158">Output</span></span>

<span data-ttu-id="c3ad9-159">Wanneer Hallo Transact-SQL-script is voltooid, klikt u op een cel onder Hallo **event_data_XML** kolomkop.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-159">When hello Transact-SQL script completes, click a cell under hello **event_data_XML** column header.</span></span> <span data-ttu-id="c3ad9-160">Een  **<event>**  element wordt weergegeven waarin u een UPDATE-instructie.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-160">One **<event>** element is displayed which shows one UPDATE statement.</span></span>

<span data-ttu-id="c3ad9-161">Hier volgt een  **<event>**  element dat is gegenereerd tijdens het testen:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-161">Here is one **<event>** element that was generated during testing:</span></span>


```xml
<event name="sql_statement_starting" package="sqlserver" timestamp="2015-09-22T19:18:45.420Z">
  <data name="state">
    <value>0</value>
    <text>Normal</text>
  </data>
  <data name="line_number">
    <value>5</value>
  </data>
  <data name="offset">
    <value>148</value>
  </data>
  <data name="offset_end">
    <value>368</value>
  </data>
  <data name="statement">
    <value>UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe'</value>
  </data>
  <action name="sql_text" package="sqlserver">
    <value>

SELECT 'BEFORE_Updates', EmployeeKudosCount, * FROM gmTabEmployee;

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 2
    WHERE EmployeeDescr = 'Jane Doe';

UPDATE gmTabEmployee
    SET EmployeeKudosCount = EmployeeKudosCount + 13
    WHERE EmployeeDescr = 'Jane Doe';

SELECT 'AFTER__Updates', EmployeeKudosCount, * FROM gmTabEmployee;
</value>
  </action>
</event>
```


<span data-ttu-id="c3ad9-162">Hallo voorgaande Transact-SQL-script waarmee Hallo system functie tooread hello event_file te volgen:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-162">hello preceding Transact-SQL script used hello following system function tooread hello event_file:</span></span>

* [<span data-ttu-id="c3ad9-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="c3ad9-163">sys.fn_xe_file_target_read_file (Transact-SQL)</span></span>](http://msdn.microsoft.com/library/cc280743.aspx)

<span data-ttu-id="c3ad9-164">Er is een uitleg van de geavanceerde opties voor het Hallo-weergave van gegevens van uitgebreide gebeurtenissen beschikbaar op:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-164">An explanation of advanced options for hello viewing of data from extended events is available at:</span></span>

* [<span data-ttu-id="c3ad9-165">Geavanceerde van doelgegevens van uitgebreide gebeurtenissen weergeven</span><span class="sxs-lookup"><span data-stu-id="c3ad9-165">Advanced Viewing of Target Data from Extended Events</span></span>](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a><span data-ttu-id="c3ad9-166">Hallo code voorbeeld toorun op SQL Server converteren</span><span class="sxs-lookup"><span data-stu-id="c3ad9-166">Converting hello code sample toorun on SQL Server</span></span>

<span data-ttu-id="c3ad9-167">Stel dat u deze wilde toorun Hallo Transact-SQL-voorbeeld vóór op Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-167">Suppose you wanted toorun hello preceding Transact-SQL sample on Microsoft SQL Server.</span></span>

* <span data-ttu-id="c3ad9-168">Voor eenvoud, zou u toocompletely vervangen gebruik van hello Azure Storage-container wilt met een eenvoudige bestand zoals **C:\myeventdata.xel**.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-168">For simplicity, you would want toocompletely replace use of hello Azure Storage container with a simple file such as **C:\myeventdata.xel**.</span></span> <span data-ttu-id="c3ad9-169">Hallo bestand zou toohello lokale vaste schijf van Hallo-computer die als host fungeert voor SQL Server worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-169">hello file would be written toohello local hard drive of hello computer that hosts SQL Server.</span></span>
* <span data-ttu-id="c3ad9-170">U hoeft niet elk soort Transact-SQL-instructies voor **CREATE MASTER KEY** en **referentie maken**.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-170">You would not need any kind of Transact-SQL statements for **CREATE MASTER KEY** and **CREATE CREDENTIAL**.</span></span>
* <span data-ttu-id="c3ad9-171">In Hallo **maken GEBEURTENIS sessie** instructie in de **doel toevoegen** -component bevat, vervangt u Hallo HTTP-waarde die is toegewezen te worden aangebracht**filename =** met een volledig padtekenreeks zoals  **C:\myfile.xel**.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-171">In hello **CREATE EVENT SESSION** statement, in its **ADD TARGET** clause, you would replace hello Http value assigned made too**filename=** with a full path string like **C:\myfile.xel**.</span></span>
  
  * <span data-ttu-id="c3ad9-172">Er is geen Azure Storage-account moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c3ad9-172">No Azure Storage account need be involved.</span></span>

## <a name="more-information"></a><span data-ttu-id="c3ad9-173">Meer informatie</span><span class="sxs-lookup"><span data-stu-id="c3ad9-173">More information</span></span>

<span data-ttu-id="c3ad9-174">Zie voor meer informatie over accounts en containers in hello Azure Storage-service:</span><span class="sxs-lookup"><span data-stu-id="c3ad9-174">For more info about accounts and containers in hello Azure Storage service, see:</span></span>

* [<span data-ttu-id="c3ad9-175">Hoe toouse .NET Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="c3ad9-175">How toouse Blob storage from .NET</span></span>](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="c3ad9-176">Naamgeving en verwijzen naar Containers, Blobs en metagegevens</span><span class="sxs-lookup"><span data-stu-id="c3ad9-176">Naming and Referencing Containers, Blobs, and Metadata</span></span>](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [<span data-ttu-id="c3ad9-177">Werken met Hallo hoofdcontainer</span><span class="sxs-lookup"><span data-stu-id="c3ad9-177">Working with hello Root Container</span></span>](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [<span data-ttu-id="c3ad9-178">Les 1: Een toegangsbeleid opgeslagen en een shared access signature maken op een Azure-container</span><span class="sxs-lookup"><span data-stu-id="c3ad9-178">Lesson 1: Create a stored access policy and a shared access signature on an Azure container</span></span>](http://msdn.microsoft.com/library/dn466430.aspx)
  * [<span data-ttu-id="c3ad9-179">Les 2: Een SQL Server-referentie met een shared access signature maken</span><span class="sxs-lookup"><span data-stu-id="c3ad9-179">Lesson 2: Create a SQL Server credential using a shared access signature</span></span>](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

