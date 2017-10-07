---
title: aaaCreate en beheren van elastische taken met behulp van PowerShell | Microsoft Docs
description: PowerShell toomanage Azure SQL Database-groepen gebruikt
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Maken en beheren van de SQL-Database van de elastische taken met behulp van PowerShell (preview)

Hallo PowerShell APIs voor **elastische Database taken** (in preview) kunt u definiëren van een groep met databases op basis waarvan de scripts worden uitgevoerd. Dit artikel laat zien hoe toocreate en beheren van **elastische Database taken** met PowerShell-cmdlets. Zie [elastische taken overzicht](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie voor een gratis proefversie [gratis proefversie van één maand](https://azure.microsoft.com/pricing/free-trial/).
* Een set databases die zijn gemaakt met Hallo-hulpprogramma's voor elastische Database. Zie [aan de slag met hulpprogramma's voor elastische Database](sql-database-elastic-scale-get-started.md).
* Azure PowerShell. Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **Elastische Database taken** PowerShell pakket: Zie [elastische Database installeren taken](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Selecteer uw Azure-abonnement
tooselect hello abonnement, moet u uw abonnements-Id (**- SubscriptionId**) of de naam van abonnement (**- SubscriptionName**). Als u meerdere abonnementen hebt kunt u Hallo uitvoeren **Get-AzureRmSubscription** cmdlet en kopieer Hallo gewenst abonnementsgegevens van Hallo resultatenset. Zodra u hebt uw abonnementsgegevens, Hallo commandlet tooset na dit abonnement uitgevoerd als Hallo standaard, namelijk Hallo doel voor het maken en beheren van taken:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Hallo [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) wordt aanbevolen voor gebruik toodevelop en PowerShell-scripts uitvoeren op Hallo elastische Database taken uitvoeren.

## <a name="elastic-database-jobs-objects"></a>Elastische taken databaseobjecten
Hallo volgende Tabellijsten uit alle objecttypen Hallo van **elastische Database taken** samen met de beschrijving en de relevante PowerShell APIs.

<table style="width:100%">
  <tr>
    <th>Objecttype</th>
    <th>Beschrijving</th>
    <th>Gerelateerde PowerShell API 's</th>
  </tr>
  <tr>
    <td>Referentie</td>
    <td>Gebruikersnaam en wachtwoord toouse bij het verbinden van toodatabases voor uitvoering van scripts of de toepassing van DACPACs. <p>Hallo-wachtwoord is versleuteld voordat tooand opslaan in Hallo elastische taken van de Database-database worden verzonden.  Hallo-wachtwoord worden ontsleuteld door Hallo Hallo referentie gemaakt en dat is geüpload van het script voor installatie Hallo elastische taken van de Database-service.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>Nieuwe AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Script</td>
    <td>Toobe van Transact-SQL-script gebruikt voor uitvoering tussen databases.  Hallo script moet opgestelde toobe idempotent omdat het Hallo-service wordt opnieuw geprobeerd de uitvoering van script Hallo bij fouten.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>Nieuwe AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">-Gegevenslaagtoepassing </a> toobe toegepast tussen databases van het pakket.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Nieuwe AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Database-doel</td>
    <td>Database- en geef een naam aan wijzen tooan Azure SQL Database.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Nieuwe AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Doel van shard-kaart</td>
    <td>Combinatie van een doel van de database en een referentie-toobe gebruikt toodetermine informatie opgeslagen in een elastische Database shard-toewijzing.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Nieuwe AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Doel van de aangepaste verzameling</td>
    <td>Gedefinieerde groep databases toocollectively gebruiken voor uitvoering.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>Nieuwe AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Aangepaste verzameling onderliggende doel</td>
    <td>Database-doel waarnaar wordt verwezen in een aangepaste verzameling.</td>
    <td>
    <p>Voeg AzureSqlJobChildTarget</p>
    <p>Verwijder AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Job</td>
    <td>
    <p>Definitie van de parameters voor een taak die gebruikt tootrigger uitvoering of toofulfill een planning worden kunnen.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>Nieuwe AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Uitvoeren van taak</td>
    <td>
    <p>Container van de benodigde toofulfill taken uitvoeren van een script of toepassen van een DACPAC tooa doel met referenties voor databaseverbindingen met fouten in overeenstemming tooan uitvoeringsbeleid behandeld.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start AzureSqlJobExecution</p>
    <p>Stop AzureSqlJobExecution</p>
    <p>Wacht AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Uitvoering van de taak taak</td>
    <td>
    <p>De eenheid van werk toofulfill een taak.</p>
    <p>Als een taak niet kunnen toosuccessfully uitvoeren, Hallo resulterende uitzondering vastgelegd en een nieuwe, overeenkomende projecttaak worden gemaakt en uitgevoerd in overeenstemming toohello opgegeven uitvoeringsbeleid.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start AzureSqlJobExecution</p>
    <p>Stop AzureSqlJobExecution</p>
    <p>Wacht AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Taak uitvoeringsbeleid</td>
    <td>
    <p>Besturingselementen taak uitvoering time-outs, limieten voor nieuwe pogingen en interval tussen nieuwe pogingen.</p>
    <p>Elastische taken van de Database bevat een standaarduitvoeringsbeleid taak waardoor in feite oneindige pogingen van de mislukte taak met exponentieel uitstel intervallen tussen nieuwe pogingen.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>Nieuwe AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Planning</td>
    <td>
    <p>Specificatie voor uitvoering tootake plaats in een interval van terugkerende of één keer op basis van tijd.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>Nieuwe AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Taak wordt geactiveerd</td>
    <td>
    <p>Een toewijzing tussen een taak en een planning tootrigger taakuitvoering volgens planning toohello.</p>
    </td>
    <td>
    <p>Nieuwe AzureSqlJobTrigger</p>
    <p>Verwijder AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Ondersteunde elastische Database taken groeperen typen
Hallo-taak uitgevoerd (T-SQL) Transact-SQL-scripts of de toepassing van DACPACs in een groep van databases. Wanneer een taak verzonden toobe uitgevoerd wordt via aangevraagd een groep van databases, Hallo-taak 'breidt' hello naar onderliggende taken waarbij elk Hallo uitvoert uitgevoerd op een individuele database in het Hallo-groep. 

Er zijn twee typen groepen die u kunt maken: 

* [Shard-toewijzing](sql-database-elastic-scale-shard-map-management.md) groep: wanneer een taak verzonden tootarget een shard-toewijzing is, Hallo taak Hallo shard-toewijzing toodetermine vraagt de huidige set shards en maakt vervolgens onderliggende taken voor elke shard in Hallo shard-toewijzing.
* Verzamelgroep voor de aangepaste: een aangepaste set van databases gedefinieerd. Wanneer een taak is bedoeld voor een aangepaste verzameling, wordt gemaakt onderliggende taken voor elke database die momenteel in een aangepaste verzameling Hallo.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>tooset hello elastische taken voor databaseverbinding
Een verbinding moet toobe set toohello taken *beheer database* voorafgaande toousing Hallo taken API's. Deze cmdlet uitvoert, activeert een referentie venster toopop up aanvragen Hallo-gebruikersnaam en wachtwoord die zijn gemaakt tijdens de installatie van de taken van de elastische Database. Alle voorbeelden in dit onderwerp wordt ervan uitgegaan dat al deze eerste stap is uitgevoerd.

Open een verbinding toohello elastische Database taken:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Versleutelde referenties binnen Hallo-taken voor elastische Database
Databasereferenties kunnen worden ingevoegd in Hallo taken *beheer database* met het wachtwoord dat is versleuteld. Is het nodig toostore referenties tooenable taken toobe uitgevoerd op een later tijdstip (met behulp van de taakschema's).

Versleuteling werkt via een certificaat gemaakt als onderdeel van het script voor installatie Hallo. Hallo installatiescript maakt en uploads Hallo certificaat in hello Azure Cloud Service voor het ontsleutelen van Hallo opgeslagen gecodeerde wachtwoorden. Hello Azure Cloud Service later slaat de openbare sleutel Hallo binnen Hallo taken *beheer database* waardoor Hallo PowerShell API of de klassieke Azure-Portal interface tooencrypt een verstrekte wachtwoord zonder Hallo certificaat toobe lokaal zijn geïnstalleerd.

Hallo referentie wachtwoorden zijn versleuteld en beveiligd van gebruikers met alleen-lezentoegang tooElastic databaseobjecten taken. Maar het is mogelijk dat een kwaadwillende gebruiker met lees-/ schrijftoegang tooElastic Database taken objecten tooextract een wachtwoord. Referenties zijn ontworpen toobe hele taak uitvoeringen gebruikt. Referenties worden tootarget databases doorgegeven bij het tot stand brengen van verbindingen. Er zijn momenteel geen beperkingen op Hallo doeldatabases gebruikt voor elke referentie, kwaadwillende gebruiker kan een database-doel voor een database onder het beheer van Hallo kwaadwillende gebruiker toevoegen. Hallo-gebruiker kan vervolgens een taak die gericht is op deze database toogain Hallo referentie wachtwoord starten.

Aanbevolen beveiligingsprocedures voor elastische Database taken omvatten:

* Informatie over het gebruik van Hallo-API's tootrusted personen wordt beperkt.
* Referenties hebt Hallo minimale bevoegdheden nodig tooperform Hallo-taak.  Meer informatie ziet u binnen dit [autorisatie en machtigingen](https://msdn.microsoft.com/library/bb669084.aspx) SQL Server MSDN-artikel.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate een versleutelde referentie voor het uitvoeren van de taak voor databases
een nieuwe versleuteld toocreate referenties, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) vraagt om een gebruikersnaam en wachtwoord die kan worden doorgegeven toohello [ **nieuw AzureSqlJobCredential cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>tooupdate referenties
Wanneer wachtwoorden wijzigen, gebruikt u Hallo [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) en set Hallo **CredentialName** parameter.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>een elastische Database shard-toewijzing doel toodefine
een taak op alle databases in een set shard tooexecute (gemaakt met behulp van [clientbibliotheek voor elastische Database](sql-database-elastic-database-client-library.md)), een shard-toewijzing met als doel voor Hallo-database gebruiken. Dit voorbeeld vereist een shard-toepassing gemaakt met behulp van Hallo-clientbibliotheek voor elastische Database. Zie [aan de slag met elastische Database extra voorbeeld](sql-database-elastic-scale-get-started.md).

Hallo shard kaart manager-database moet worden ingesteld als het doel van een database en vervolgens Hallo specifieke shard-toewijzing moet worden opgegeven als een doel.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Maken van een T-SQL-Script voor uitvoering tussen databases
Bij het maken van T-SQL-scripts voor de uitvoering van het is raadzaam toobuild ze toobe [idempotent](https://en.wikipedia.org/wiki/Idempotence) en robuuste tegen fouten. Elastische Database-taken opnieuw uitvoeren van het script als een fout optreedt, ongeacht het Hallo-classificatie van Hallo fout wordt aangetroffen die worden uitgevoerd.

Gebruik Hallo [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate en opslaan van een script voor uitvoering en stel Hallo **- ContentName** en **- CommandText**parameters.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Een nieuw script maken vanuit een bestand
Als Hallo T-SQL-script is gedefinieerd in een bestand, moet u dit tooimport Hallo-script gebruiken:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>tooupdate een T-SQL-script voor uitvoering tussen databases
Deze updates PowerShell-script Hallo T-SQL-opdrachttekst voor een bestaand script.

Set Hallo variabelen tooreflect Hallo gewenst script definitie toobe set te volgen:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>tooupdate hello definitie tooan bestaand script
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate een taak tooexecute een script in een shard-toewijzing
Deze PowerShell-script start een taak voor uitvoering van een script dat op elke shard in een elastische Schaalfunctionaliteit van shard-toewijzing.

Set Hallo na variabelen tooreflect Hallo gewenst script en het doel:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>een taak tooexecute
Deze PowerShell-script wordt een bestaande taak uitgevoerd:

Hallo variabele tooreflect Hallo gewenst taak naam toohave uitgevoerd na bijwerken:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>tooretrieve hello status van het uitvoeren van een enkele taak
Gebruik Hallo [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) en set Hallo **JobExecutionId** parameter tooview Hallo status van taak kan worden uitgevoerd.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Gebruik dezelfde Hallo **Get-AzureSqlJobExecution** cmdlet Hello **voor IncludeChildren** namelijk Hallo specifieke status voor elke taak uitvoeren voor elke parameter tooview Hallo status van onderliggende taak uitvoeringen, de database is gericht door Hallo-taak.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>tooview hello staat tussen meerdere taak uitvoeringen
Hallo [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) heeft meerdere optionele parameters die gebruikt toodisplay worden kunnen meerdere taak uitvoeringen, gefilterd via Hallo opgegeven parameters. Hallo hieronder toont een aantal Hallo mogelijke manieren toouse Get-AzureSqlJobExecution:

Alle actieve taken voor de bovenste niveau uitvoeringen ophalen:

    Get-AzureSqlJobExecution

Alle bovenste niveau taak uitvoeringen, met inbegrip van niet-actieve taak uitvoeringen ophalen:

    Get-AzureSqlJobExecution -IncludeInactive

Alle onderliggende taak uitvoeringen van een opgegeven taak uitvoerings-ID, met inbegrip van niet-actieve taak uitvoeringen ophalen:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Ophalen van alle taak uitvoeringen gemaakt met behulp van een planning / taak combinatie, met inbegrip van niet-actieve taken:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Alle taken die gericht is op een opgegeven shard-kaart, inclusief niet-actieve taken worden opgehaald:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Alle taken die gericht is op een opgegeven aangepaste verzameling, met inbegrip van niet-actieve taken worden opgehaald:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Hallo-lijst met taak taak uitvoeringen binnen het uitvoeren van een specifieke taak ophalen:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Taak uitvoeren taakdetails ophalen:

Hallo volgende PowerShell-script kan gebruikte tooview Hallo details van een taak uitvoering van taken, die bijzonder nuttig is bij het opsporen van fouten in uitvoering zijn.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>tooretrieve storingen in taak taak uitvoeringen
Hallo **JobTaskExecution object** bevat een eigenschap voor de levenscyclus van taak samen met een berichteigenschap Hallo Hallo. Als de uitvoering van de taak een taak is mislukt, Hallo lifecycle eigenschap te worden ingesteld*mislukt* en wordt de berichteigenschap Hallo ingesteld resulterende uitzonderingsbericht toohello en de stack. Als een taak is mislukt, is het belangrijk tooview Hallo details van de taken die voor een bepaalde taak is mislukt.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait voor een taak uitvoeren toocomplete
Hallo volgende PowerShell-script kan gebruikte toowait voor een taak taak toocomplete zijn:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

## <a name="create-a-custom-execution-policy"></a>Maken van een aangepaste uitvoeringsbeleid
Elastische Database taken ondersteunt het maken van aangepaste uitvoeringsbeleidsregels die kunnen worden toegepast wanneer u taken start.

Uitvoeringsbeleidsregels toestaan op dit moment voor het definiëren van:

* Naam: Id voor het uitvoeringsbeleid Hallo.
* De time-out van de taak: Totale tijd voordat een taak met elastische taken van de Database, worden geannuleerd.
* Eerste Interval voor opnieuw proberen: Interval toowait voordat de eerste poging.
* Maximale Interval voor opnieuw proberen: Cap van opnieuw intervallen toouse.
* Probeer het opnieuw Interval Backoff Coefficient: Coefficient gebruikt toocalculate Hallo volgende interval tussen nieuwe pogingen.  Hallo volgende formule gebruikt: (eerste Interval voor opnieuw proberen) * Math.pow ((Interval Backoff Coefficient) (nummer van pogingen) - 2). 
* Maximum aantal pogingen: Hallo maximum aantal nieuwe pogingen pogingen tooperform in een job.

Hallo standaarduitvoeringsbeleid Hallo volgende waarden gebruikt:

* Naam: Standaarduitvoeringsbeleid
* De time-out van de taak: 1 week
* Eerste Interval voor opnieuw proberen: 100 milliseconden
* Maximale Interval voor opnieuw proberen: 30 minuten
* Coefficient Interval opnieuw proberen: 2
* Maximum aantal pogingen: 2.147.483.647

Hallo gewenst uitvoeringsbeleid maken:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Een aangepaste uitvoeringsbeleid bijwerken
Hallo gewenst uitvoering beleid tooupdate bijwerken:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Een taak annuleren
Elastische Database taken ondersteunt aanvragen van de annulering van taken.  Als taken voor elastische Database een annuleringsverzoek voor een taak die momenteel wordt uitgevoerd detecteert, wordt geprobeerd toostop Hallo taak.

Er zijn twee verschillende manieren dat elastische Database taken een annulering kan uitvoeren:

1. Annuleren taken momenteel worden uitgevoerd: als een annulering wordt gedetecteerd, terwijl een taak die momenteel wordt uitgevoerd, een annulering wordt geprobeerd binnen Hallo aspect van Hallo taak momenteel wordt uitgevoerd.  Bijvoorbeeld: als er een langdurige query die momenteel wordt uitgevoerd wanneer een annulering wordt uitgevoerd, zal er een poging toocancel Hallo-query.
2. Nieuwe pogingen taak annuleren: als een annulering wordt gedetecteerd door Hallo besturingselement thread voordat een taak voor uitvoering wordt gestart, Hallo besturingselement threads wordt voorkomen Hallo taak starten en Hallo aanvraag declareren als geannuleerd.

Als een taak annulering is aangevraagd voor een bovenliggende taak, wordt Hallo annuleringsverzoek ingewilligd voor Hallo bovenliggende taak en alle bijbehorende onderliggende taken.

toosubmit een annuleringsverzoek gebruiken Hallo [ **cmdlet Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) en set Hallo **JobExecutionId** parameter.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>een taak toodelete en Taakgeschiedenis asynchroon
Elastische taken van de Database biedt ondersteuning voor asynchrone verwijderen van jobs. Een taak kan worden gemarkeerd voor verwijdering en Hallo system Hallo taak en de taakgeschiedenis wordt verwijderd nadat alle taak uitvoeringen voor Hallo taak hebt voltooid. Hallo-systeem wordt niet automatisch uitvoeringen van de actieve taak geannuleerd.  

Aanroepen [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel actieve taak uitvoeringen.

tootrigger taak verwijderen, gebruik Hallo [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) en set Hallo **JobName** parameter.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>het doel van een aangepaste database toocreate
U kunt aangepaste database doelen voor directe uitvoering of voor insluiting in een aangepaste database wilt definiëren. Bijvoorbeeld, omdat **elastische pools** zijn nog niet rechtstreeks ondersteund met behulp van PowerShell APIs, kunt u een aangepaste database doel en de aangepaste database verzameling doel op die alle Hallo-databases in de groep Hallo omvat.

Hallo variabelen tooreflect Hallo gewenst databasegegevens volgende instellen:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>een verzameling aangepaste database doel toocreate
Gebruik Hallo [ **nieuw AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet toodefine een aangepaste database verzameling doel tooenable uitvoering tussen meerdere gedefinieerde database doelen. Na het maken van een databasegroep, kunnen de databases worden gekoppeld aan Hallo aangepaste verzameling doel.

Stel Hallo variabelen tooreflect Hallo gewenste aangepaste verzameling doelconfiguratie te volgen:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>tooadd databases tooa aangepaste database verzameling doel
een database tooa specifieke aangepaste verzameling tooadd gebruiken Hallo [ **toevoegen AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Hallo-databases binnen een doel van de verzameling aangepaste database controleren
Gebruik Hallo [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet tooretrieve Hallo onderliggende databases binnen een doel van de verzameling aangepaste database. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Een taak tooexecute van een script voor een doel van de verzameling aangepaste database maken
Gebruik Hallo [ **nieuw AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) cmdlet toocreate een taak op basis van een groep met databases die zijn gedefinieerd door een doel van de verzameling aangepaste database. Elastische taken van de Database wordt Hallo taak uitbreiden naar meerdere onderliggende taken elke overeenkomstige tooa-database die is gekoppeld aan Hallo aangepaste database verzameling doel en zorg ervoor dat Hallo script wordt uitgevoerd tegen elke database. Ook is het belangrijk dat scripts idempotent toobe robuuste tooretries zijn.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Gegevens verzamelen over databases
U kunt een taak tooexecute een query gebruiken in een groep met databases en Hallo resultaten tooa specifieke tabel verzenden. Hallo tabel kan worden opgevraagd na Hallo feit toosee Hallo queryresultaat van elke database. Dit biedt een asynchrone methode tooexecute een query tussen meerdere databases. Mislukte pogingen worden automatisch verwerkt via de nieuwe pogingen.

de opgegeven doeltabel Hallo worden automatisch gemaakt als deze nog niet bestaat. de nieuwe tabel Hallo komt overeen met schema Hallo Hallo heeft een resultatenset geretourneerd. Als meerdere resultatensets worden geretourneerd door een script, verzendt elastische Database taken alleen Hallo eerste toohello doeltabel.

Hallo volgende PowerShell-script een script wordt uitgevoerd en verzamelt de resultaten in een opgegeven tabel. Dit script wordt ervan uitgegaan dat een T-SQL-script is gemaakt waarmee een enkelvoudig resultaat wordt verkregen set levert en dat er een doel van de verzameling aangepaste database is gemaakt.

Dit script maakt gebruik van Hallo [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet. Hallo parameters instellen voor script, referenties en uitvoering van doel:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate en start een taak voor scenario's voor het verzamelen van gegevens
Dit script maakt gebruik van Hallo [ **Start AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>een taak uitvoeren trigger tooschedule
Hallo volgende PowerShell-script kan worden gebruikt toocreate een terugkerend schema. Dit script maakt gebruik van een minuut interval maar [ **nieuw AzureSqlJobSchedule** ](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) biedt ook ondersteuning voor parameters - DayInterval, - HourInterval, - MonthInterval, en -WeekInterval. Schema's die slechts één keer worden uitgevoerd, kunnen worden gemaakt door doorgeven - eenmalige.

Maak een nieuwe planning:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>een taak uitgevoerd op een tijdschema tootrigger
Een trigger voor de taak kan worden gedefinieerd toohave uitgevoerd volgens tooa tijdschema van een taak. Hallo volgende PowerShell-script kan worden gebruikt toocreate een trigger taak.

Gebruik [nieuw AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) en set Hallo variabelen toocorrespond toohello gewenste taak en planning:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove een geplande koppeling toostop taak wordt uitgevoerd volgens schema
toodiscontinue taakuitvoering via een taak worden geactiveerd, Hallo taak trigger opnieuw optreedt, kan worden verwijderd. Verwijderen van een taak trigger toostop een taak uit te voeren volgens tooa schema met behulp van Hallo [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Triggers gebonden tooa tijd taakschema ophalen
Hallo volgende PowerShell-script kan worden gebruikt tooobtain en Hallo taak triggers geregistreerde tooa bepaald tijdschema weergeven.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>tooretrieve taak triggers gebonden tooa taak
Gebruik [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain en weergave van schema's met een geregistreerde taak.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>een toepassing-gegevenslaagtoepassingen (DACPAC) voor uitvoering tussen databases toocreate
Zie een DACPAC toocreate [Data-Tier applications](https://msdn.microsoft.com/library/ee210546.aspx). een DACPAC toodeploy gebruiken Hallo [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Hallo DACPAC moet toegankelijk toohello service. Het is aanbevolen tooupload een gemaakte DACPAC tooAzure opslag en maak een [Shared Access Signature](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor Hallo DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>een toepassing-gegevenslaagtoepassingen (DACPAC) voor uitvoering tussen databases tooupdate
Bestaande DACPACs geregistreerd binnen een elastische Database taken kunnen worden bijgewerkt toopoint toonew URI's. Gebruik Hallo [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate hello DACPAC URI op een bestaande DACPAC geregistreerd:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>een taak tooapply een toepassing-gegevenslaagtoepassingen (DACPAC) voor databases toocreate
Nadat een DACPAC binnen elastische taken van de Database is gemaakt, kan een taak kan tooapply hello DACPAC in een groep met databases worden gemaakt. Hallo volgende PowerShell-script kan gebruikte toocreate een taak DACPAC via een aangepaste verzameling van databases zijn:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
