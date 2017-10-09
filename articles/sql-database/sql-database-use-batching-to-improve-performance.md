---
title: aaaHow toouse batchverwerking tooimprove Azure SQL Database-toepassingsprestaties
description: Hallo onderwerp vindt u bewijs dat batchverwerking database operations aanzienlijk imroves Hallo snelheid en schaalbaarheid van uw Azure SQL Database-toepassingen. Hoewel deze batchen technieken voor elke SQL Server-database werken, Hallo Hallo artikel worden op Azure.
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Hoe toouse batchverwerking tooimprove SQL Database-toepassingsprestaties
Batchverwerking van bewerkingen tooAzure SQL-Database aanzienlijk verbetert Hallo prestaties en schaalbaarheid van uw toepassingen. In de volgorde toounderstand Hallo voordelen Hallo eerste deel van dit artikel bevat informatie over sommige voorbeeld testresultaten die sequentieel en batch aanvragen tooa SQL-Database te vergelijken. Hallo rest van Hallo artikel geeft Hallo technieken, scenario's en overwegingen toohelp u toouse batchverwerking is in uw Azure-toepassingen.

## <a name="why-is-batching-important-for-sql-database"></a>Waarom is batchverwerking belangrijk voor SQL-Database?
Batchverwerking aanroepen tooa externe service is een bekende strategie voor prestaties en schaalbaarheid te verhogen. Er zijn vaste kosten tooany interactie met een externe service, zoals serialisatie netwerkoverdracht en deserialisatie verwerken. Veel afzonderlijke transacties in één batch minimaliseert deze kosten.

In dit artikel willen we tooexamine verschillende scenario's en batchen strategieën SQL-Database. Hoewel deze strategieën ook belang voor on-premises toepassingen die gebruikmaken van SQL Server zijn, zijn er diverse redenen voor Hallo gebruik van batchverwerking voor SQL-Database te markeren:

* Er is mogelijk groter netwerklatentie toegang tot SQL-Database, met name als u krijgt u toegang tot SQL-Database van de buitenste Hallo hetzelfde Microsoft Azure-datacenter.
* Hallo multitenant kenmerken van SQL-Database betekent dat de efficiëntie van de gegevens Hallo Hallo toegang tot laag standaarddocumentnaam toohello algehele schaalbaarheid van Hallo-database. SQL-Database moet voorkomen dat een single-tenant/gebruiker nadeel werken toohello van database-bronnen van andere tenants belasten. In het antwoord toousage boven het vooraf gedefinieerde quota, SQL Database verminderen doorvoer of reageren met een beperking van uitzonderingen. Efficiëntie, zoals batches, kunnen u toodo meer werk voor SQL-Database voordat deze limiet is bereikt. 
* Batchverwerking is ook geschikt voor architecturen die gebruikmaken van meerdere databases (sharding). Hallo-efficiëntie van uw interactie met elke eenheid database nog steeds een belangrijke factor in uw algehele schaalbaarheid. 

Een van de Hallo voordelen van het gebruik van SQL-Database is dat er geen toomanage Hallo servers die host Hallo-database. Deze beheerde infrastructuur ook betekent echter dat u toothink anders over optimalisaties van de database hebt. U kunt niet meer tooimprove Hallo database hardware- of -infrastructuur te zoeken. Microsoft Azure bepaalt deze omgevingen. Hallo gebied die u kunt beheren, is de interactie van uw toepassing met de SQL-Database. Batchverwerking is een van deze optimalisaties. 

eerste deel van de Hallo Hallo papier onderzoekt verschillende batchen technieken voor .NET-toepassingen die gebruikmaken van SQL-Database. de laatste twee secties Hallo uitgelegd batchen scenario's en richtlijnen.

## <a name="batching-strategies"></a>Batchverwerking strategieën
### <a name="note-about-timing-results-in-this-topic"></a>Houd er rekening mee over timing resultaten in dit onderwerp
> [!NOTE]
> Resultaten niet benchmarks, maar zijn bedoeld tooshow **relatieve prestaties**. Tijdsinstellingen zijn gebaseerd op een gemiddelde van ten minste 10 test wordt uitgevoerd. Bewerkingen worden ingevoegd in een lege tabel. Deze tests zijn gemeten pre-V12 en ze niet per se toothroughput die mogelijk optreden in een V12-database met Hallo nieuwe overeenkomen [Servicelagen](sql-database-service-tiers.md). Hallo relatieve voordeel van het Hallo batchverwerking techniek moet vergelijkbaar zijn.
> 
> 

