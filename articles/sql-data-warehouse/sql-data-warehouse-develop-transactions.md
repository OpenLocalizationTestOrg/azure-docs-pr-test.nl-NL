---
title: aaaTransactions in SQL Data Warehouse | Microsoft Docs
description: Tips voor het implementeren van transacties in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>Transacties in SQL datawarehouse
Zoals u verwachten zou, SQL Data Warehouse biedt ondersteuning voor transacties als onderdeel van de datawarehouse-workload Hallo. Echter wordt tooensure Hallo prestaties van SQL Data Warehouse onderhouden op grote schaal die sommige functies beperkt wanneer zijn vergeleken tooSQL Server. In dit artikel worden gemarkeerd Hallo verschillen en lijsten Hallo anderen. 

## <a name="transaction-isolation-levels"></a>Transactie-isolatieniveaus
SQL Data Warehouse implementeert ACID-transactions. Hallo isolatie van Hallo transactionele ondersteuning is echter beperkt te`READ UNCOMMITTED` en dit kan niet worden gewijzigd. U kunt een aantal codering methoden tooprevent vervuild gegevens leest als dit een probleem voor u is kunt implementeren. Hallo populairste methoden gebruikmaken van CTAS en tabel partitie overschakelen (vaak ook bekend als verschuivende venster patroon Hallo) tooprevent gebruikers van een query die nog steeds wordt voorbereid. Weergaven die vooraf filter Hallo gegevens is ook een populaire benadering.  

## <a name="transaction-size"></a>De grootte van de transactie
Er is een wijziging één transactie in grootte beperkt. Hallo limiet is vandaag de dag "per distributiepunt' toegepast. Daarom kan Hallo totale toewijzing worden vermenigvuldigd Hallo limiet Hallo distributie count. Hallo distributie cap deelt tooapproximate Hallo maximale aantal rijen in de transactie Hallo door Hallo totale grootte van elke rij. Houd rekening met een gemiddelde kolomlengte duurt in plaats van met behulp van de maximale grootte Hallo voor kolommen met variabele lengte.

In de tabel hieronder Hallo Hallo zijn volgende veronderstellingen aangebracht:

* Een gelijkmatige verdeling van gegevens is opgetreden 
* de gemiddelde rijlengte Hallo is 250 bytes

| [DWU][DWU] | Cap per distributiepunt (GiB) | Aantal distributies | Transactie maximumgrootte (GiB) | # Rijen per distributiepunt | Maximumaantal rijen per transactie |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4,000,000 |240,000,000 |
| DW200 |1.5 |60 |90 |6,000,000 |360,000,000 |
| DW300 |2.25 |60 |135 |9,000,000 |540,000,000 |
| DW400 |3 |60 |180 |12,000,000 |720,000,000 |
| DW500 |3.75 |60 |225 |15,000,000 |900,000,000 |
| DW600 |4.5 |60 |270 |18,000,000 |1,080,000,000 |
| DW1000 |7.5 |60 |450 |30,000,000 |1,800,000,000 |
| DW1200 |9 |60 |540 |36,000,000 |2,160,000,000 |
| DW1500 |11.25 |60 |675 |45,000,000 |2,700,000,000 |
| DW2000 ZIJN |15 |60 |900 |60,000,000 |3,600,000,000 |
| DW3000 |22.5 |60 |1,350 |90,000,000 |5,400,000,000 |
| DW6000 |45 |60 |2,700 |180,000,000 |10,800,000,000 |

Hallo transactie groottelimiet wordt per transactie of bewerking toegepast. Het is niet toegepast op alle gelijktijdige transacties. Elke transactie is daarom toowrite deze hoeveelheid gegevens toohello logboek toegestaan. 

toooptimize en minimaliseren Hallo en de hoeveelheid gegevens geschreven toohello logboek Raadpleeg toohello [transacties aanbevolen procedures] [ Transactions best practices] artikel.

> [!WARNING]
> maximale grootte van de transactie kan alleen worden bereikt voor HASH of ROUND_ROBIN gedistribueerd tabellen waarbij Hallo verspreiden Hallo gegevens Hallo is even. Als Hallo transactie is schrijven van gegevens op een wijze vertekende toohello distributies is hello limiet waarschijnlijk toobe voorafgaande toohello transactie maximale grootte heeft bereikt.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>Transactiestatus
SQL Data Warehouse gebruikt Hallo XACT_STATE() functie tooreport een mislukte transactie Hallo waarde -2. Dit betekent dat Hallo transactie is mislukt en is gemarkeerd voor alleen terugdraaien

