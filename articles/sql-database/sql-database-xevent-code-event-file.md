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
# <a name="event-file-target-code-for-extended-events-in-sql-database"></a>Bestand doel gebeurteniscode voor uitgebreide gebeurtenissen in SQL-Database

[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

U wilt een compleet codevoorbeeld voor een robuuste manier toocapture en rapport de informatie voor een uitgebreide gebeurtenis.

In Microsoft SQL Server, Hallo [gebeurtenisbestand doel](http://msdn.microsoft.com/library/ff878115.aspx) gebruikte toostore gebeurtenis uitvoer naar een lokale vaste schijf-bestand is. Maar deze bestanden zijn niet beschikbaar tooAzure SQL-Database. We gebruiken in plaats daarvan hello Azure Storage-service toosupport Hallo gebeurtenis doel voor het bestand.

In dit onderwerp wordt een codevoorbeeld in twee fasen:

* PowerShell toocreate een Azure Storage-container in Hallo cloud.
* Transact-SQL:
  
  * tooassign hello Azure Storage-container tooan gebeurtenisbestand doel.
  * gebeurtenissessie toocreate en begin hello, enzovoort.

## <a name="prerequisites"></a>Vereisten

* Een Azure-account en -abonnement. U  kunt zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/). 
* De database die kunt u een tabel in.
  
  * Desgewenst kunt u [maken een **AdventureWorksLT** demonstratiedatabase](sql-database-get-started.md) in minuten.
* SQL Server Management Studio (ssms.exe) in het ideale geval de meest recente maandelijkse updateversie. 
  U kunt de meest recente ssms.exe Hallo van downloaden:
  
  * Onderwerp [SQL Server Management Studio downloaden](http://msdn.microsoft.com/library/mt238290.aspx).
  * [Een directe koppeling toohello downloaden.](http://go.microsoft.com/fwlink/?linkid=616025)
* U moet hebben Hallo [Azure PowerShell-modules](http://go.microsoft.com/?linkid=9811175) geïnstalleerd.
  
  * Hallo-modules bieden opdrachten zoals - **nieuw AzureStorageAccount**.

## <a name="phase-1-powershell-code-for-azure-storage-container"></a>Fase 1: PowerShell-code voor Azure Storage-container

Deze PowerShell is de fase 1 van Hallo in twee fasen codevoorbeeld.

Hallo-script wordt gestart met opdrachten tooclean nadat een vorige mogelijk uitgevoerd en is rerunnable.

1. Hallo PowerShell-script in een teksteditor zoals Notepad.exe plakken en Hallo script opslaan als een bestand met extensie Hallo **.ps1**.
2. Start PowerShell ISE als beheerder.
3. Typ achter Hallo<br/>`Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Scope CurrentUser`<br/>en druk op Enter.
4. Open in PowerShell ISE uw **.ps1** bestand. Hallo-script uitvoeren.
5. Hallo-script voor het eerst een nieuw venster waarin u zich aanmeldt tooAzure opstart.
   
   * Als u opnieuw Hallo-script uitvoeren zonder uw sessie verstoren, hebt u Hallo handige optie commentaarteken Hallo **Add-AzureAccount** opdracht.

![PowerShell ISE met Azure-module is geïnstalleerd, klaar toorun script.][30_powershell_ise]


### <a name="powershell-code"></a>PowerShell-code

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


Let op Hallo enkele naamwaarden die Hallo PowerShell-script wordt afgedrukt wanneer deze wordt beëindigd. U moet deze waarden bewerken in Hallo Transact-SQL-script dat volgt op fase 2.

## <a name="phase-2-transact-sql-code-that-uses-azure-storage-container"></a>Fase 2: Transact-SQL-code die gebruikmaakt van Azure Storage-container

* In stap 1 van dit voorbeeld hebt u een PowerShell-script toocreate een Azure Storage-container.
* Naast in fase 2 hello volgende Transact-SQL-script moet Hallo container gebruiken.

Hallo-script wordt gestart met opdrachten tooclean nadat een vorige mogelijk uitgevoerd en is rerunnable.

Hallo PowerShell-script afgedrukt enkele naamwaarden geëindigd. Deze waarden, moet u Hallo Transact-SQL-script toouse bewerken. Zoeken naar **TODO** in Hallo Transact-SQL-script toolocate Hallo punten bewerken.

1. Open SQL Server Management Studio (ssms.exe).
2. Verbinding maken met tooyour Azure SQL Database database.
3. Klik op een nieuwe Querydeelvenster tooopen.
4. Plak de volgende Transact-SQL-script op in het Querydeelvenster Hallo Hallo.
5. Zoeken naar elke **TODO** in script Hallo en relevante Hallo-bewerkingen.
6. Opslaan en vervolgens Hallo-script uitvoeren.


> [!WARNING]
> Hallo SAS-sleutelwaarde is gegenereerd door Hallo voorafgaand aan de PowerShell-script kan beginnen met een '?' (vraagteken). Wanneer u Hallo SAS-sleutel in de volgende T-SQL-script hello gebruikt, moet u *Hallo voorloopspaties verwijderen '?'* . Anders wordt uw inspanningen mogelijk geblokkeerd door security.


### <a name="transact-sql-code"></a>Transact-SQL-code

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


Als doel Hallo tooattach mislukt wanneer u uitvoert, moet u stoppen en opnieuw Hallo event-sessie:

```sql
ALTER EVENT SESSION ... STATE = STOP;
GO
ALTER EVENT SESSION ... STATE = START;
GO
```


## <a name="output"></a>Uitvoer

Wanneer Hallo Transact-SQL-script is voltooid, klikt u op een cel onder Hallo **event_data_XML** kolomkop. Een  **<event>**  element wordt weergegeven waarin u een UPDATE-instructie.

Hier volgt een  **<event>**  element dat is gegenereerd tijdens het testen:


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


Hallo voorgaande Transact-SQL-script waarmee Hallo system functie tooread hello event_file te volgen:

* [sys.fn_xe_file_target_read_file (Transact-SQL)](http://msdn.microsoft.com/library/cc280743.aspx)

Er is een uitleg van de geavanceerde opties voor het Hallo-weergave van gegevens van uitgebreide gebeurtenissen beschikbaar op:

* [Geavanceerde van doelgegevens van uitgebreide gebeurtenissen weergeven](http://msdn.microsoft.com/library/mt752502.aspx)


## <a name="converting-hello-code-sample-toorun-on-sql-server"></a>Hallo code voorbeeld toorun op SQL Server converteren

Stel dat u deze wilde toorun Hallo Transact-SQL-voorbeeld vóór op Microsoft SQL Server.

* Voor eenvoud, zou u toocompletely vervangen gebruik van hello Azure Storage-container wilt met een eenvoudige bestand zoals **C:\myeventdata.xel**. Hallo bestand zou toohello lokale vaste schijf van Hallo-computer die als host fungeert voor SQL Server worden geschreven.
* U hoeft niet elk soort Transact-SQL-instructies voor **CREATE MASTER KEY** en **referentie maken**.
* In Hallo **maken GEBEURTENIS sessie** instructie in de **doel toevoegen** -component bevat, vervangt u Hallo HTTP-waarde die is toegewezen te worden aangebracht**filename =** met een volledig padtekenreeks zoals  **C:\myfile.xel**.
  
  * Er is geen Azure Storage-account moet worden uitgevoerd.

## <a name="more-information"></a>Meer informatie

Zie voor meer informatie over accounts en containers in hello Azure Storage-service:

* [Hoe toouse .NET Blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Naamgeving en verwijzen naar Containers, Blobs en metagegevens](http://msdn.microsoft.com/library/azure/dd135715.aspx)
* [Werken met Hallo hoofdcontainer](http://msdn.microsoft.com/library/azure/ee395424.aspx)
* [Les 1: Een toegangsbeleid opgeslagen en een shared access signature maken op een Azure-container](http://msdn.microsoft.com/library/dn466430.aspx)
  * [Les 2: Een SQL Server-referentie met een shared access signature maken](http://msdn.microsoft.com/library/dn466435.aspx)

<!--
Image references.
-->

[30_powershell_ise]: ./media/sql-database-xevent-code-event-file/event-file-powershell-ise-b30.png

