---
title: aaaIn-geheugen OLTP verbetert de prestaties van SQL-transacties | Microsoft Docs
description: Hanteer In het geheugen OLTP tooimprove transactionele prestaties in een bestaande SQL-database.
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Gebruik In het geheugen OLTP tooimprove de toepassingsprestaties van uw in SQL-Database
[In het geheugen OLTP](sql-database-in-memory.md) gebruikte tooimprove Hallo prestaties van transactieverwerking gegevensopname en tijdelijke gegevens scenario's, kunnen zich in [Premium](sql-database-service-tiers.md) Azure SQL-Databases zonder te verhogen Hallo prijscategorie. 

> [!NOTE] 
> Meer informatie over hoe [Quorum wordt sleutel database werkbelasting verdubbeld tijdens DTU verlagen door 70% met SQL Database](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Volg deze stappen tooadopt In het geheugen OLTP in uw bestaande database.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Stap 1: Zorg ervoor dat u gebruikt een Premium-database
In het geheugen OLTP wordt alleen ondersteund in Premium-databases. In het geheugen wordt ondersteund als Hallo geretourneerd resultaat is 1 (niet 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* staat voor *Extreme transactieverwerking*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Stap 2: Identificeren objecten toomigrate tooIn-geheugen OLTP
SSMS bevat een **transactie prestaties Analysis overzicht** rapport dat u op een database met een actieve werkbelasting uitvoeren kunt. Hallo-rapport identificeert de tabellen en opgeslagen procedures die geschikt voor migratie zijn tooIn-geheugen OLTP.

In SSMS, toogenerate Hallo rapport:

* In Hallo **Objectverkenner**, met de rechtermuisknop op het databaseknooppunt van uw.
* Klik op **rapporten** > **standaardrapporten** > **transactie prestaties Analysis overzicht**.

Zie voor meer informatie [vaststellen als een tabel of een opgeslagen Procedure moet worden overgezet tooIn-geheugen OLTP](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Stap 3: Een vergelijkbare testdatabase maken
Stel dat het Hallo-rapport geeft aan dat de database een tabel die kunnen van wordt profiteren zouden geconverteerd tooa geheugen geoptimaliseerde tabel. U wordt aangeraden tooconfirm Hallo indicatie eerst te testen door te testen.

U moet een test-kopie van de productiedatabase. Hallo testdatabase moet op Hallo service hetzelfde niveau als uw productiedatabase.

tooease tests aanpassen uw testdatabase als volgt:

1. Verbinding maken met toohello testdatabase met behulp van SSMS.
2. tooavoid hoeven Hallo van de optie WITH (SNAPSHOT) in query's, Hallo databaseoptie ingesteld zoals wordt weergegeven in de volgende T-SQL-instructie Hallo:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Stap 4: Tabellen migreren
U moet maken en vullen van een kopie geoptimaliseerd voor geheugen van de tabel Hallo gewenste tootest. U kunt deze maken met behulp van:

* Hallo handige Wizard in SSMS geheugen optimalisatie.
* Handmatige T-SQL.

#### <a name="memory-optimization-wizard-in-ssms"></a>Wizard van geheugen optimalisatie in SSMS
toouse deze migratieoptie:

1. Toohello testdatabase met SSMS verbinden.
2. In Hallo **Objectverkenner**, met de rechtermuisknop op het Hallo-tabel en klik vervolgens op **geheugen optimalisatie Advisor**.
   
   * Hallo **tabel geheugen optimalisatie van Advisor** wizard wordt weergegeven.
3. Klik in de wizard Hallo op **migratie validatie** (of Hallo **volgende** knop) toosee als Hallo tabel een heeft niet-ondersteunde functies die niet worden ondersteund in tabellen geoptimaliseerd voor geheugen. Zie voor meer informatie:
   
   * Hallo *geheugen optimalisatie controlelijst* in [geheugen optimalisatie Advisor](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Transact-SQL-Constructs niet wordt ondersteund door In het geheugen OLTP](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migreren tooIn-geheugen OLTP](http://msdn.microsoft.com/library/dn247639.aspx).
4. Als Hallo tabel geen niet-ondersteunde onderdelen heeft, kunt Hallo advisor Hallo werkelijke schema en de gegevensmigratie voor u uitvoeren.

#### <a name="manual-t-sql"></a>Handmatige T-SQL
toouse deze migratieoptie:

1. Verbinding tooyour testdatabase met SSMS (of een vergelijkbaar hulpprogramma).
2. Hallo volledige T-SQL-script voor de tabel en de indexen ervan verkrijgen.
   
   * SSMS, met de rechtermuisknop op het knooppunt van uw tabel.
   * Klik op **tabel als een Script** > **maken naar** > **nieuwe queryvenster**.
3. In de script-venster Hallo toevoegen WITH (MEMORY_OPTIMIZED = ON) toohello CREATE TABLE-instructie.
4. Als er een GECLUSTERDE index, wijzigt u het tooNONCLUSTERED.
5. Wijzig de naam van de bestaande tabel Hallo via SP_RENAME.
6. Hallo nieuwe geoptimaliseerd voor geheugen kopie maken van Hallo tabel uw bewerkte CREATE TABLE-script uit te voeren.
7. Hallo gegevens tooyour geheugen geoptimaliseerde tabel kopiëren met behulp van INSERT... SELECTEER * IN:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Stap 5 (optioneel): opgeslagen procedures migreren
Hallo-In-Memory-functie kunt ook een opgeslagen procedure voor verbeterde prestaties wijzigen.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Overwegingen voor systeemeigen, gecompileerde, opgeslagen procedures
Een systeemeigen, gecompileerde, opgeslagen procedure moet beschikken over de volgende opties in de component T-SQL met Hallo:

* NATIVE_COMPILATION
* SCHEMABINDING: betekenis tabellen die Hallo opgeslagen procedure geen hun kolomdefinities gewijzigd op een manier waardoor Hallo opgeslagen procedure, zou beïnvloeden, tenzij u Hallo opgeslagen procedure verwijderen.

Een systeemeigen module moet een gebruiken big [ATOMIC-blokken](http://msdn.microsoft.com/library/dn452281.aspx) voor het transactiebeheer van de. Er is geen rol voor een expliciete BEGIN TRANSACTION of ROLLBACK TRANSACTION. Als uw code een schending van een bedrijfsregel detecteert, deze beëindigen Hallo-atomic-blok met een [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instructie.

### <a name="typical-create-procedure-for-natively-compiled"></a>Typische CREATE PROCEDURE voor systeemeigen, gecompileerde
Hallo T-SQL-toocreate een systeemeigen, gecompileerde, opgeslagen procedure is doorgaans vergelijkbare toohello sjabloon te volgen:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* MOMENTOPNAME is voor Hallo TRANSACTION_ISOLATION_LEVEL, Hallo meest voorkomende waarde voor Hallo systeemeigen, gecompileerde opgeslagen procedure. Echter een subset van Hallo andere waarden worden ook ondersteund:
  
  * REPEATABLE READ
  * SERIALISEERBAAR
* Hallo-waarde van taal moet aanwezig zijn in Hallo sys.languages weergeven.

### <a name="how-toomigrate-a-stored-procedure"></a>Hoe een opgeslagen procedure toomigrate
Hallo migratiestappen zijn:

1. Hallo CREATE PROCEDURE script toohello reguliere geïnterpreteerde opgeslagen procedure verkrijgen.
2. Herschrijf de header toomatch Hallo vorige sjabloon.
3. Nagaan of Hallo opgeslagen procedure T-SQL-code maakt gebruik van alle functies die worden niet ondersteund voor systeemeigen, gecompileerde, opgeslagen procedures. Tijdelijke oplossingen implementeren indien nodig.
   
   * Zie voor meer informatie [migratieproblemen voor systeemeigen gecompileerde opgeslagen Procedures](http://msdn.microsoft.com/library/dn296678.aspx).
4. Wijzig de naam van de oude opgeslagen procedure Hallo via SP_RENAME. Of u gewoon.
5. De bewerkte CREATE PROCEDURE T-SQL-script uitvoeren.

## <a name="step-6-run-your-workload-in-test"></a>Stap 6: Uw werkbelasting uitvoeren in de test
Voer een werkbelasting in uw testdatabase die is vergelijkbaar toohello werkbelasting die wordt uitgevoerd in de productiedatabase. Dit zou moeten uitwijzen Hallo prestatieverbetering bereikt door het gebruik van Hallo In-Memory-functie voor tabellen en opgeslagen procedures.

Belangrijke kenmerken van de werkbelasting Hallo zijn:

* Het aantal gelijktijdige verbindingen.
* Verhouding tussen lezen/schrijven.

tootailor en werkbelasting uitvoeren Hallo-test, kunt u overwegen Hallo handige ostress.exe hulpprogramma, geïllustreerd in [hier](sql-database-in-memory.md).

toominimize netwerklatentie, voert u uw test in Hallo dezelfde Azure geografische regio waar Hallo database bestaat.

## <a name="step-7-post-implementation-monitoring"></a>Stap 7: Na de implementatie controleren
Houd rekening met bewaking Hallo prestaties gevolgen van uw implementaties In het geheugen in productie:

* [In het geheugen, opslag bewaken](sql-database-in-memory-oltp-monitoring.md).
* [Bewaking van Azure SQL-database met behulp van de dynamische beheerweergave](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Verwante koppelingen
* [In het geheugen OLTP (optimalisatie In het geheugen)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Inleiding tooNatively gecompileerde opgeslagen Procedures](http://msdn.microsoft.com/library/dn133184.aspx)
* [Geheugen optimalisatie Advisor](http://msdn.microsoft.com/library/dn284308.aspx)

