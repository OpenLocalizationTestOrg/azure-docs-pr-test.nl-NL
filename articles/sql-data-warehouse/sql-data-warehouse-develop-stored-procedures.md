---
title: de procedures aaaStored in SQL Data Warehouse | Microsoft Docs
description: Tips voor het implementeren van opgeslagen procedures in Azure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>Opgeslagen procedures in SQL Data Warehouse
Veel van Hallo Transact-SQL-functies gevonden in SQL Server biedt ondersteuning voor SQL Data Warehouse. Er zijn belangrijker scale-out specifieke functies die we tooleverage toomaximize Hallo prestaties van uw oplossing wordt wilt.

Toomaintain hello schaal en prestaties van SQL Data Warehouse zijn echter ook sommige functies en functionaliteit die u hebt doorgevoerd verschillen en anderen die niet worden ondersteund.

Dit artikel wordt uitgelegd hoe tooimplement opgeslagen procedures in SQL Data Warehouse.

## <a name="introducing-stored-procedures"></a>Introductie van opgeslagen procedures
Opgeslagen procedures zijn een goede manier voor het inkapselen van uw SQL-code opslaan van het sluiten tooyour gegevens in het datawarehouse Hallo. Door het Hallo-code in beheerbare eenheden encapsulating opgeslagen procedures ontwikkelaars helpen bij het modularize hun oplossingen; vergemakkelijken groter herbruikbaarheid van code. Elke opgeslagen procedure kan ook parameters toomake accepteren ze nog meer flexibiliteit.

SQL Data Warehouse biedt een vereenvoudigd en gestroomlijnd opgeslagen procedure-implementatie. Hallo grootste verschil vergeleken tooSQL-Server is die Hallo opgeslagen procedure is niet vooraf gecompileerde code. In datawarehouses we in het algemeen minder betrokken zijn bij het Hallo-compilatietijd. Het is belangrijk dat Hallo opgeslagen procedurecode correct is geoptimaliseerd, als het wordt uitgevoerd op basis van grote hoeveelheden gegevens. Hallo-doel is toosave uren, minuten en seconden niet milliseconden. Daarom is het handiger toothink van opgeslagen procedures als containers voor SQL-logica.     

Wanneer SQL Data Warehouse wordt uitgevoerd zijn de opgeslagen procedure Hallo SQL-instructies geparseerd, vertaald en geoptimaliseerd tijdens runtime. Tijdens dit proces wordt elke instructie omgezet in gedistribueerde query's. SQL-code die daadwerkelijk wordt uitgevoerd op gegevens Hallo Hallo is verschillende toohello query verzonden.

## <a name="nesting-stored-procedures"></a>Nesten van opgeslagen procedures
Als opgeslagen procedures andere opgeslagen procedures aanroepen of dynamische sql uitvoeren Hallo interne opgeslagen procedure of code aanroep wordt gezegd toobe genest.

SQL Data Warehouse ondersteunt maximaal 8 geneste niveaus. Dit is een iets andere tooSQL Server. Hallo nest niveau in SQL Server is 32.

aanroepen van de bovenste niveau opgeslagen procedure Hallo gelijkstaat toonest niveau 1

```sql
EXEC prc_nesting
```
Als Hallo opgeslagen procedure kan ook een andere EXEC aanroep wordt hierdoor neemt Hallo nest niveau too2

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Als u de tweede procedure Hallo voert enkele dynamische sql vervolgens vergroten dit Hallo nest niveau too3

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Opmerking SQL Data Warehouse ondersteunt momenteel geen@NESTLEVEL. U moet een nummer van uw niveau nest tookeep zelf. Het lijkt onwaarschijnlijk u Hallo 8 nest limiet bereikt, maar als u u wilt nodig hebt toore werk uw code en 'plat' deze zodat het past binnen deze limiet.

## <a name="insertexecute"></a>INSERT... UITVOEREN
SQL Data Warehouse mag u geen tooconsume Hallo resultatenset van een opgeslagen procedure met een instructie INSERT. Er is echter een alternatieve methode die u kunt gebruiken.

Raadpleeg de volgende artikel op toohello [tijdelijke tabellen] voor een voorbeeld over het toodo dit.

## <a name="limitations"></a>Beperkingen
Er zijn bepaalde aspecten van Transact-SQL opgeslagen procedures die niet zijn geïmplementeerd in SQL Data Warehouse.

Ze zijn:

* tijdelijke opgeslagen procedures
* genummerde opgeslagen procedures
* uitgebreide opgeslagen procedures
* CLR opgeslagen procedures
* versleutelingsoptie
* replicatie-optie
* Table-valued parameters
* alleen-lezen parameters
* standaardparameters
* contexten worden uitgevoerd
* instructie return

## <a name="next-steps"></a>Volgende stappen
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[tijdelijke tabellen]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