### <a name="transactions"></a>Transacties
Het lijkt erop vreemd toobegin een overzicht van batchverwerking door het bespreken van transacties. Maar gebruik Hallo van client-side transacties heeft een subtiele serverzijde batchen-effect dat zorgt voor betere prestaties. En transacties kunnen worden toegevoegd met slechts een paar regels code, zodat ze een snelle manier tooimprove prestaties van opeenvolgende bewerkingen bieden.

Overweeg het volgende C#-code die een reeks van insert bevat Hallo en bewerkingen op een eenvoudige tabel bijwerken.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Hallo ADO.NET code sequentieel na voert deze bewerkingen.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Hallo de beste manier toooptimize deze code tooimplement is een vorm van client-side batchverwerking van deze aanroepen. Maar er is een eenvoudige manier tooincrease Hallo prestaties van deze code door gewoon Hallo reeks aanroepen in een transactie. Hier volgt Hallo dezelfde code die gebruikmaakt van een transactie.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

In beide voorbeelden worden daadwerkelijk transacties gebruikt. In het eerste voorbeeld hello is elke aanroep van afzonderlijke een impliciete transactie. Een expliciete transactie verpakt in het tweede voorbeeld hello, alle Hallo aanroepen. Per Hallo-documentatie voor Hallo [vooraf geschreven transactielogboek](https://msdn.microsoft.com/library/ms186259.aspx), logboekrecords worden leeggemaakt toohello schijf wanneer Hallo transactie wordt doorgevoerd. Dus door meer aanroepen in een transactie, kan hello schrijven toohello transactielogboek stellen tot Hallo transactie doorgevoerd is. In feite inschakelt u voor Hallo schrijfbewerkingen toohello van server-transactielogboek batchverwerking.

Hallo volgende tabel ziet u enkele ad-hoc-testresultaten. Hallo tests uitgevoerd Hallo die dezelfde sequentiële met en zonder transacties voegt. Voor meer perspectief Hallo eerste reeks tests op afstand vanaf uitgevoerd een laptop toohello-database in Microsoft Azure. Hallo tweede reeks tests uitgevoerd vanuit een cloudservice en de database dat beide zich bevond in Hallo dezelfde Microsoft Azure-datacenter (VS-West). Hallo volgende tabel toont Hallo duur in milliseconden van opeenvolgende voegt met en zonder transacties.

**On-Premises tooAzure**:

| Bewerkingen | Er is geen transactie (ms) | Transactie (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**Azure tooAzure (hetzelfde datacenter)**:

| Bewerkingen | Er is geen transactie (ms) | Transactie (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> Geen zijn resultaten benchmarks. Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).
> 
> 

Op basis van de vorige testresultaten hello, één bewerking in een transactie wrapping neemt af prestaties. Maar als u het aantal bewerkingen binnen een enkele transactie Hallo verhoogt, Hallo prestatieverbeteringen meer wordt gemarkeerd. Hallo prestatieverschil is ook meer merkbare bij alle bewerkingen binnen Hallo Microsoft Azure-datacenter plaatsvinden. Hallo overshadows langere latentie van het gebruik van SQL-Database van Microsoft Azure-datacenter buiten Hallo Hallo prestatieverbetering te bereiken van het gebruik van transacties.

Hoewel het gebruik van transacties Hallo van de prestaties verhogen kunt te blijven[observeren best practices voor transacties en verbindingen](https://msdn.microsoft.com/library/ms187484.aspx). Hallo-transactie zo kort mogelijk en sluiten Hallo databaseverbinding behouden nadat Hallo werk is voltooid. met de instructie in het vorige voorbeeld Hallo Hallo zorgt ervoor dat de Hallo verbinding wordt gesloten wanneer het volgende codeblok Hallo is voltooid.

Hallo vorige voorbeeld laat zien dat u een lokale transactie tooany ADO.NET code met twee regels kunt toevoegen. Transacties bieden een snelle manier tooimprove Hallo prestaties van code waarmee u opeenvolgende invoegen, bijwerken en verwijderen van bewerkingen. Echter kunt wijzigen in Hallo code verdere tootake profiteren van de client-side batches, zoals table-valued parameters voor de snelste Hallo prestaties.

Zie voor meer informatie over transacties in ADO.NET [lokale transacties in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Table-valued parameters
Tabeltypen die door de gebruiker gedefinieerde ondersteunen table-valued parameters als parameters in de Transact-SQL-instructies, opgeslagen procedures en functies. Deze client-side batchen techniek kunt u toosend meerdere rijen van gegevens binnen Hallo tabelwaardeparameter. toouse table-valued parameters definiëren eerst een tabeltype. Hallo volgende Transact-SQL-instructie maakt een tabeltype met de naam **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


In de code, maakt u een **DataTable** Hello exact dezelfde namen en typen van Hallo tabeltype. Dit geeft **DataTable** aanroepen in een parameter van een tekstquery of een opgeslagen procedure. Hallo volgende voorbeeld ziet u deze techniek:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

In het vorige voorbeeld Hallo Hallo **SqlCommand** object voegt rijen uit een tabelwaardeparameter  **@TestTvp** . Hallo eerder gemaakte **DataTable** -object toegewezen toothis parameter Hello **SqlCommand.Parameters.Add** methode. Batchen Hallo invoegen in een aanroep aanzienlijk toeneemt Hallo prestaties via sequentiële ingevoegd.

een opgeslagen procedure tooimprove Hallo vorige voorbeeld bovendien gebruiken in plaats van een opdracht op basis van tekst. Hallo volgende Transact-SQL-opdracht maakt een opgeslagen procedure waarmee Hallo **SimpleTestTableType** tabelwaardeparameter.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Wijzig de Hallo **SqlCommand** declaratie in Hallo vorige code voorbeeld toohello volgende object.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

In de meeste gevallen hebben table-valued parameters gelijkwaardige of betere prestaties dan andere batchen technieken. Table-valued parameters zijn vaak beter, omdat ze meer flexibiliteit dan andere opties. Bijvoorbeeld, staan andere technieken, zoals SQL bulksgewijs kopiëren, alleen de Hallo invoegen van nieuwe rijen. Maar met tabelwaarden parameters, kunt u logica in Hallo opgeslagen procedure toodetermine welke rijen updates zijn en die zijn ingevoegd. Hallo tabeltype kan ook worden gewijzigd toocontain een 'Bewerking'-kolom waarin wordt aangegeven of Hallo opgegeven rij moet worden ingevoegd, bijgewerkt of verwijderd.

Hallo volgende tabel ziet u de testresultaten ad-hoc voor gebruik van parameters tabelwaarden Hallo in milliseconden.

| Bewerkingen | On-Premises tooAzure (ms) | Azure hetzelfde datacenter (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10.000 |23830 |3586 |

> [!NOTE]
> Geen zijn resultaten benchmarks. Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).
> 
> 

Hallo prestatieverbetering van batchverwerking is onmiddellijk zichtbaar. In vorige sequentiële test hello, 1000 bewerkingen zijn in 129 seconden buiten Hallo datacenter en 21 seconden uit binnen Hallo datacenter. Maar met tabelwaarden parameters 1000 operations alleen 2.6 buiten Hallo datacenter en 0,4 seconden binnen Hallo datacenter.

Zie voor meer informatie over table-valued parameters [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>SQL bulksgewijs kopiëren
SQL bulksgewijs kopiëren is een andere manier tooinsert grote hoeveelheden gegevens in een doeldatabase. .NET-toepassingen kunnen gebruikmaken van Hallo **SqlBulkCopy** bewerkingen klasse tooperform bulksgewijs invoegen. **SqlBulkCopy** lijkt in functie toohello opdrachtregelprogramma **Bcp.exe**, of Hallo Transact-SQL-instructie **BULK INSERT**. Hallo volgende voorbeeldcode laat zien hoe toobulk kopie Hallo rijen in de bron Hallo **DataTable**, tabel, toohello doeltabel in SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Er zijn enkele gevallen waarbij bulksgewijs kopiëren heeft de voorkeur boven table-valued parameters. Zie Hallo Vergelijkingstabel Table-Valued parameters versus BULK INSERT-bewerkingen in Hallo onderwerp [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).

Hallo volgende ad-hoc testresultaten geven Hallo prestaties van batchverwerking met **SqlBulkCopy** in milliseconden.

| Bewerkingen | On-Premises tooAzure (ms) | Azure hetzelfde datacenter (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10.000 |21605 |2737 |

> [!NOTE]
> Geen zijn resultaten benchmarks. Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).
> 
> 

In kleinere batch Hallo gebruik table-valued parameters ver-loop Hallo **SqlBulkCopy** klasse. Echter, **SqlBulkCopy** 12-31% sneller dan table-valued parameters uitgevoerd voor de tests Hallo van 1000 en 10.000 rijen. Table-valued parameters, zoals **SqlBulkCopy** is een goede optie voor batch ingevoegd, vooral wanneer vergeleken toohello prestatie van bewerkingen niet batch verwerkt.

Zie voor meer informatie over bulksgewijs kopiëren in ADO.NET [Bulksgewijze kopieerbewerkingen in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Meerdere rij geparametriseerde INSERT-instructies
Een alternatief voor kleine batches is een grote tooconstruct geparametriseerde INSERT-instructie die meerdere rijen worden ingevoegd. Hallo volgende codevoorbeeld ziet u deze methode.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


In dit voorbeeld is tooshow hello basisconcept bedoeld. Een meer realistische scenario zou doorlopen Hallo vereist entiteiten tooconstruct Hallo-queryreeks en Hallo opdrachtparameters tegelijkertijd. Bent u beperkt tooa totaal van 2100 queryparameters bevatten, zodat dit Hallo kunt u het totale aantal rijen dat kan worden verwerkt op deze manier beperkt.

Hallo na ad-hoc resultaten weergeven Hallo prestaties testen van dit type van de instructie insert in milliseconden.

| Bewerkingen | Table-valued parameters (ms) | Één instructie INSERT (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Geen zijn resultaten benchmarks. Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).
> 
> 

Deze methode kan worden iets snellere voor batches die minder dan 100 rijen zijn. Hoewel Hallo verbetering klein is, is deze techniek een andere optie die goed in uw scenario specifieke toepassing werkt mogelijk.

### <a name="dataadapter"></a>DataAdapter
Hallo **DataAdapter** klasse kunt u toomodify een **gegevensset** object en vervolgens dient Hallo wijzigingen Als INSERT, UPDATE en DELETE-bewerkingen. Als u van Hallo gebruikmaakt **DataAdapter** op deze manier is het belangrijk toonote die scheiden oproepen worden gedaan voor elke afzonderlijke bewerking. tooimprove prestaties, gebruik Hallo **UpdateBatchSize** eigenschap toohello aantal bewerkingen tegelijk in batch moet worden opgenomen. Zie voor meer informatie [uitvoeren van Batch bewerkingen met behulp van DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Entity framework
Entity Framework ondersteunt momenteel geen batchverwerking. Andere ontwikkelaars in Hallo community toodemonstrate oplossingen, zoals een onderdrukking Hallo hebt geprobeerd **SaveChanges** methode. Maar Hallo oplossingen zijn meestal complexe en aangepaste toohello toepassing en gegevensmodel. Hallo Entity Framework codeplex project heeft momenteel een bespreking van de pagina voor deze functie-aanvraag. tooview deze discussie Zie [ontwerp notulen - 2 augustus 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Voor de volledigheid, we van mening bent dat deze belangrijk tootalk XML als een batchen strategie. Hallo-gebruik van XML heeft echter geen voordelen ten opzichte van andere methoden en enkele nadelen. Hallo aanpak is vergelijkbaar tootable-valued parameters, maar een XML-bestand of de tekenreeks wordt doorgegeven tooa opgeslagen procedure in plaats van een gebruiker gedefinieerde tabel. Hallo opgeslagen procedure parseert Hallo opdrachten in Hallo opgeslagen procedure.

Er zijn enkele nadelen toothis benadering:

* Werken met XML kan lastig zijn en foutgevoelig.
* Bij het parseren Hallo XML op Hallo-database kan CPU-intensief zijn.
* Deze methode is langzamer dan table-valued parameters in de meeste gevallen.

Hallo gebruik van XML voor batch-query's is daarom niet aanbevolen.

## <a name="batching-considerations"></a>Batchverwerking overwegingen
Hallo uit te voeren meer richtlijnen voor het gebruik van de Hallo van batchverwerking in SQL-Database-toepassingen te bieden.

### <a name="tradeoffs"></a>Voor-en nadelen
Afhankelijk van uw architectuur batchverwerking kan betrekking hebben op een afweging tussen de prestaties en tolerantie. Denk bijvoorbeeld Hallo scenario waar uw rol onverwacht uitvalt. Als u één rij met gegevens verliest, is Hallo impact kleiner dan Hallo gevolgen van het verlies van een grote batch van niet-verzonden rijen. Er is een groter risico wanneer u rijen worden gebufferd voordat ze worden verzonden toohello database in een opgegeven periode.

Vanwege deze afweging evalueren Hallo-type van bewerkingen die u batch. Batch-agressiever (grotere batches en langer tijdvensters) met gegevens die minder kritiek is.

### <a name="batch-size"></a>Batchgrootte
In onze tests is er meestal geen voordeel toobreaking grote batches in kleinere reeksen. Deze onderverdeling vaak resulteerde in feite in trager dan één grote batch wordt verzonden. Neem bijvoorbeeld een scenario waar u tooinsert 1000 rijen. Hallo volgende tabel ziet u hoe lang duurt het toouse table-valued parameters tooinsert 1000 rijen wanneer onderverdeeld in kleinere batches.

| Batchgrootte | Herhalingen | Table-valued parameters (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Geen zijn resultaten benchmarks. Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).
> 
> 

U ziet dat de beste prestaties Hallo voor 1000 rijen toosubmit ze in één keer. In andere tests (hier niet weergegeven) is er een kleine prestaties voordeel toobreak een batch 10000 rij in twee batches van 5000. Maar Hallo tabelschema voor deze tests is relatief eenvoudige, dus u moet uitvoeren op getest uw specifieke gegevens en de batch grootten tooverify deze bevindingen.

Een andere factor tooconsider is dat als de totale batch Hallo te groot wordt, SQL Database mogelijk beperken en toocommit Hallo batch weigeren. Test voor de beste resultaten Hallo uw specifieke scenario toodetermine als er een ideaal batchgrootte. Hallo batchgrootte configureerbaar maken op runtime tooenable snel aanpassingen op basis van prestaties of fouten.

Ten slotte Hallo grootte van Hallo batch worden verdeeld met Hallo risico's van batchverwerking. Als er tijdelijke fouten of Hallo-rol is mislukt, kunt u de Hallo gevolgen van het Hallo opnieuw te proberen of verlies van gegevens in een batch Hallo Hallo.

### <a name="parallel-processing"></a>Parallelle verwerking
Wat gebeurt er als u duurde Hallo benadering Hallo batchgrootte vermindering van maar meerdere threads tooexecute Hallo werk gebruikt? Onze tests bleek opnieuw, of meerdere kleinere multithreaded batches doorgaans uitgevoerd slechter dan één groter batch. Hallo probeert volgende test tooinsert 1000 rijen in een of meer parallelle batches. Deze test toont hoe meer gelijktijdige batches daadwerkelijk prestaties verlaagd.

| Batchgrootte [iteraties] | Twee threads (ms) | Vier threads (ms) | Zes threads (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Geen zijn resultaten benchmarks. Zie Hallo [opmerking over timing resultaten in dit onderwerp](#note-about-timing-results-in-this-topic).
> 
> 

Er zijn verschillende mogelijke oorzaken voor Hallo vermindering in prestaties vanwege tooparallelism:

* Er zijn meerdere gelijktijdige netwerk aanroepen in plaats van een.
* Meerdere bewerkingen op één tabel kunnen leiden tot conflicten en blokkeren.
* Er zijn overhead die is gekoppeld aan multithreading.
* Hallo kosten van meerdere verbindingen belangrijker is dan Hallo voordeel van parallelle verwerking.

Als u verschillende tabellen of databases als doel, is het mogelijk toosee prestaties krijgen met deze strategie. Database-sharding of federaties zou een scenario voor deze benadering zijn. Sharding maakt gebruik van meerdere databases en de andere database tooeach routes. Als er elke kleine batch tooa andere database, kan vervolgens Hallo bewerkingen uit te voeren parallel efficiënter zijn. Hallo prestatieverbetering te bereiken is echter niet groot genoeg toouse als Hallo basis voor een sharding besluit toouse database in uw oplossing.

Parallelle uitvoering van kleinere batches kan in sommige ontwerpen resulteren in betere doorvoer van aanvragen in een systeem wordt belast. In dit geval, zelfs als het sneller tooprocess één groter batch, verwerking van meerdere batches parallel mogelijk efficiënter.

Als u parallelle uitvoering gebruikt, kunt u beheren Hallo maximum aantal werkthreads. Een kleiner getal kan leiden tot minder conflicten en een sneller worden uitgevoerd. Houd ook rekening met Hallo extra belasting die door dit op Hallo doeldatabase in verbindingen en transacties geplaatst.

### <a name="related-performance-factors"></a>Prestaties gerelateerd aan factoren
Typische richtlijnen op de prestaties van de database is ook van invloed op de batchverwerking. Voeg bijvoorbeeld presteert voor tabellen die een primaire sleutel voor grote of veel niet-geclusterde indexen.

Als het table-valued parameters een opgeslagen procedure gebruikt, kunt u opdracht Hallo **SET NOCOUNT ON** aan Hallo begin van Hallo procedure. Deze instructie onderdrukt return van het aantal Hallo van invloed op rijen in de procedure Hallo HALLO hallo. Hallo echter in onze tests gebruik van **SET NOCOUNT ON** geen invloed heeft ofwel nemen de prestaties af. Hallo opgeslagen testprocedure is heel eenvoudig met één **invoegen** opdracht Hallo tabelwaardeparameter. Het is mogelijk dat de complexere opgeslagen procedures van deze instructie profiteren wilt. Maar niet wordt ervan uitgegaan dat toe te voegen **SET NOCOUNT ON** tooyour opgeslagen procedure automatisch verbetert de prestaties. toounderstand Hallo effect, testen van de opgeslagen procedure met en zonder Hallo **SET NOCOUNT ON** instructie.

## <a name="batching-scenarios"></a>Batchverwerking scenario 's
Hallo volgende secties wordt beschreven hoe toouse table-valued parameters in drie scenario's van toepassing. Hallo eerste scenario ziet u hoe buffer en batches kunnen samenwerken. het tweede scenario Hallo verbetert de prestaties door het uitvoeren van de operations master-details in een aanroep van één opgeslagen procedure. Hallo laatste scenario toont hoe toouse table-valued parameters in een "UPSERT"-bewerking.

### <a name="buffering"></a>Buffer
Er zijn enkele scenario's die voor de hand liggende kandidaat voor batchverwerking, zijn er veel scenario's die gebruikmaken van batchverwerking door vertraagde verwerking kunnen uitvoeren. Vertraagde verwerking ook wordt echter een groter risico dat Hallo gegevens gaan in de gebeurtenis Hallo van een onverwachte fout verloren. Het is belangrijk toounderstand dit risico en overweeg Hallo gevolgen.

Neem bijvoorbeeld een webtoepassing waarmee wordt bijgehouden Hallo navigatiegeschiedenis van elke gebruiker. Op elke pagina-aanvraag kan de toepassing hello paginaweergave database aanroep toorecord Hallo van een gebruiker maken. Maar hogere prestaties en schaalbaarheid kunnen worden bereikt door het bufferen Hallo gebruikers navigatie activiteiten en vervolgens deze gegevens toohello database in batches wordt verzonden. U kunt Hallo database bijwerken door de verstreken tijd en/of buffergrootte activeren. Een regel kan bijvoorbeeld opgeven dat Hallo batch moet worden verwerkt na 20 seconden of wanneer Hallo buffer 1000 objecten bereikt.

Hallo volgende codevoorbeeld wordt [reactieve extensies - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffer opgeslagen gebeurtenissen die worden gegenereerd door een controleprogramma klasse. Wanneer Hallo buffer opvulling of er is een time-out is bereikt, Hallo batch van gebruikersgegevens toohello database met een tabelwaardeparameter is verzonden.

Hallo volgende NavHistoryData klasse modellen Hallo gebruiker navigatie details. Deze bevat algemene informatie, zoals gebruikers-id hello, Hallo URL geopend en Hallo tijd toegang.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Hallo NavHistoryDataMonitor klasse is verantwoordelijk voor het bufferen Hallo navigatie gegevens toohello gebruikersdatabase. Het bevat een methode, RecordUserNavigationEntry die antwoordt door een **OnAdded** gebeurtenis. Hallo volgende code toont Hallo constructor logica die gebruikmaakt van Rx toocreate een waarneembare verzameling op basis van Hallo-gebeurtenis. Vervolgens worden toothis waarneembare verzameling bijgehouden met Hallo Buffer methode. Hallo overbelasting geeft dat die buffer Hallo elke 20 seconden of 1000 vermeldingen moet worden verzonden.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

Hallo-handler alle items in de buffer opgeslagen Hallo converteert naar een type tabelwaarden en stuurt vervolgens deze type tooa opgeslagen procedure die processen Hallo batch. Hallo toont volgende code Hallo volledige definitie voor zowel Hallo NavHistoryDataEventArgs en Hallo NavHistoryDataMonitor klassen.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse deze buffer klasse, Hallo-toepassing maakt een statische NavHistoryDataMonitor-object. Telkens wanneer die een gebruiker toegang krijgt een pagina tot roept Hallo toepassing hello NavHistoryDataMonitor.RecordUserNavigationEntry methode. Hallo buffer logica voortgezet tootake antwoord verzenden van de database van deze vermeldingen toohello in batches.

### <a name="master-detail"></a>Details van basispagina
Table-valued parameters zijn handig voor eenvoudige INSERT-scenario's. Het kan echter meer lastig toobatch voegt die betrekking hebben op meer dan één tabel zijn. Hallo ' master/detail'-scenario is een goed voorbeeld. Hallo hoofdtabel identificeert Hallo primaire entiteit. Een of meer detailtabellen opslaan meer gegevens over Hallo entiteit. In dit scenario afdwingen refererende-sleutelrelaties Hallo van details tooa unieke master entiteit. U kunt een vereenvoudigde versie van een tabel PurchaseOrder en de bijbehorende OrderDetail-tabel. Hallo volgende Transact-SQL maakt Hallo PurchaseOrder tabel met vier kolommen: OrderID, OrderDate CustomerID en Status.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Elke order bevat een of meer kopen van een product. Deze informatie wordt vastgelegd in Hallo PurchaseOrderDetail tabel. Hallo volgende Transact-SQL maakt Hallo PurchaseOrderDetail tabel met vijf kolommen: OrderID, OrderDetailID ProductID, UnitPrice en OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

Hallo OrderID kolom in Hallo PurchaseOrderDetail tabel moet verwijzen naar een order uit Hallo PurchaseOrder tabel. na de definitie van een refererende sleutel Hallo dwingt deze beperking af.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

In de volgorde toouse table-valued parameters, moet u een gebruiker gedefinieerde tabeltype voor elke doeltabel hebben.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Vervolgens definieert u een opgeslagen procedure die tabellen van de volgende typen accepteert. Deze procedure kunt een toepassing toolocally batch de een reeks orders en orderdetails in één aanroep. Hallo biedt volgende Transact-SQL Hallo voltooid opgeslagen procedure-declaratie voor deze aankoop voorbeeld.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

In dit voorbeeld Hallo lokaal gedefinieerde @IdentityLink tabel Hallo werkelijke OrderID waarden uit Hallo zojuist ingevoegd rijen bevat. Deze volgorde-id's zijn anders dan Hallo tijdelijke OrderID waarden in Hallo @orders en @details table-valued parameters. Om deze reden Hallo @IdentityLink tabel verbindt vervolgens Hallo OrderID waarden uit Hallo @orders toohello echte OrderID parameterwaarden voor nieuwe rijen Hallo in Hallo PurchaseOrder tabel. Na deze stap Hallo @IdentityLink tabel invoegen Hallo volgorde details Hello kunt vergemakkelijken werkelijke OrderID die voldoet aan de Hallo foreign key-beperking.

Deze opgeslagen procedure kan worden gebruikt vanuit code of van andere Transact-SQL-aanroepen. Zie Hallo table-valued parameters sectie van dit artikel voor een codevoorbeeld. Hallo volgende Transact-SQL ziet u hoe toocall sp_InsertOrdersBatch Hallo.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Deze oplossing kunt elke batch toouse een set waarden OrderID die bij 1 beginnen. Deze tijdelijke OrderID waarden Hallo relaties in batch Hallo beschreven, maar Hallo werkelijke OrderID waarden worden bepaald bij Hallo Hallo insert-bewerking. U kunt Hallo dezelfde instructies in het vorige voorbeeld Hallo meerdere keren worden uitgevoerd en unieke orders genereren in Hallo-database. Overweeg meer code of database logica waarmee wordt voorkomen dubbele orders dat bij het gebruik van deze techniek batchverwerking om deze reden.

In dit voorbeeld laat zien dat zelfs complexere databasebewerkingen, zoals operations master-details, kunnen in batch worden opgenomen met tabelwaarden parameters.

### <a name="upsert"></a>UPSERT
Een ander batchen scenario omvat het gelijktijdig bijwerken van bestaande rijen en nieuwe rijen invoegen. Deze bewerking is het soms waarnaar wordt verwezen tooas een "UPSERT" (update + insert)-bewerking. In plaats van afzonderlijke oproepen tooINSERT en bij te werken, is de instructie MERGE Hallo beste geschikt toothis taak. Hallo MERGE-instructie kunt uitvoeren van beide invoegen en updatebewerkingen in één aanroep.

Table-valued parameters kunnen worden gebruikt met Hallo MERGE-instructie tooperform updates en toevoegingen. Neem bijvoorbeeld een vereenvoudigde werknemerstabel met Hallo volgende kolommen: werknemer-id, FirstName, LastName, SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

In dit voorbeeld kunt u Hallo feit die Hallo SocialSecurityNumber unieke tooperform een SAMENVOEGING van meerdere werknemers. Maak eerst Hallo gebruiker gedefinieerde tabeltype:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Vervolgens maakt u een opgeslagen procedure of code schrijven dat maakt gebruik van MERGE-instructie tooperform Hallo update hello en in te voegen. Hallo volgende voorbeeld wordt Hallo MERGE-instructie op een tabelwaardeparameter @employees, van het type EmployeeTableType. inhoud van Hallo Hallo @employees tabel worden hier niet weergegeven.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Zie voor meer informatie Hallo documentatie en voorbeelden voor het Hallo MERGE-instructie. Hoewel Hallo hetzelfde werk kan worden uitgevoerd in meerdere stappen procedureaanroep met afzonderlijke INSERT- en UPDATE-bewerkingen opgeslagen, is het efficiënter Hallo MERGE-instructie. Databasecode kunt Transact-SQL-aanroepen die gebruikmaken van de instructie MERGE Hallo rechtstreeks zonder twee databaseaanroepen voor INSERT en UPDATE ook opstellen.

## <a name="recommendation-summary"></a>Aanbeveling samenvatting
Hallo bevat volgende lijst een samenvatting van Hallo batchverwerking aanbevelingen in dit onderwerp wordt beschreven:

* Buffer en batchverwerking tooincrease Hallo prestaties en schaalbaarheid van SQL Database-toepassingen gebruiken.
* Begrijpen Hallo balans vinden tussen batchverwerking/buffer en tolerantie. Tijdens een storing rol Hallo risico van het verlies van een niet-verwerkte batch van essentiële bedrijfsgegevens mogelijk bieden, opwegen tegen Hallo prestatievoordelen van batchverwerking.
* Poging tookeep alle aanroepen toohello database binnen één datacenter tooreduce latentie.
* Als u een bepaalde batchen techniek, bieden table-valued parameters Hallo optimale prestaties en flexibiliteit.
* Invoegen van de prestaties voor Hallo snelste, volg deze algemene richtlijnen maar testen van uw scenario:
  * Voor < 100 rijen geparametriseerde gebruik één opdracht invoegen.
  * Voor < 1000 rijen, table-valued parameters te gebruiken.
  * Voor > = 1000 rijen, SqlBulkCopy gebruiken.
* Voor bijwerken en verwijderen van bewerkingen, table-valued parameters gebruiken met opgeslagen procedure logica die de juiste werking Hallo voor elke rij in de Hallo tabel parameter bepaalt.
* Richtlijnen voor batch grootte:
  * Gebruik het grootste batch grootten hello, die geschikt zijn voor uw toepassing en de zakelijke vereisten.
  * Saldo Hallo prestaties krijgen van grote batches met Hallo risico's van tijdelijke of onherstelbare fouten. Wat is Hallo gevolg pogingen of verlies van gegevens in een batch Hallo Hallo? 
  * Test Hallo grootste batch grootte tooverify dat SQL-Database komt niet afwijzen.
  * Configuratie-instellingen maken dat beheer batches, zoals batchgrootte Hallo of Hallo buffering tijdvenster. Deze instellingen bieden flexibiliteit. Hallo gedrag in productie batchverwerking zonder Hallo cloud-service opnieuw te implementeren, kunt u wijzigen.
* Vermijd parallelle uitvoering van batches die worden uitgevoerd op één tabel in een database. Als u toodivide één batch tussen meerdere worker threads kiest, voert u tests toodetermine Hallo ideaal aantal threads. Na een niet-opgegeven drempelwaarde meer threads worden de prestaties verminderen, in plaats van verhogen.
* Overweeg het bufferen van grootte en de tijd bij wijze van het implementeren van batchverwerking voor scenario's met meer.

## <a name="next-steps"></a>Volgende stappen
In dit artikel gericht op het ontwerpen van databases en het coderen van technieken relatie toobatching kunt verbeteren de prestaties en schaalbaarheid. Maar dit is slechts één factor in uw algehele beveiligingsstrategie. Zie voor meer manieren tooimprove prestaties en schaalbaarheid [richtlijnen voor Azure SQL Database-prestaties voor individuele databases](sql-database-performance-guidance.md) en [prijs- en Prestatieoverwegingen voor een elastische pool](sql-database-elastic-pool-guidance.md).

