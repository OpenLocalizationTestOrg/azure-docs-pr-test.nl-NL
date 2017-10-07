---
title: foutcodes aaaSQL - fout in databaseverbinding | Microsoft Docs
description: "Meer informatie over SQL-foutcodes voor SQL-Database-clienttoepassingen, zoals algemene databasefouten verbinding met de database kopiëren en algemene fouten. "
keywords: SQL-foutcode, toegang tot sql, fout in databaseverbinding, sql-foutcodes
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 2a23e4ca-ea93-4990-855a-1f9f05548202
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 683a7d72c935742f3f9f9a0c683e5d8161167d6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-error-codes-for-sql-database-client-applications-database-connection-error-and-other-issues"></a>SQL-foutcodes voor SQL-Database-clienttoepassingen: databaseverbindingsfout en andere problemen
<!--
Old Title on MSDN:  Error Messages (Azure SQL Database)
ShortId on MSDN:  ff394106.aspx
Dx 4cff491e-9359-4454-bd7c-fb72c4c452ca
-->


Dit artikel bevat een overzicht van de SQL-foutcodes voor SQL-Database-clienttoepassingen, waaronder verbinding databasefouten, tijdelijke fouten (ook wel tijdelijke fouten), resource governance fouten, problemen met de database kopiëren, elastische pool en andere fouten. De meeste categorieën zijn bepaalde tooAzure SQL-Database en tooMicrosoft SQL Server zijn niet van toepassing.

## <a name="database-connection-errors-transient-errors-and-other-temporary-errors"></a>Database-verbindingsfouten en tijdelijke fouten andere tijdelijke fouten
Hallo volgende tabel bevat informatie over Hallo SQL-foutcodes voor verbindingsfouten gegevensverlies en andere tijdelijke fouten die mogelijk optreden wanneer uw toepassing tooaccess SQL-Database probeert. Voor het ophalen van gestarte zelfstudies over het tooconnect tooAzure SQL-Database, Zie [verbinding maken met SQL-Database tooAzure](sql-database-libraries.md).

### <a name="most-common-database-connection-errors-and-transient-fault-errors"></a>Meest voorkomende fouten in database-verbinding en tijdelijke fout
Hello Azure-infrastructuur heeft Hallo mogelijkheid toodynamically servers configureren wanneer zware workloads in Hallo SQL Database-service optreden.  Dit dynamische gedrag kan ertoe leiden dat uw client programma toolose de verbinding tooSQL Database. Dit type fout heet een *tijdelijke fout*.

Het is raadzaam dat uw clientprogramma Pogingslogica heeft zodat deze kan opnieuw verbinding te maken nadat u Hallo tijdelijke fout tijd toocorrect zelf hebt.  Het is raadzaam om u te stellen voor 5 seconden voordat de eerste poging. Probeert het opnieuw nadat een korter is dan 5 seconden vertraging risico's overweldigend Hallo-cloudservice. Voor elke opeenvolgende pogingen Hallo vertraging moet worden uitgebreid exponentieel, up tooa maximaal 60 seconden.

Tijdelijke fout fouten manifest doorgaans als een van de volgende foutberichten van uw client-programma's Hallo:

* Database &lt;db_name&gt; op server &lt;Azure_instance&gt; is momenteel niet beschikbaar. Probeer het later opnieuw verbinding Hallo. Als Hallo probleem zich blijft voordoen, neem contact op met klantenondersteuning en geeft u Hallo sessietracering-ID &lt;session_id&gt;
* Database &lt;db_name&gt; op server &lt;Azure_instance&gt; is momenteel niet beschikbaar. Probeer het later opnieuw verbinding Hallo. Als Hallo probleem zich blijft voordoen, neem contact op met klantenondersteuning en geeft u Hallo sessietracering-ID &lt;session_id&gt;. (Microsoft SQL Server, fout: 40613)
* Een bestaande verbinding is verbroken door de externe host Hallo.
* System.Data.Entity.Core.EntityCommandExecutionException: Er is een fout opgetreden tijdens het uitvoeren van de opdrachtdefinitie Hallo. Zie Hallo binnenste uitzondering voor meer informatie. ---> System.Data.SqlClient.SqlException: Er is een fout transportniveau opgetreden tijdens het ontvangen van resultaten van Hallo-server. (provider: sessieprovider, fout: 19 - fysieke verbinding is niet bruikbaar)
* Een verbinding poging tooa secundaire database is mislukt omdat het Hallo-database is in proces Hallo van reconfguration en is bezig nieuwe pagina's tijdens het in het midden van een actieve line transactie Hallo toepassen op de primaire database Hallo. 