> [!NOTE]
> Hallo gebruiken-2 Hallo XACT_STATE functie toodenote een mislukte transactie vertegenwoordigt verschillend gedrag tooSQL Server. Hallo waarde -1 toorepresent een niet-doorvoerbare transactie maakt gebruik van SQL Server. SQL Server kan een aantal fouten binnen een transactie zonder toobe gemarkeerd als niet-doorvoerbare tolereren. Bijvoorbeeld `SELECT 1/0` wordt een fout veroorzaken, maar niet afdwingen van een transactie in een niet-doorvoerbare staat. SQL Server kan ook leesbewerkingen in niet-doorvoerbare transactie Hallo. Echter kunt SQL Data Warehouse u niet doen. Als een fout in een SQL Data Warehouse-transactie optreedt wordt automatisch overgeschakeld naar de Hallo -2-status en kunt u niet kunt toomake selecteren een verdere instructies tot het Hallo-instructie is teruggedraaid. Het is daarom belangrijk toocheck uw toepassing code toosee als XACT_STATE() als u gebruikt moet mogelijk toomake codewijzigingen.
> 
> 

Bijvoorbeeld, in SQL Server mogelijk ziet u een transactie die er als volgt uit:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Als u uw code laat als hierboven krijgt u Hallo volgende foutbericht weergegeven:

Bericht 111233, 16 niveau 1 staat, regel 1 111233; Hallo huidige transactie is afgebroken en alle wijzigingen in afwachting zijn teruggedraaid. Oorzaak: Een transactie in een status terugdraaien van de alleen-lezen is niet expliciet teruggedraaid voordat een DDL-, DML- of SELECT-instructie.

U wordt ook Hallo-uitvoer van Hallo ERROR_ * functies niet ophalen.

Hallo-code moet in SQL Data Warehouse toobe enigszins gewijzigd:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Hallo verwacht gedrag is nu waargenomen. Hallo-fout in Hallo transactie wordt beheerd en Hallo ERROR_ * functies waarden opgeven, zoals verwacht.

Alles wat is gewijzigd dat Hallo is `ROLLBACK` Hallo transactie toohappen had voordat Hallo Hallo foutinformatie in Hallo lezen `CATCH` blok.

## <a name="errorline-function"></a>De functie Error_Line()
Het is ook opgemerkt dat SQL Data Warehouse niet implementeren of Hallo ERROR_LINE() functie ondersteunen. Als u dit in uw code u tooremove, moet deze toobe compatibel zijn met SQL Data Warehouse. Query labels in uw code gebruiken in plaats daarvan tooimplement dezelfde functionaliteit. Raadpleeg toohello [LABEL] [ LABEL] artikel voor meer informatie over deze functie.

## <a name="using-throw-and-raiserror"></a>Met behulp van THROW en RAISERROR
THROW is moderne implementatie voor uitzonderingen in SQL Data Warehouse Hallo maar RAISERROR wordt ook ondersteund. Er zijn een paar verschillen waarde aandacht toohowever betaalt.

* De gebruiker gedefinieerde foutberichten cijfers mogen niet in Hallo 100.000 150.000 bereik voor WEGGOOIEN
* Foutberichten voor RAISERROR worden opgelost op 50.000
* Gebruik van sys.messages wordt niet ondersteund.

## <a name="limitiations"></a>Limitiations
SQL Data Warehouse heeft enkele andere beperkingen die betrekking tootransactions hebben.

Ze zijn als volgt:

* Er is geen gedistribueerde transacties
* Er is geen geneste transacties toegestaan
* Er is geen opslaan punten toegestaan
* Er zijn geen benoemde transacties
* Er is geen gemarkeerde transacties
* Er is geen ondersteuning voor DDL zoals `CREATE TABLE` gedefinieerd binnen een transactie

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over het optimaliseren van transacties, Zie [transacties aanbevolen procedures][Transactions best practices].  Zie toolearn over andere best practices SQL Data Warehouse [aanbevolen procedures voor SQL Data Warehouse][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
