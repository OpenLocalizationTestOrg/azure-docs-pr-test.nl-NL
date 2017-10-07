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
# <a name="extended-events-in-sql-database"></a>Uitgebreide gebeurtenissen in SQL-Database
[!INCLUDE [sql-database-xevents-selectors-1-include](../../includes/sql-database-xevents-selectors-1-include.md)]

Dit onderwerp wordt uitgelegd hoe Hallo-implementatie van uitgebreide gebeurtenissen in Azure SQL Database iets anders dan tooextended gebeurtenissen in Microsoft SQL Server is.

- SQL Database V12 die is opgedaan Hallo uitgebreide gebeurtenissen functie in Hallo tweede helft van de kalender 2015.
- SQL Server heeft uitgebreide gebeurtenissen sinds 2008.
- Hallo-functieset van uitgebreide gebeurtenissen op de SQL-Database is een robuuste subset van Hallo-functies op SQL Server.

*XEvents* is een informele bijnaam die soms wordt gebruikt voor 'uitgebreide gebeurtenissen' in blogs en andere informele locaties.

Meer informatie over uitgebreide gebeurtenissen voor Azure SQL Database en Microsoft SQL Server, is beschikbaar op:

- [Snelstartgids: Uitgebreide gebeurtenissen in SQL Server](http://msdn.microsoft.com/library/mt733217.aspx)
- [Uitgebreide gebeurtenissen](http://msdn.microsoft.com/library/bb630282.aspx)

## <a name="prerequisites"></a>Vereisten

In dit onderwerp wordt ervan uitgegaan dat u al enige kennis hebt van:

- [Azure SQL Database-service](https://azure.microsoft.com/services/sql-database/).
- [Uitgebreide gebeurtenissen](http://msdn.microsoft.com/library/bb630282.aspx) in Microsoft SQL Server.

- Hallo bulksgewijs van onze documentatie over uitgebreide gebeurtenissen geldt tooboth SQL Server en SQL-Database.

Eerdere blootstelling toohello volgende items is handig bij het kiezen van de gebeurtenisbestand als Hallo Hallo [doel](#AzureXEventsTargets):

- [Azure Storage-service](https://azure.microsoft.com/services/storage/)


- PowerShell
    - [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) -bevat uitgebreide informatie over PowerShell en hello Azure Storage-service.

## <a name="code-samples"></a>Codevoorbeelden

Verwante onderwerpen bieden twee codevoorbeelden:


- [Ring Buffer doel code voor uitgebreide gebeurtenissen in SQL-Database](sql-database-xevent-code-ring-buffer.md)
    - Korte eenvoudig Transact-SQL-script.
    - We benadrukken in Hallo code voorbeeldonderwerp dat, wanneer u klaar bent met een doel ringbuffer, u de bronnen vrijgeven moet door het uitvoeren van een alter neerzetten `ALTER EVENT SESSION ... ON DATABASE DROP TARGET ...;` instructie. Later kunt u een ander exemplaar van ringbuffer door toevoegen `ALTER EVENT SESSION ... ON DATABASE ADD TARGET ...`.


- [Bestand doel gebeurteniscode voor uitgebreide gebeurtenissen in SQL-Database](sql-database-xevent-code-event-file.md)
    - Fase 1 is PowerShell toocreate een Azure Storage-container.
    - Fase 2 is Transact-SQL die gebruikmaakt van hello Azure Storage-container.

## <a name="transact-sql-differences"></a>Verschillen Transact-SQL


- Bij het uitvoeren van Hallo [maken GEBEURTENIS sessie](http://msdn.microsoft.com/library/bb677289.aspx) opdracht op SQL Server u Hallo gebruikt **ON SERVER** component. Maar op de SQL-Database gebruikt u Hallo **ON DATABASE** component in plaats daarvan.


- Hallo **ON DATABASE** component is ook van toepassing toohello [ALTER GEBEURTENIS sessie](http://msdn.microsoft.com/library/bb630368.aspx) en [DROP GEBEURTENIS sessie](http://msdn.microsoft.com/library/bb630257.aspx) Transact-SQL-opdrachten.


- Is een best practice tooinclude Hallo gebeurtenis sessieoptie van **STARTUP_STATE = ON** in uw **maken GEBEURTENIS sessie** of **ALTER GEBEURTENIS sessie** instructies.
    - Hallo **= ON** waarde ondersteunt automatisch opnieuw opstarten na een herconfiguratie van logische Hallo-database vanwege tooa failover.

## <a name="new-catalog-views"></a>Nieuwe catalogusweergaven

Hallo uitgebreide gebeurtenissen functie wordt ondersteund door verschillende [catalogus weergaven](http://msdn.microsoft.com/library/ms174365.aspx). Catalogusweergaven vertellen u *metagegevens of definities* van gebeurtenissessies in de huidige database Hallo gebruiker gemaakt. Hallo weergaven retourneren informatie over exemplaren van actieve gebeurtenissessies kunnen niet.

| Naam van<br/>catalogusweergave | Beschrijving |
|:--- |:--- |
| **sys.database_event_session_actions** |Retourneert een rij voor elke actie op elke gebeurtenis van de gebeurtenissessie van een. |
| **sys.database_event_session_events** |Retourneert een rij voor elke gebeurtenis in een event-sessie. |
| **sys.database_event_session_fields** |Retourneert een rij voor elke aanpassen kunnen kolom die expliciet is ingesteld op gebeurtenissen en doelen. |
| **sys.database_event_session_targets** |Retourneert een rij voor elk gebeurtenisdoel voor een event-sessie. |
| **sys.database_event_sessions** |Retourneert een rij voor elke gebeurtenissessie in Hallo SQL Database-database. |

In Microsoft SQL Server, vergelijkbare catalogusweergaven hebben namen die zijn *.server\_*  in plaats van *.database\_*. Hallo naampatroon is vergelijkbaar met **sys.server_event_%**.

## <a name="new-dynamic-management-views-dmvshttpmsdnmicrosoftcomlibraryms188754aspx"></a>Nieuwe dynamische beheerweergaven [(DMV's)](http://msdn.microsoft.com/library/ms188754.aspx)

Azure SQL-Database heeft [dynamische beheerweergaven (DMV's)](http://msdn.microsoft.com/library/bb677293.aspx) die ondersteuning bieden voor uitgebreide gebeurtenissen. DMV's informatie over de *active* event-sessies.

| Naam van de DMV | Beschrijving |
|:--- |:--- |
| **sys.dm_xe_database_session_event_actions** |Retourneert informatie over de gebeurtenis sessie acties. |
| **sys.dm_xe_database_session_events** |Retourneert informatie over sessiegebeurtenissen. |
| **sys.dm_xe_database_session_object_columns** |Hallo configuratiewaarden voor objecten die gebonden tooa sessie zijn ziet. |
| **sys.dm_xe_database_session_targets** |Retourneert informatie over de doelen van de sessie. |
| **sys.dm_xe_database_sessions** |Retourneert een rij voor elke gebeurtenissessie die is de huidige database scoped toohello. |

In Microsoft SQL Server, catalogusweergaven vergelijkbaar zijn met de naam zonder Hallo  *\_database* gedeelte van het Hallo-naam, zoals:

- **sys.dm_xe_sessions**, in plaats van naam<br/>**sys.dm_xe_database_sessions**.

### <a name="dmvs-common-tooboth"></a>Algemene tooboth DMV 's
Voor uitgebreide gebeurtenissen er zijn aanvullende DMV's die algemene tooboth Azure SQL Database zijn en Microsoft SQL Server:

- **sys.dm_xe_map_values**
- **sys.dm_xe_object_columns**
- **sys.dm_xe_objects**
- **sys.dm_xe_packages**

 <a name="sqlfindseventsactionstargets" id="sqlfindseventsactionstargets"></a>

## <a name="find-hello-available-extended-events-actions-and-targets"></a>Zoeken naar beschikbare uitgebreide gebeurtenissen hello, acties en doelen

U kunt een eenvoudige SQL uitvoeren **Selecteer** tooobtain een lijst met beschikbare gebeurtenissen hello, acties en doel.

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


<a name="AzureXEventsTargets" id="AzureXEventsTargets"></a> &nbsp;

## <a name="targets-for-your-sql-database-event-sessions"></a>Doelen voor uw SQL-Database event-sessies

Hier volgen doelen die de resultaten van uw event-sessies op SQL-Database kunnen vastleggen:

- [Ring Buffer doel](http://msdn.microsoft.com/library/ff878182.aspx) -kort bevat gegevens van gebeurtenissen in het geheugen.
- [Gebeurtenis teller doel](http://msdn.microsoft.com/library/ff878025.aspx) -telt alle gebeurtenissen die zich tijdens een extended events-sessie voordoen.
- [Doel voor het bestand gebeurtenis](http://msdn.microsoft.com/library/ff878115.aspx) -schrijfbewerkingen voltooid buffers tooan Azure Storage-container.

Hallo [Event Tracing voor Windows (ETW)](http://msdn.microsoft.com/library/ms751538.aspx) API is niet beschikbaar voor uitgebreide gebeurtenissen op de SQL-Database.

## <a name="restrictions"></a>Beperkingen

Er zijn een aantal betrekking hebben op beveiliging verschillen befitting hello cloudomgeving van SQL-Database:

- Uitgebreide gebeurtenissen zijn gevonden op Hallo één tenantisolatie model. Een event-sessie in de ene database geen toegang tot gegevens of gebeurtenissen uit een andere database.
- U het niet mogelijk om een **maken GEBEURTENIS sessie** instructie in de context van Hallo Hallo **master** database.

## <a name="permission-model"></a>Machtiging model

U moet hebben **besturingselement** machtiging op Hallo database tooissue een **maken GEBEURTENIS sessie** instructie. Hallo database-eigenaar (dbo) heeft **besturingselement** machtiging.

### <a name="storage-container-authorizations"></a>Storage-container autorisaties

Hallo SAS-token u genereren voor uw Azure Storage-container moet opgeven **rwl** voor Hallo machtigingen. Hallo **rwl** waarde biedt Hallo volgende machtigingen:

- Lezen
- Schrijven
- Lijst

## <a name="performance-considerations"></a>Prestatieoverwegingen

Er zijn scenario's waar intensief gebruik van uitgebreide gebeurtenissen verzamelen actievere geheugen hebben dan is in orde voor Hallo van het hele systeem. Daarom hello Azure SQL Database system dynamisch wordt ingesteld en past u limieten op Hallo hoeveelheid active geheugen die door een gebeurtenissessie kan worden verzameld. Veel factoren gaat u naar Hallo dynamische berekening.

Als u een foutbericht dat een maximum geheugen is afgedwongen ontvangt, zijn sommige corrigerende acties die u kunt uitvoeren:

- Minder gelijktijdige gebeurtenissessies kunnen worden uitgevoerd.
- Via uw **maken** en **ALTER** -instructies voor de event-sessies verlagen Hallo en de hoeveelheid geheugen die u op Hallo opgeeft **MAX\_geheugen** component.

### <a name="network-latency"></a>Netwerklatentie

Hallo **gebeurtenisbestand** doel tegenkomen netwerklatentie of fouten bij het persistente gegevens tooAzure Storage-blobs. Andere gebeurtenissen in SQL-Database kunnen worden uitgesteld, terwijl ze Hallo netwerk communicatie toocomplete wachten. Deze vertraging kan uw werkbelasting vertragen.

- toomitigate deze prestaties risico, Vermijd de instelling Hallo **EVENT_RETENTION_MODE** te optie**NO_EVENT_LOSS** in uw sessie gebeurtenisdefinities.

## <a name="related-links"></a>Verwante koppelingen

- [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md).
- [Azure-opslag-Cmdlets](http://msdn.microsoft.com/library/dn806401.aspx)
- [Azure PowerShell gebruiken met Azure Storage](../storage/common/storage-powershell-guide-full.md) -bevat uitgebreide informatie over PowerShell en hello Azure Storage-service.
- [Hoe toouse .NET Blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md)
- [CREATE CREDENTIAL (Transact-SQL)](http://msdn.microsoft.com/library/ms189522.aspx)
- [MAKEN van de EVENT-sessie (Transact-SQL)](http://msdn.microsoft.com/library/bb677289.aspx)
- [De Jonathan Kehayias blogberichten over uitgebreide gebeurtenissen in Microsoft SQL Server](http://www.sqlskills.com/blogs/jonathan/category/extended-events/)


- Hello Azure *Service-Updates* webpagina, teruggebracht door parameter tooAzure SQL-Database:
    - [https://Azure.Microsoft.com/updates/?service=SQL-database](https://azure.microsoft.com/updates/?service=sql-database)


Andere onderwerpen voor het voorbeeld van code voor uitgebreide gebeurtenissen zijn beschikbaar op Hallo koppelingen te volgen. Echter, moet u eventuele toosee voorbeeld regelmatig controleren of Hallo voorbeeld is bedoeld voor Microsoft SQL Server versus Azure SQL Database. U kunt vervolgens beslissen of kleine wijzigingen nodig toorun Hallo voorbeeld zijn.

<!--
('lock_acquired' event.)

- Code sample for SQL Server: [Determine Which Queries Are Holding Locks](http://msdn.microsoft.com/library/bb677357.aspx)
- Code sample for SQL Server: [Find hello Objects That Have hello Most Locks Taken on Them](http://msdn.microsoft.com/library/bb630355.aspx)
-->