Zie voor voorbeelden van de programmacode van Pogingslogica:

* [Verbindingsbibliotheken voor SQL-Database en SQL Server](sql-database-libraries.md) 
* [Acties toofix verbindingsfouten en tijdelijke fouten in SQL-Database](sql-database-connectivity-issues.md)

Een beschrijving van de Hallo *blokkerende periode* voor clients die gebruikmaken van ADO.NET is beschikbaar in [SQL Server-verbinding groeperen (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).

### <a name="transient-fault-error-codes"></a>Foutcodes voor tijdelijke fout
Hallo volgende fouten zijn tijdelijk en moeten opnieuw worden geprobeerd in toepassingslogica 

| Foutcode | Ernst | Beschrijving |
| ---:| ---:|:--- |
| 4060 |16 |Kan database niet openen '%. & #x2a; ls' aangevraagd door de Hallo aanmelding. Hallo-aanmelding is mislukt. |
| 40197 |17 |Hallo-service heeft een fout bij het verwerken van uw aanvraag aangetroffen. Probeer het opnieuw. Foutcode: %d.<br/><br/>U ontvangt deze fout, wanneer het Hallo-service is niet actief vanwege toosoftware of hardware-upgrades, hardwarefouten of andere problemen met betrekking tot failover. Hallo-foutcode (%d) die zijn ingesloten in het Hallo-bericht van fout 40197 bevat aanvullende informatie over Hallo type fout of failover die is opgetreden. Enkele voorbeelden van Hallo fout codes zijn ingesloten in het Hallo-bericht van fout 40197 zijn 40020, 40143 40166 en 40540.<br/><br/>Herstellen van verbindingen tooyour SQL Database-server wordt u automatisch tooa orde kopie van uw database verbinding. Uw toepassing moet catch-fout 40197, logboek Hallo ingesloten foutcode (%d) in voor het oplossen van het Hallo-bericht en probeer opnieuw verbinding te maken tooSQL Database totdat Hallo bronnen beschikbaar zijn en de verbinding tot stand is gebracht opnieuw. |
| 40501 |20 |Hallo-service is momenteel bezet. Hallo aanvraag opnieuw proberen na tien seconden. Incident-ID: %ls. Code: %d.<br/><br/>*Opmerking:* Zie voor meer informatie:<br/>• [Limieten voor azure SQL Database](sql-database-resource-limits.md). |
| 40613 |17 |Database '%. & #x2a; ls' op server '%. & #x2a; ls' is momenteel niet beschikbaar. Probeer het later opnieuw verbinding Hallo. Als Hallo probleem zich blijft voordoen, neem contact op met klantenondersteuning en geeft u Hallo sessietracering-ID '%. & #x2a; ls'. |
| 49918 |16 |Kan aanvraag niet verwerken. De aanvraag tooprocess onvoldoende resources.<br/><br/>Hallo-service is momenteel bezet. Probeer het Hallo-aanvraag later opnieuw. |
| 49919 |16 |Proces kan geen aanvraag maken of bijwerken. Te veel bewerkingen maken of bijwerken uitgevoerd voor abonnement ' % ld '.<br/><br/>Hallo-service is bezet verwerking van meerdere maken of bijwerken van aanvragen voor uw abonnement of de server. Aanvragen die momenteel is geblokkeerd voor optimalisatie van de resource. Query [sys.dm_operation_status bevat](https://msdn.microsoft.com/library/dn270022.aspx) voor bewerkingen die in behandeling. Wacht tot de in behandeling zijnde maken of bijwerken aanvragen zijn voltooid of verwijder een van de in behandeling genomen aanvragen en uw aanvraag later opnieuw. |
| 49920 |16 |Kan aanvraag niet verwerken. Te veel bewerkingen uitgevoerd voor abonnement ' % ld '.<br/><br/>Hallo-service is bezig met de verwerking van meerdere aanvragen voor dit abonnement. Aanvragen die momenteel is geblokkeerd voor optimalisatie van de resource. Query [sys.dm_operation_status bevat](https://msdn.microsoft.com/library/dn270022.aspx) voor de bewerkingsstatus van de. Wacht totdat aanvragen in behandeling zijn voltooid of verwijder een van de in behandeling zijnde aanvragen en uw aanvraag later opnieuw. |
| 4221 |16 |Aanmelding tooread-secundaire is mislukt vanwege toolong wachten op 'HADR_DATABASE_WAIT_FOR_TRANSITION_TO_VERSIONING'. Hallo-replica is niet beschikbaar voor aanmelding, omdat de versies van de rij ontbreken voor transacties die onderweg zijn als Hallo replica werd opnieuw gebruikt. Hallo probleem kan worden opgelost door terugdraaien of actieve transacties op de primaire replica Hallo Hallo doorvoeren. Instanties van dit probleem kunnen worden geminimaliseerd door te lang schrijftransacties op Hallo primaire vermijden. |

## <a name="database-copy-errors"></a>Fouten in de database kopiëren
Hallo volgende fouten kan opgetreden bij het kopiëren van een database in Azure SQL Database. Zie [Een Azure SQL Database kopiëren](sql-database-copy.md) voor meer informatie.

| Foutcode | Ernst | Beschrijving |
| ---:| ---:|:--- |
| 40635 |16 |Client met IP-adres '%. & #x2a; ls' is tijdelijk uitgeschakeld. |
| 40637 |16 |Maken van database-exemplaar is momenteel uitgeschakeld. |
| 40561 |16 |Kopiëren van de database is mislukt. De database van Hallo bron- of doelentiteit bestaat niet. |
| 40562 |16 |Kopiëren van de database is mislukt. Hallo-brondatabase is verwijderd. |
| 40563 |16 |Kopiëren van de database is mislukt. Hallo doeldatabase is verwijderd. |
| 40564 |16 |Kopiëren is mislukt vanwege een interne fout tooan van de database. Doeldatabase en probeer het opnieuw. |
| 40565 |16 |Kopiëren van de database is mislukt. Niet meer dan 1 gelijktijdige databasekopie van Hallo dezelfde bron is toegestaan. Doeldatabase en probeer het later opnieuw. |
| 40566 |16 |Kopiëren is mislukt vanwege een interne fout tooan van de database. Doeldatabase en probeer het opnieuw. |
| 40567 |16 |Kopiëren is mislukt vanwege een interne fout tooan van de database. Doeldatabase en probeer het opnieuw. |
| 40568 |16 |Kopiëren van de database is mislukt. Brondatabase is niet meer beschikbaar. Doeldatabase en probeer het opnieuw. |
| 40569 |16 |Kopiëren van de database is mislukt. Doeldatabase is niet meer beschikbaar. Doeldatabase en probeer het opnieuw. |
| 40570 |16 |Kopiëren is mislukt vanwege een interne fout tooan van de database. Doeldatabase en probeer het later opnieuw. |
| 40571 |16 |Kopiëren is mislukt vanwege een interne fout tooan van de database. Doeldatabase en probeer het later opnieuw. |

## <a name="resource-governance-errors"></a>Resource governance fouten
Hallo volgende fouten worden veroorzaakt door overmatig gebruik van bronnen tijdens het werken met Azure SQL Database. Bijvoorbeeld:

* Een transactie is te lang geopend.
* Een transactie is te veel vergrendelingen.
* Een toepassing is er te veel geheugen.
* Een toepassing te veel verbruikt `TempDb` ruimte.

Verwante onderwerpen:

* Meer gedetailleerde informatie is hier beschikbaar: [limieten voor Azure SQL Database](sql-database-resource-limits.md)

| Foutcode | Ernst | Beschrijving |
| ---:| ---:|:--- |
| 10928 |20 |Resource-ID: %d. Hallo %s limiet voor de database Hallo %d is en is bereikt. Zie voor meer informatie [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637).<br/><br/>Hallo-bron-ID geeft Hallo resource Hallo limiet heeft bereikt. Hallo voor werkthreads, Resource-ID = 1. Hallo voor sessies, Resource-ID = 2.<br/><br/>*Opmerking:* voor meer informatie over deze fout en hoe tooresolve, Zie:<br/>• [Limieten voor azure SQL Database](sql-database-resource-limits.md). |
| 10929 |20 |Resource-ID: %d. Hallo %s minimumgarantie is %d, maximum aantal %d is en Hallo huidige gebruik voor Hallo-database is %d. Hallo-server is echter momenteel te druk bezet toosupport aanvragen groter zijn dan %d voor deze database. Zie voor meer informatie [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637). Anders, probeer het later opnieuw.<br/><br/>Hallo-bron-ID geeft Hallo resource Hallo limiet heeft bereikt. Hallo voor werkthreads, Resource-ID = 1. Hallo voor sessies, Resource-ID = 2.<br/><br/>*Opmerking:* voor meer informatie over deze fout en hoe tooresolve, Zie:<br/>• [Limieten voor azure SQL Database](sql-database-resource-limits.md). |
| 40544 |20 |Hallo-database heeft het quotum grootte bereikt. Partitioneer of verwijder gegevens, verwijder indexen of Raadpleeg Hallo-documentatie voor mogelijke oplossingen. |
| 40549 |16 |Sessie is beëindigd omdat er een langlopende transactie. Probeer uw transactie te verkorten. |
| 40550 |16 |Hallo-sessie is beëindigd omdat er te veel vergrendelingen heeft verkregen. Probeer het lezen of minder rijen in één transactie te wijzigen. |
| 40551 |16 |Hallo-sessie is beëindigd vanwege het overmatige `TEMPDB` informatie over het gebruik. Probeer uw query tooreduce Hallo tijdelijke tabelruimte te wijzigen.<br/><br/>*Tip:* als u van tijdelijke objecten gebruikmaakt, schijfruimte besparen in Hallo `TEMPDB` database door tijdelijke objecten neer te zetten nadat ze niet langer nodig zijn voor Hallo-sessie. |
| 40552 |16 |Hallo-sessie is beëindigd vanwege het gebruik van ruimte overmatige transactielogboeken. Probeer minder rijen in één transactie te wijzigen.<br/><br/>*Tip:* dat u bulksgewijs invoegen met Hallo uitvoeren `bcp.exe` hulpprogramma of Hallo `System.Data.SqlClient.SqlBulkCopy` klasse, probeert u Hallo `-b batchsize` of `BatchSize` opties toolimit Hallo aantal rijen in elke transactie toohello server hebt gekopieerd. Als u opnieuw van een index met Hallo opbouwen `ALTER INDEX` gebruik Hallo-instructie `REBUILD WITH ONLINE = ON` optie. |
| 40553 |16 |Hallo-sessie is beëindigd vanwege het overmatige geheugengebruik. Probeer minder rijen te wijzigen van uw query tooprocess.<br/><br/>*Tip:* Hallo aantal verminderen `ORDER BY` en `GROUP BY` bewerkingen in uw code Transact-SQL vermindert Hallo geheugenvereisten van de query. |

## <a name="elastic-pool-errors"></a>Elastische pool fouten
Hallo volgende fouten zijn gerelateerde toocreating en het gebruik van Elastics groepen.

| Foutnummer | ErrorSeverity | ErrorFormat | ErrorInserts | ErrorCause | ErrorCorrectiveAction |
|:--- |:--- |:--- |:--- |:--- |:--- |
| 1132 |EX_RESOURCE |Hallo elastische groep heeft de opslaglimiet bereikt. Hallo opslaggebruik voor de elastische groep Hallo mag niet meer dan (%d) MB. |Limiet voor elastische pool schijfruimte in MB. |Er wordt geprobeerd toowrite gegevens tooa database als Hallo opslaglimiet van de elastische pool Hallo is bereikt. |Overweeg het toenemende Hallo dtu's van Hallo elastische pool indien mogelijk in volgorde tooincrease de opslaglimiet bereikt, Hallo opslagruimte die wordt gebruikt door de afzonderlijke databases in de elastische pool Hallo verminderen of databases verwijderen uit elastische groep Hallo. |
| 10929 |EX_USER |Hallo %s minimumgarantie is %d, maximum aantal %d is en Hallo huidige gebruik voor Hallo-database is %d. Hallo-server is echter momenteel te druk bezet toosupport aanvragen groter zijn dan %d voor deze database. Zie [http://go.microsoft.com/fwlink/?LinkId=267637](http://go.microsoft.com/fwlink/?LinkId=267637) voor hulp. Anders, probeer het later opnieuw. |Minimale aantal DTU's per database. Maximale aantal DTU's per database |Totaal aantal gelijktijdige werknemers (aanvragen) voor alle databases in Hallo elastische pool tooexceed poging om de limiet van Hallo Hallo. |Neem Hallo dtu's van Hallo elastische pool indien mogelijk in volgorde tooincrease vergroot de werknemer bereikt of databases verwijderen uit elastische groep Hallo. |
| 40844 |EX_USER |Database '%ls' op Server '%ls' is een '%ls'-database in een elastische pool en een relatie doorlopend kopiëren kan hebben. |databasenaam, de database-editie, de servernaam |Een opdracht StartDatabaseCopy is uitgegeven voor een niet-premium-database in een elastische pool. |Binnenkort beschikbaar |
| 40857 |EX_USER |Elastische groep niet vinden voor server: '%ls', naam elastische groep: '%ls'. |naam van de server. de naam van de elastische groep |Opgegeven elastische groep bestaat niet in de opgegeven server Hallo. |Geef de naam van een geldige elastische groep. |
| 40858 |EX_USER |Elastische groep '%ls' bestaat al in de server: '%ls' |de naam van de elastische groep, servernaam |Opgegeven elastische groep bestaat al in de opgegeven logische server Hallo. |Geef de naam van een nieuwe elastische pool. |
| 40859 |EX_USER |Elastische groep biedt geen ondersteuning voor servicelaag '%ls'. |elastische groepservicelaag |Laag van de opgegeven service wordt niet ondersteund voor het inrichten van de elastische groep. |Geef de juiste editie Hallo of laat service tier leeg toouse Hallo standaard servicelaag. |
| 40860 |EX_USER |Combinatie van elastische groep '%ls' en de service doelstelling '%ls' is ongeldig. |de naam van de elastische groep; naam van serviceniveaudoelstelling |Elastische pool en service doelstelling tegelijk worden opgegeven als de servicedoelstelling is opgegeven als 'ElasticPool'. |Geef de juiste combinatie van elastische pool en servicedoelstelling. |
| 40861 |EX_USER |database-editie Hallo ' %. *ls kunnen niet anders dan Hallo elastische groepservicelaag die is ' %.* ls'. |database-editie, elastische groepservicelaag |Hallo database-editie is anders dan de elastische groepservicelaag Hallo. |Geef geen een database-editie die anders dan de elastische groepservicelaag Hallo is.  Houd er rekening mee dat Hallo database-editie niet hoeft toobe opgegeven. |
| 40862 |EX_USER |De naam van de elastische groep moet worden opgegeven als de servicedoelstelling voor Hallo elastische groep is opgegeven. |Geen |Elastische pool servicedoelstelling vormt geen unieke identificatie voor een elastische pool. |Geef naam van de elastische groep Hallo als Hallo elastische pool servicedoelstelling gebruikt. |
| 40864 |EX_USER |Hallo dtu's voor Hallo elastische groep moet ten minste (%d) dtu's voor servicelaag ' % * ls'. |Aantal dtu's voor de elastische groep; elastische groepservicelaag. |Er wordt geprobeerd tooset hello dtu's voor de elastische groep Hallo onder Hallo minimum. |Probeer het opnieuw instellen Hallo dtu's voor Hallo elastische pool tooat minimaal Hallo minimale limiet. |
| 40865 |EX_USER |Hallo dtu's voor de elastische groep Hallo niet langer zijn dan (%d) dtu's voor servicelaag ' % * ls'. |Aantal dtu's voor de elastische groep; elastische groepservicelaag. |Er wordt geprobeerd tooset hello dtu's voor de elastische groep Hallo hierboven Hallo maximumlimiet. |Probeer het opnieuw instellen Hallo dtu's voor Hallo elastische pool toono groter is dan de maximumlimiet Hallo. |
| 40867 |EX_USER |Hallo DTU max per database moet ten minste (%d) voor servicelaag ' % * ls'. |Maximale aantal DTU's per database. elastische groepservicelaag |Tooset hello DTU max per database hieronder Hallo probeert de ondersteunde limiet. |Overweeg het gebruik van Hallo elastische groepservicelaag die ondersteuning biedt voor Hallo desired-instelling. |
| 40868 |EX_USER |Hallo DTU max per database kan niet groter zijn dan (%d) voor servicelaag ' % * ls'. |Maximale aantal DTU's per database. elastische groepservicelaag. |Tooset hello DTU max per database buiten Hallo probeert de ondersteunde limiet. |Overweeg het gebruik van Hallo elastische groepservicelaag die ondersteuning biedt voor Hallo desired-instelling. |
| 40870 |EX_USER |Hallo minimale aantal DTU's per database kan niet groter zijn dan (%d) voor servicelaag ' % * ls'. |Minimale aantal DTU's per database. elastische groepservicelaag. |Tooset hello minimale aantal DTU's per database buiten Hallo probeert de ondersteunde limiet. |Overweeg het gebruik van Hallo elastische groepservicelaag die ondersteuning biedt voor Hallo desired-instelling. |
| 40873 |EX_USER |Hallo aantal databases (%d) en het minimale aantal DTU's per database (%d) kan niet groter zijn dan Hallo dtu's van de Hallo elastische groep (%d). |Aantal databases in elastische pool; Minimale aantal DTU's per database. Dtu's van elastische pool. |Er wordt geprobeerd toospecify minimale aantal DTU's voor databases in Hallo elastische pool die langer is dan Hallo dtu's van elastische pool Hallo. |Hallo dtu's van elastische pool hello, vergroot of Hallo minimale aantal DTU's per database te verkleinen of verminder het aantal databases in de elastische pool Hallo Hallo. |
| 40877 |EX_USER |Een elastische groep kan niet worden verwijderd tenzij het bevat niet alle databases. |Geen |Hallo elastische groep bevat een of meer databases en kan niet worden verwijderd. |Neem databases verwijderen uit de elastische groep Hallo in volgorde toodelete deze. |
| 40881 |EX_USER |Hallo elastische groep ' % * ls heeft de database count-limiet bereikt.  Hallo databaselimiet voor de elastische groep Hallo kan niet groter zijn dan (%d) voor een elastische groep met dtu's (%d). |Naam van de elastische pool; limiet voor het aantal van de elastische pool database; e dtu's voor de resourcegroep. |Probeert toocreate of tooelastic databasegroep toevoegen wanneer Hallo databaselimiet voor het aantal van de elastische pool Hallo is bereikt. |Neem Hallo dtu's van Hallo elastische pool indien mogelijk in volgorde tooincrease vergroot de databaselimiet voor de of databases verwijderen uit elastische groep Hallo. |
| 40889 |EX_USER |Hallo dtu's of de opslaglimiet voor de elastische groep Hallo ' % * ls kunnen niet worden verhoogd omdat die niet voldoende opslagruimte voor de databases wilt opgeven. |De naam van de elastische pool. |Er wordt geprobeerd toodecrease Hallo opslaglimiet van de elastische pool Hallo lager dan het gebruik van de opslag. |Overweeg opslaggebruik Hallo van afzonderlijke databases in de elastische groep Hallo verminderen of verwijderen uit de groep Hallo in volgorde tooreduce databases de dtu's of de opslag limiet. |
| 40891 |EX_USER |Hallo minimale aantal DTU's per database (%d) kan niet groter zijn dan Hallo maximale aantal DTU's per database (%d). |Minimale aantal DTU's per database. DTU max per database. |Er wordt geprobeerd tooset Hallo minimale aantal DTU's per database hoger is dan Hallo DTU max per database. |Controleer of de Hallo minimale aantal DTU's per databases niet langer zijn dan Hallo DTU max per database. |
| NOG TE BEPALEN |EX_USER |Hallo opslag voor een individuele database in een elastische groep kan niet groter zijn dan de maximale grootte Hallo toegestaan door ' % * ls' service tier elastische pool. |elastische groepservicelaag |Hallo max voor database Hallo Hallo max is groter dan toegestaan door de elastische groepservicelaag Hallo. |Stel de maximale grootte van database binnen de limieten van Hallo maximaal toegestaan door de elastische groepservicelaag Hallo Hallo HALLO hallo. |

Verwante onderwerpen:

* [Een elastische pool (C#) maken](sql-database-elastic-pool-manage-csharp.md) 
* [Een elastische pool (C#) beheren](sql-database-elastic-pool-manage-csharp.md). 
* [Maken van een elastische pool (PowerShell)](sql-database-elastic-pool-manage-powershell.md) 
* [Bewaken en beheren van een elastische pool (PowerShell)](sql-database-elastic-pool-manage-powershell.md).

## <a name="general-errors"></a>Algemene fouten
Hallo volgende fouten vallen niet in de vorige categorieën.

| Foutcode | Ernst | Beschrijving |
| ---:| ---:|:--- |
| 15006 |16 |<AdministratorLogin>is niet een geldige naam omdat deze ongeldige tekens bevat. |
| 18452 |14 |Aanmelden is mislukt. Hallo aanmelding is afkomstig uit een niet-vertrouwd domein en kan niet worden gebruikt met Windows authentication.%. & #x2a; ls (Windows-aanmeldingen worden niet ondersteund in deze versie van SQL Server.) |
| 18456 |14 |Aanmelding mislukt voor gebruiker ' % #x2a;ls'.%. & #x2a; % ls. & #x2a; ls (Hallo aanmelding is mislukt voor gebruiker '%. & #x2a; ls'. Hallo wachtwoordwijziging is mislukt. Wijzigen van wachtwoorden tijdens het aanmelden wordt niet ondersteund in deze versie van SQL Server.) |
| 18470 |14 |Aanmelding mislukt voor gebruiker '%. & #x2a; ls'. Reden: het Hallo-account is disabled.%. & #x2a; ls |
| 40014 |16 |Meerdere databases kunnen niet worden gebruikt in Hallo dezelfde transactie. |
| 40054 |16 |Tabellen zonder geclusterde index worden niet ondersteund in deze versie van SQL Server. Een geclusterde index maken en probeer het opnieuw. |
| 40133 |15 |Deze bewerking wordt niet ondersteund in deze versie van SQL Server. |
| 40506 |16 |De opgegeven SID is ongeldig voor deze versie van SQL Server. |
| 40507 |16 |' %. & #x2a; ls kunnen niet worden aangeroepen met parameters in deze versie van SQL Server. |
| 40508 |16 |De instructie USE is geen ondersteunde tooswitch tussen databases. Gebruik een nieuwe verbinding tooconnect tooa andere database. |
| 40510 |16 |De instructie '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server |
| 40511 |16 |De ingebouwde functie '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40512 |16 |Afgeschafte functie '%ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40513 |16 |Server variabele '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40514 |16 |'%ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40515 |16 |Referentienaam toodatabase en/of de server in '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40516 |16 |Globale, tijdelijke objecten worden niet ondersteund in deze versie van SQL Server. |
| 40517 |16 |Trefwoord-of instructieoptie '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40518 |16 |DBCC-opdracht '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40520 |16 |De beveiligbare klasse '% S_MSG' wordt niet ondersteund in deze versie van SQL Server. |
| 40521 |16 |S_MSG beveiligbare klasse '%' wordt niet ondersteund in het serverbereik Hallo in deze versie van SQL Server. |
| 40522 |16 |Database-principal '%. & #x2a; ls'-type wordt niet ondersteund in deze versie van SQL Server. |
| 40523 |16 |Maken van het impliciete gebruiker '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. Expliciet Hallo-gebruiker maken voordat u deze gebruikt. |
| 40524 |16 |Gegevenstype '%. & #x2a; ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40525 |16 |MET '%.ls' wordt niet ondersteund in deze versie van SQL Server. |
| 40526 |16 |' %. & #x2a; rijensetprovider ls niet ondersteund in deze versie van SQL Server. |
| 40527 |16 |Gekoppelde servers worden niet ondersteund in deze versie van SQL Server. |
| 40528 |16 |Gebruikers kunnen niet worden toegewezen toocertificates, asymmetrische sleutels of Windows-aanmeldingen in deze versie van SQL Server. |
| 40529 |16 |De ingebouwde functie '%. & #x2a; ls' in imitatie context niet wordt ondersteund in deze versie van SQL Server. |
| 40532 |11 |Server kan niet worden geopend '%. & #x2a; ls' aangevraagd door de Hallo aanmelding. Hallo-aanmelding is mislukt. |
| 40553 |16 |Hallo-sessie is beëindigd vanwege het overmatige geheugengebruik. Probeer minder rijen te wijzigen van uw query tooprocess.<br/><br/>*Opmerking:* Hallo aantal verminderen `ORDER BY` en `GROUP BY` bewerkingen in uw code Transact-SQL reduceert Hallo geheugenvereisten van de query. |
| 40604 |16 |Kan geen CREATE/ALTER DATABASE, omdat het Hallo-quotum van Hallo server overschreden. |
| 40606 |16 |Databases koppelen wordt niet ondersteund in deze versie van SQL Server. |
| 40607 |16 |Windows-aanmeldingen worden niet ondersteund in deze versie van SQL Server. |
| 40611 |16 |Servers kunnen maximaal 128 firewallregels zijn gedefinieerd hebben. |
| 40614 |16 |Eerste IP-adres van de firewallregel kan IP-eindadres niet overschrijden. |
| 40615 |16 |Kan de server '{0}' is aangevraagd door de Hallo aanmelding niet openen. Client met IP-adres is '{1}' niet toegestaan voor tooaccess Hallo-server.  tooenable toegang, Hallo SQL Database-Portal gebruiken of sp_set_firewall_rule op Hallo hoofddatabase toocreate een firewallregel voor dit IP-adres of het adresbereik dat wordt uitgevoerd.  Het kan hiertoe tootake wijziging toofive minuten duren. |
| 40617 |16 |Hallo naam firewallregel die met begint <rule name> is te lang. Maximale lengte is 128. |
| 40618 |16 |naam van de firewallregel Hallo mag niet leeg zijn. |
| 40620 |16 |Hallo-aanmelding is mislukt voor gebruiker '%. & #x2a; ls'. Hallo wachtwoordwijziging is mislukt. Wijzigen van wachtwoorden tijdens het aanmelden wordt niet ondersteund in deze versie van SQL Server. |
| 40627 |20 |Bewerking op server '{0}' en de database '{1}' wordt uitgevoerd. Wacht een paar minuten en probeer het opnieuw. |
| 40630 |16 |Wachtwoordvalidatie is mislukt. Hallo wachtwoord voldoet niet aan de beleidseisen omdat het te kort is. |
| 40631 |16 |Hallo u opgegeven wachtwoord is te lang. Hallo-wachtwoord moet langer zijn dan 128 tekens hebben. |
| 40632 |16 |Wachtwoordvalidatie is mislukt. Hallo wachtwoord voldoet niet aan de beleidseisen omdat het niet complex genoeg is. |
| 40636 |16 |Een gereserveerde databasenaam niet gebruiken '%. & #x2a; ls' in deze bewerking. |
| 40638 |16 |Ongeldige abonnements-id < abonnements-id >. Abonnement bestaat niet. |
| 40639 |16 |Aanvraag voldoet niet tooschema: <schema error>. |
| 40640 |20 |Hallo-server heeft een onverwachte uitzondering aangetroffen. |
| 40641 |16 |Hallo opgegeven locatie is ongeldig. |
| 40642 |17 |Hallo-server is momenteel bezet. Probeer het later opnieuw. |
| 40643 |16 |Hallo opgegeven x-ms-version-kopwaarde is ongeldig. |
| 40644 |14 |Mislukte tooauthorize toegang toohello opgegeven abonnement. |
| 40645 |16 |ServerName <servername> mag niet leeg of null zijn. Deze kan alleen bestaan uit kleine letters 'a'-'z', Hallo cijfers 0-9 en Hallo afbreekstreepje. Hallo koppelteken kan niet leiden of audittrail in Hallo-naam. |
| 40646 |16 |Abonnements-ID mag niet leeg zijn. |
| 40647 |16 |Abonnement < abonnement-id is geen servernaam. |
| 40648 |17 |Zijn er te veel aanvragen uitgevoerd. Probeer het later opnieuw. |
| 40649 |16 |Ongeldig inhoudstype is opgegeven. Alleen application/xml wordt ondersteund. |
| 40650 |16 |< Abonnements-id >-abonnement bestaat niet of is niet gereed voor Hallo-bewerking. |
| 40651 |16 |Kan niet toocreate server omdat het Hallo-abonnement < abonnements-id > is uitgeschakeld. |
| 40652 |16 |Kan niet worden verplaatst of gemaakt van de server. Abonnement < abonnements-id > zal de serverquota overschrijden. |
| 40671 |17 |Communicatiefout tussen Hallo-gateway en Hallo management-service. Probeer het later opnieuw. |
| 40852 |16 |Kan database niet openen ' %. *ls op server ' %.* ls' aangevraagd door de Hallo aanmelding. Access toohello-database is alleen toegestaan met een verbindingsreeks die door de beveiliging is ingeschakeld. tooaccess dit database wijzigen van uw verbinding tekenreeksen toocontain beveiligde in Hallo server FQDN - naam van server.database.windows .net moet gewijzigde too'server naam '.database. `secure`. windows.net. |
| 45168 |16 |Hallo SQL Azure-systeem wordt belast, en een bovenlimiet op gelijktijdige DB CRUD-bewerkingen voor één server is geplaatst (bijv, een database maken). Hallo-server is opgegeven in het foutbericht Hallo heeft maximum aantal gelijktijdige verbindingen Hallo overschreden. Probeer het later opnieuw. |
| 45169 |16 |Hallo SQL azure-systeem wordt belast, en een bovengrens van het aantal gelijktijdige server CRUD-bewerkingen voor een abonnement van één hello wordt geplaatst (bijvoorbeeld een server maken). Hallo abonnement Hallo onjuist opgegeven bericht overschrijdt de maximum aantal gelijktijdige verbindingen Hallo en Hallo-aanvraag is geweigerd. Probeer het later opnieuw. |

## <a name="related-links"></a>Verwante koppelingen
* [Functies van Azure SQL Database](sql-database-features.md)
* [Limieten voor Azure SQL Database](sql-database-resource-limits.md)

