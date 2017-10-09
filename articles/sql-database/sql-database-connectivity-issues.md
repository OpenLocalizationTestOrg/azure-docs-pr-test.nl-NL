---
title: aaaFix is een verbindingsfout SQL tijdelijke fout | Microsoft Docs
description: 'Ontdek hoe tootroubleshoot, onderzoeken en te voorkomen dat een SQL-fout of een tijdelijke fout in Azure SQL Database. '
keywords: SQL-verbinding, verbindingsreeks, problemen met de netwerkverbinding, tijdelijke fout, is een verbindingsfout
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a>Oplossen, opsporen en voorkomen van SQL-verbindingsfouten en tijdelijke fouten voor SQL-database
Dit artikel wordt beschreven hoe tooprevent, oplossen, analyseren en beperken van verbindingsfouten en tijdelijke fouten die uw clienttoepassing tegenkomt wanneer deze met Azure SQL Database samenwerkt. Informatie over hoe tooconfigure Pogingslogica, Hallo-verbindingsreeks en andere instellingen aanpassen.

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a>Tijdelijke fouten (tijdelijke fouten)
Een tijdelijke fout - ook tijdelijke fout - heeft een oorzaak die wordt binnenkort automatisch opgelost. Een incidentele oorzaak van tijdelijke fouten is wanneer hello Azure systeem snel hardware resources toobetter verdelen verschillende workloads verschuift. De meeste van deze gebeurtenissen herconfiguratie vaak voltooid in minder dan 60 seconden. Tijdens deze tijdsspanne herconfiguratie wellicht hebt u connectiviteit problemen tooAzure SQL-Database. Toepassingen verbinding tooAzure SQL-Database moet worden opgebouwd tooexpect deze tijdelijke fouten ingang ze door het implementeren van Pogingslogica in de code in plaats van ze toousers als toepassingsfouten halen.

Als uw clientprogramma ADO.NET, het programma is adviseert over tijdelijke fout Hallo Hallo throw van een **SqlException**. Hallo **getal** eigenschap kan worden vergeleken op basis van de lijst Hallo van tijdelijke fouten aan de bovenkant Hallo van Hallo onderwerp: [SQL-foutcodes voor SQL-Database-clienttoepassingen](sql-database-develop-error-messages.md).

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>De verbinding ten opzichte van de opdracht
U kunt opnieuw proberen Hallo SQL-verbinding of opnieuw instellen, afhankelijk van de volgende Hallo:

* **Een tijdelijke fout optreedt tijdens een verbindingspoging**: Hallo verbinding moet opnieuw worden geprobeerd na enkele seconden vertraagd.
* **Een tijdelijke fout optreedt tijdens de opdracht van een SQL-query**: Hallo-opdracht moet niet onmiddellijk opnieuw uitgevoerd. In plaats daarvan na een vertraging Hallo verbinding moet worden opnieuw worden gemaakt. Vervolgens Hallo-opdracht kan opnieuw worden geprobeerd.

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a>Pogingslogica voor tijdelijke problemen
Client-programma's die soms treedt er een tijdelijke fout zijn krachtiger wanneer ze Pogingslogica bevatten.

Wanneer uw programma met Azure SQL Database via een 3e partij middleware communiceert, informeren met Hallo leverancier of Hallo middleware Pogingslogica voor tijdelijke fouten bevat.

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a>Principes voor een nieuwe poging
* Een poging tooopen een verbinding moet opnieuw worden geprobeerd, als tijdelijke Hallo-fout.
* Een SQL SELECT-instructie is mislukt met een tijdelijke fout moet niet opnieuw worden geprobeerd rechtstreeks.
  
  * In plaats daarvan een nieuwe verbinding tot stand brengen en probeer vervolgens Hallo selecteren.
* Wanneer een UPDATE van SQL-instructie is mislukt met een tijdelijke fout, moet een nieuwe verbinding worden gemaakt voordat Hallo die update wordt herhaald.
  
  * Hallo Pogingslogica moet ervoor zorgen dat Hallo gehele databasetransactie is voltooid of dat Hallo hele transactie wordt teruggedraaid.

#### <a name="other-considerations-for-retry"></a>Andere overwegingen voor een nieuwe poging
* Een batch-programma die automatisch wordt gestart nadat de werkuren en die wordt voltooid voordat de ochtend betaalbare toovery geduld met lange tijdsintervallen tussen de nieuwe pogingen.
* Een gebruikersinterfaceprogramma moet rekening houden met Hallo menselijke neiging toogive up na een wachttijd te lang.
  
  * Echter mag Hallo oplossing geen tooretry paar seconden, omdat dit beleid Hallo-systeem met aanvragen overspoelen kunt.

