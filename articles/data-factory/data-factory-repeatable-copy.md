---
title: aaaRepeatable kopie in Azure Data Factory | Microsoft Docs
description: "Meer informatie over hoe tooavoid duplicaten ondanks dat is meer dan één keer worden uitgevoerd in een segment dat gegevens worden gekopieerd."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 79a3fde2b700bf0a0e167479d6a86c5bee1bf7ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a>Herhaalbare kopie in Azure Data Factory

## <a name="repeatable-read-from-relational-sources"></a>Herhaalbare leesbewerking van relationele bronnen
Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten. In Azure Data Factory, kunt u een segment handmatig opnieuw. U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt. Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.  
 
> [!NOTE]
> Hallo volgende voorbeelden zijn voor Azure SQL maar zijn van toepassing tooany gegevensarchief die ondersteuning biedt voor rechthoekige gegevenssets. Wellicht hebt u tooadjust hello **type** van de bron- en Hallo **query** eigenschap (bijvoorbeeld: query in plaats van sqlReaderQuery) voor Hallo gegevens opslaan.   

Normaal gesproken bij het lezen van relationele winkels, wilt u tooread alleen Hallo gegevens toothat segment overeenkomt. Een manier toodo zou dus worden met behulp van Hallo WindowStart en WindowEnd systeemvariabelen beschikbaar in Azure Data Factory. Meer informatie over Hallo variabelen en functies in Azure Data Factory hier in Hallo [Azure Data Factory - functies en systeemvariabelen](data-factory-functions-variables.md) artikel. Voorbeeld: 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
Deze query leest de gegevens die uit tabel Hallo MyTable Hallo segment duur bereik (WindowStart -> WindowEnd) valt. Opnieuw uitvoeren van dit segment zou ook altijd voor zorgen dat dezelfde gegevens gelezen Hallo. 

In andere gevallen tooread Hallo gehele tabel kunt desgewenst en Hallo sqlReaderQuery kan als volgt gedefinieerd:

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a>TooSqlSink herhaalbare schrijven
Bij het kopiëren van gegevens te**Azure SQL/SQL-Server** uit andere gegevensarchieven, moet u tookeep herhaalbaarheid in gedachten tooavoid ongewenste resultaten. 

Bij het kopiëren van gegevens tooAzure SQL/SQL Server-Database, voegt de kopieeractiviteit Hallo gegevenstabel toohello sink standaard. Zeggen kunt u gegevens wilt kopiëren uit een CSV (door komma's gescheiden waarden) bestand met twee records toohello tabel in een Azure SQL/SQL Server-Database. Wanneer een segment wordt uitgevoerd, zijn de twee records Hallo gekopieerde toohello SQL-tabel. 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Stel dat u fouten gevonden in het bronbestand en Hallo hoeveelheid omlaag buis van 2 too4 bijgewerkt. Als u het gegevenssegment Hallo handmatig opnieuw voor deze periode, vindt u twee nieuwe records tooAzure SQL/SQL Server-Database toegevoegd. In dit voorbeeld wordt ervan uitgegaan dat geen van de kolommen in tabel Hallo HALLO hallo primary key-beperking heeft.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid dit gedrag, moet u toospecify UPSERT semantiek met behulp van een Hallo na twee mechanismen:

### <a name="mechanism-1-using-sqlwritercleanupscript"></a>Methode 1: met behulp van sqlWriterCleanupScript
U kunt Hallo **sqlWriterCleanupScript** eigenschap tooclean van gegevens uit Hallo sink tabel voordat u gegevens Hallo invoegt wanneer een segment wordt uitgevoerd. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Wanneer een segment wordt uitgevoerd, wordt de script voor opschoning van Hallo eerste toodelete gegevens die overeenkomt met toohello segment van de SQL-tabel Hallo uitgevoerd. Hallo kopieeractiviteit voegt vervolgens de gegevens in Hallo SQL-tabel. Als het Hallo-segment wordt opnieuw uitgevoerd, Hallo hoeveelheid is bijgewerkt naar wens.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Stel Hallo platte was record wordt verwijderd uit de oorspronkelijke csv Hallo. Hallo-segment opnieuw uit te voeren resulteert vervolgens Hallo resultaat te volgen: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

Hallo kopieeractiviteit uitgevoerd Hallo opschonen script toodelete Hallo bijbehorende gegevens voor dit segment. En vervolgens het Hallo-invoer wordt gelezen uit Hallo csv (die vervolgens bevat slechts één record) en ingevoegd Hallo tabel. 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a>Methode 2: met behulp van sliceIdentifierColumnName
> [!IMPORTANT]
> SliceIdentifierColumnName wordt momenteel niet ondersteund voor Azure SQL Data Warehouse. 

Hallo tweede mechanisme tooachieve herhaalbaarheid is door een specifieke kolom (sliceIdentifierColumnName) in Hallo doel tabel. In deze kolom wordt gebruikt door Azure Data Factory tooensure Hallo bron- en doelserver gesynchroniseerd blijven. Deze methode werkt wanneer er flexibiliteit bij het definiëren van de SQL-tabel doelschema Hallo of wijzigen. 

In deze kolom wordt gebruikt door Azure Data Factory voor herhaalbaarheid doeleinden en in proces hello Azure Data Factory maakt geen geen schema toohello tabel wordt gewijzigd. Manier toouse deze benadering:

1. Een kolom van het type definieert **binair (32)** in Hallo doel-SQL-tabel. Er mag geen beperkingen voor deze kolom. Laten we in deze kolom als AdfSliceIdentifier naam voor dit voorbeeld.


    Brontabel:

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    Doeltabel: 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. Gebruik deze als volgt in Hallo kopieeractiviteit:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

Azure Data Factory vult deze kolom aan de hand van de noodzaak tooensure Hallo bron- en doelserver gesynchroniseerd blijven. Hallo-waarden van deze kolom mag niet worden gebruikt buiten deze context. 

Hallo-gegevens voor Hallo opgegeven segment van Hallo doel-SQL-tabel vergelijkbare toomechanism 1, Kopieeractiviteit automatisch opgeruimd. Vervolgens voegt de gegevens van de bron in de doeltabel toohello. 

## <a name="next-steps"></a>Volgende stappen
Controleer Hallo connector artikelen die voor JSON-voorbeelden worden voltooid na: 

- [Azure SQL Database](data-factory-azure-sql-connector.md)
- [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)