#### <a name="interval-increase-between-retries"></a>Verhoging van het interval tussen nieuwe pogingen
Het is raadzaam om u te stellen voor 5 seconden voordat de eerste poging. Probeert het opnieuw nadat een korter is dan 5 seconden vertraging risico's overweldigend Hallo-cloudservice. Voor elke opeenvolgende pogingen Hallo vertraging moet worden uitgebreid exponentieel, up tooa maximaal 60 seconden.

Een beschrijving van de Hallo *blokkerende periode* voor clients die gebruikmaken van ADO.NET is beschikbaar in [SQL Server-verbinding groeperen (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

U kunt ook het maximale aantal nieuwe pogingen tooset voordat Hallo programma zelf wordt beëindigd.

#### <a name="code-samples-with-retry-logic"></a>Codevoorbeelden met Pogingslogica
Codevoorbeelden met Pogingslogica in diverse programmeertalen, zijn beschikbaar op:

* [Verbindingsbibliotheken voor SQL-Database en SQL Server](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a>Uw Pogingslogica testen
tootest uw Pogingslogica heeft, moet u simuleren of een fout veroorzaken, dan kan worden gecorrigeerd terwijl uw programma nog steeds actief is.

##### <a name="test-by-disconnecting-from-hello-network"></a>Testen door Hallo netwerk verbreekt
Een manier die u kunt uw Pogingslogica testen is toodisconnect uw clientcomputer vanuit Hallo netwerk terwijl Hallo programma wordt uitgevoerd. Hallo-fout is:

* **SqlException.Number** 11001 =
* Bericht: "Er is geen host is onbekend'

Als onderdeel van Hallo proberen eerst poging, kan uw programma Hallo onjuist gespeld corrigeren en vervolgens probeert tooconnect.

Dit praktische toomake, u de computer vanaf het netwerk Hallo loskoppelen voordat u uw programma. Het programma herkent vervolgens een runtime-parameter die ervoor zorgt Hallo dat:

1. 11001 tooits lijst met fouten tooconsider tijdelijk toevoegen als tijdelijk.
2. De eerste verbinding gewoon proberen.
3. Nadat het Hallo-fout is opgetreden, verwijdert u 11001 uit Hallo-lijst.
4. Een bericht Hallo gebruiker tooplug Hallo computer aan op Hallo netwerk weergeven.
   * Verder kan worden uitgevoerd met behulp van beide Hallo onderbreken **Console.ReadLine** methode of een dialoogvenster met de knop OK. Hallo-gebruiker op Hallo Enter-toets drukt nadat Hallo computer op Hallo-netwerk aangesloten.
5. Probeer opnieuw tooconnect, succes verwacht.

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a>Testen door onjuist gespeld Hallo databasenaam op om verbinding te maken
Het programma kan Hallo gebruikersnaam voordat de eerste verbindingspoging Hallo opzettelijk Maak een typefout. Hallo-fout is:

* **SqlException.Number** 18456 =
* Bericht: 'aanmelding is mislukt voor gebruiker 'WRONG_MyUserName'.'

Als onderdeel van Hallo proberen eerst poging, kan uw programma Hallo onjuist gespeld corrigeren en vervolgens probeert tooconnect.

Dit praktische toomake, het programma kan een runtime-parameter die ervoor zorgt Hallo dat herkend:

1. Tijdelijk 18456 tooits lijst met fouten tooconsider toevoegen als tijdelijk.
2. De naam van de gebruiker toohello 'WRONG_' opzettelijk toevoegen.
3. Nadat het Hallo-fout is opgetreden, verwijdert u 18456 uit Hallo-lijst.
4. 'WRONG_' uit de gebruikersnaam Hallo verwijderen.
5. Probeer opnieuw tooconnect, succes verwacht.

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a>.NET-SqlConnection parameters voor een nieuwe poging verbinding
Als uw clientprogramma tootooAzure SQL-Database verbindt met behulp van .NET Framework-klasse Hallo **System.Data.SqlClient.SqlConnection**, moet u .NET 4.6.1 of hoger (of .NET Core) zodat u van de functie van de verbinding opnieuw gebruikmaken kunt. Details van de functie Hallo zijn [hier](http://go.microsoft.com/fwlink/?linkid=393996).

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


Wanneer u Hallo bouwen [verbindingsreeks](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) voor uw **SqlConnection** object, moet u waarden tussen de volgende parameters Hallo Hallo coördineren:

* ConnectRetryCount &nbsp; &nbsp; *(de standaardwaarde is 1. Bereik is 0 tot en met 255.)*
* ConnectRetryInterval &nbsp; &nbsp; *(de standaardwaarde is 1 seconde. Bereik is 1 tot en met 60).*
* Verbindingstime-out &nbsp; &nbsp; *(de standaardwaarde is 15 seconden. Bereik is 0 tot 2147483647)*

Uw gekozen waarden moet in het bijzonder Hallo gelijkheid waar te volgen:

* Verbindingstime-out ConnectRetryCount = * ConnectionRetryInterval

Bijvoorbeeld, als hello tellen = 3, en interval = 10 seconden, een time-out van alleen 29 seconden niet erg Hallo systeem voldoende tijd voor de 3e en final opnieuw op verbinding te maken krijgt: 29 < 3 * 10.

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a>De verbinding ten opzichte van de opdracht
Hallo **ConnectRetryCount** en **ConnectRetryInterval** parameters, kunnen uw **SqlConnection** object opnieuw Hallo verbindingsbewerking zonder ontvangt of proberen alles uit uw programma, zoals tooyour besturingsprogramma retourneren. Hallo pogingen kunnen in Hallo volgende situaties optreden:

* de methodeaanroep mySqlConnection.Open
* de methodeaanroep mySqlConnection.Execute

Er is een geldt de volgende werkwijze. Als een tijdelijke fout optreedt terwijl uw *query* wordt uitgevoerd, uw **SqlConnection** -object heeft geen nieuwe poging Hallo verbindingsbewerking deze gewoon probeert niet opnieuw uw query. Echter, **SqlConnection** zeer snel controles Hallo verbinding voordat de query voor uitvoering worden verzonden. Als Hallo snelle controle een verbindingsprobleem detecteert **SqlConnection** verbindingsbewerking Hallo voor nieuwe pogingen. Als Hallo nieuwe poging is gelukt, wordt u query verzonden voor uitvoering.

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a>Moet ConnectRetryCount worden gecombineerd met toepassingslogica opnieuw proberen?
Stel dat uw toepassing robuuste aangepaste Pogingslogica. Dit mogelijk opnieuw Hallo verbindingsbewerking 4 keer. Als u **ConnectRetryInterval** en **ConnectRetryCount** = 3 tooyour verbindingsreeks, verhoogt u Hallo opnieuw aantal too4 * 3 = 12 opnieuw probeert. U kunt niet van plan bent een groot aantal pogingen.

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a>Verbindingen tooAzure SQL-Database
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a>Verbinding: De verbindingsreeks
Hallo-verbindingsreeks nodig voor het verbinden van tooAzure SQL-Database is enigszins afwijken van het Hallo-tekenreeks voor het verbinden van tooMicrosoft SQL Server. U kunt Hallo-verbindingsreeks voor uw database kopiëren van Hallo [Azure-portal](https://portal.azure.com/).

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a>Verbinding: IP-adres
U moet Hallo SQL-Database tooaccept servercommunicatie van Hallo IP-adres van Hallo-computer die als host fungeert voor uw clientprogramma configureren. U dit doen door de firewall-instellingen via Hallo Hallo bewerken [Azure-portal](https://portal.azure.com/).

Als u tooconfigure Hallo IP-adres vergeet, mislukt het programma met een handige foutbericht dat Hallo vereiste IP-adres aangeeft.

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

Zie voor meer informatie: [procedure: firewall-instellingen configureren op de SQL-Database](sql-database-configure-firewall-settings.md)

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a>Verbinding: poorten
Normaal gesproken hoeft u alleen tooensure dat poort 1433 is geopend voor uitgaande communicatie, op Hallo-computer waarop u clientprogramma wordt gehost.

Bijvoorbeeld, wanneer uw clientprogramma wordt gehost op een Windows-computer, kunt Hallo Windows Firewall op Hallo host u tooopen poort 1433:

1. Hallo Configuratiescherm openen
2. &gt;Alle Configuratiescherm-onderdelen
3. &gt;Windows Firewall
4. &gt;Geavanceerde instellingen
5. &gt;Regels voor uitgaande verbindingen
6. &gt;Acties
7. &gt;Nieuwe regel

Als wordt uw clientprogramma wordt gehost in Azure een virtuele machine (VM), dient u te lezen:<br/>[Poorten buiten 1433 voor ADO.NET 4.5 en SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).

Zie voor achtergrondinformatie over cofiguration van poorten en IP-adres: [Azure SQL Database-firewall](sql-database-firewall-configure.md)

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a>Verbinding: ADO.NET 4.6.1
Als het programma wordt gebruikt voor klassen als ADO.NET **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL-Database, het is raadzaam dat u .NET Framework versie 4.6.1 of hoger.

ADO.NET 4.6.1:

* Voor Azure SQL Database zich verbeterde betrouwbaarheid wanneer u een verbinding openen met behulp van Hallo **SqlConnection.Open** methode. Hallo **Open** methode bevat nu best effort opnieuw mechanismen antwoord tootransient fouten, voor bepaalde fouten binnen Hallo verbinding time-outperiode.
* Ondersteunt Groepsgewijze verbinding nodig. Dit omvat een doeltreffende controle verbinding Hallo object geeft uw programma werkt.

Wanneer u een verbindingsobject van een verbindingsgroep gebruikt, wordt u aangeraden dat uw programma Hallo verbinding tijdelijk sluiten wanneer deze niet direct gebruikt. Opnieuw een verbinding te openen, is geen dure Hallo manier voor het maken van een nieuwe verbinding is.

Als u van ADO.NET 4.0 gebruikmaakt of eerder wordt aangeraden dat u een upgrade toohello uitvoert nieuwste ADO.NET.

* U kunt vanaf November 2015 [downloaden ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a>Diagnostiek
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a>Diagnostische gegevens: Testen of hulpprogramma's verbinding kunnen maken
Als het programma niet tooconnect tooAzure SQL-Database, is een optie om diagnostische tootry tooconnect met een hulpprogramma's. In het ideale geval Hallo hulpprogramma verbinding te maken met behulp van Hallo dezelfde bibliotheek dat het programma gebruikt.

Op elke Windows-computer probeert u deze hulpprogramma's:

* SQL Server Management Studio (ssms.exe) die is verbonden met ADO.NET.
* Sqlcmd.exe die verbinding met behulp van maakt [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).

Eenmaal zijn verbonden, test u of een korte SQL SELECT-query werkt.

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a>Diagnostische gegevens: Open poorten Hallo controleren
Stel dat u vermoedt dat verbindingspogingen vanwege tooport problemen mislukken. U kunt een hulpprogramma waarmee u over Hallo poortconfiguraties rapporten uitvoeren op uw computer.

Op Linux Hallo volgende hulpprogramma's mogelijk nuttig zijn:

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * (Hallo voorbeeld waarde toobe uw IP-adres wijzigen.)

Op Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) hulpprogramma kan handig zijn. Hier volgt een voorbeeld van de uitvoering die Hallo poort situatie op een Azure SQL Database-server een query uitgevoerd en die is uitgevoerd op een laptopcomputer:

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a>Diagnostische gegevens: Uw fouten in logboek registreren
Er is een onregelmatig probleem wordt soms beste gediagnosticeerd door detectie van een algemene patroon gedurende dagen of weken.

De client kan helpen bij het een diagnose door logboekregistratie van alle fouten die worden aangetroffen. U kunt toocorrelate Hallo logboekvermeldingen met foutgegevens met Azure SQL Database intern zichzelf registreert mogelijk.

Enterprise-bibliotheek 6 (EntLib60) biedt beheerde klassen tooassist met logboekregistratie:

* [5 - als gemakkelijk als vallen buiten een logboek: met behulp van Hallo Logging Application Block](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a>Diagnostische gegevens: Raadpleeg het systeemlogboek in Logboeken op fouten
Hier volgen enkele Transact-SQL SELECT-instructies die querylogboeken van de fout en andere informatie.

| Query van het logboek | Beschrijving |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |Hallo [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) weergave biedt informatie over afzonderlijke gebeurtenissen, inclusief een aantal die leiden tijdelijke fouten of verbindingsproblemen tot kunnen.<br/><br/>In het ideale geval correleren van Hallo **start_time** of **end_time** waarden met informatie over wanneer uw clientprogramma problemen ondervonden.<br/><br/>**TIP:** moet u verbinding maken met toohello **master** toorun deze database. |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |Hallo [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) weergave biedt cumulatief aantal gebeurtenistypen, voor aanvullende diagnostische gegevens.<br/><br/>**TIP:** moet u verbinding maken met toohello **master** toorun deze database. |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a>Diagnostische gegevens: Zoek naar gebeurtenissen in het SQL-databaselogboek Hallo probleem
U kunt zoeken naar vermeldingen over probleem gebeurtenissen in Hallo van Azure SQL Database. Probeer het volgende Transact-SQL SELECT-instructie in Hallo Hallo **master** database:

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a>Enkele geretourneerde rijen uit sys.fn_xe_telemetry_blob_target_read_file
Hierna volgt wat een geretourneerde rij als volgt uitzien. Hallo null-waarden weergegeven zijn vaak niet null zijn in andere rijen.

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a>Enterprise-bibliotheek 6
Enterprise-bibliotheek 6 (EntLib60) is een raamwerk van .NET-klassen waarmee u robuuste clients van cloud-services te implementeren waarbij een van de hello Azure SQL Database-service is. U kunt speciale tooeach gebied van onderwerpen waarin EntLib60 in eerste via helpen kan zoeken:

* [Enterprise-bibliotheek 6 April 2013](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

Pogingslogica voor tijdelijke foutafhandeling is een gebied waarin EntLib60 kan helpen:

* [4 - perseverance, geheim van alle successen: met behulp van Hallo tijdelijke fout afhandeling van Application Block](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> Hallo broncode voor EntLib60 is beschikbaar voor openbare [downloaden](http://go.microsoft.com/fwlink/p/?LinkID=290898). Microsoft heeft geen plannen toomake verdere functie-updates of onderhoud tooEntLib bijgewerkt.
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a>EntLib60 klassen voor tijdelijke fouten en probeer het opnieuw
Hallo na EntLib60 klassen zijn bijzonder nuttig voor Pogingslogica. Alle deze in, of zijn onder meer naamruimte Hallo **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:

*In de naamruimte Hallo **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*

* **Het RetryPolicy** klasse
  
  * **ExecuteAction** methode
* **ExponentialBackoff** klasse
* **SqlDatabaseTransientErrorDetectionStrategy** klasse
* **ReliableSqlConnection** klasse
  
  * **ExecuteCommand** methode

In de naamruimte Hallo **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:

* **AlwaysTransientErrorDetectionStrategy** klasse
* **NeverTransientErrorDetectionStrategy** klasse

Hier vindt u koppelingen tooinformation over EntLib60:

* Gratis [adresboek downloaden: Developer's Guide tooMicrosoft Enterprise-bibliotheek, 2e Edition](http://www.microsoft.com/download/details.aspx?id=41145)
* Aanbevolen procedures: [Probeer algemene richtlijnen](../best-practices-retry-general.md) is een uitstekende gedetailleerdere beschrijving van Pogingslogica.
* Downloaden van NuGet [Enterprise Library - toepassing blok 6.0 afhandeling van tijdelijke fout](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a>EntLib60: Hallo logboekregistratie blokkeren
* Hallo logboekregistratie blok is een zeer flexibele en configureerbare oplossing waarmee u kunt:
  
  * Maak en logboekberichten opslaan in een groot aantal verschillende locaties.
  * Categoriseren en berichten filteren.
  * Contextuele informatie verzameld die handig voor foutopsporing en tracering, evenals voor controle en algemene logboekregistratie vereisten.
* Hallo logboekregistratie blok isoleert Hallo functionaliteit logboekregistratie van Hallo logboekbestemming zodat Hallo toepassingscode consistent, ongeacht het Hallo-locatie en het type van Hallo doel logboekregistratie store.

Zie voor meer informatie: [5 - als gemakkelijk als vallen buiten een logboek: met behulp van Hallo Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a>EntLib60 IsTransient methode broncode
Vervolgens Hallo **SqlDatabaseTransientErrorDetectionStrategy** klasse, Hallo C#-broncode voor Hallo **IsTransient** methode. Hallo-broncode wordt uitleg gegeven over welke fouten zijn beschouwd als tijdelijke toobe en leveringsopties opnieuw vanaf April 2013.

Talrijke **//comment** regels zijn verwijderd uit deze kopie tooemphasize leesbaarheid.

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a>Volgende stappen
* Voor het oplossen van andere veelvoorkomende verbindingsproblemen van Azure SQL Database, gaat u naar [oplossen verbinding problemen tooAzure SQL-Database](sql-database-troubleshoot-common-connection-issues.md).
* [SQL Server-verbinding (ADO.NET) groeperen](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [*Opnieuw proberen* is een Apache 2.0 in licentie gegeven algemene bibliotheek, geschreven in opnieuw **Python**, toosimplify Hallo taak opnieuw gedrag toojust over iets toe te voegen.](https://pypi.python.org/pypi/retrying)

