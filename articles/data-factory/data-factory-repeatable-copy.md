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
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="d1114-103">Herhaalbare kopie in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d1114-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="d1114-104">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="d1114-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="d1114-105">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="d1114-105">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="d1114-106">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d1114-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d1114-107">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="d1114-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d1114-108">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d1114-108">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="d1114-109">Hallo volgende voorbeelden zijn voor Azure SQL maar zijn van toepassing tooany gegevensarchief die ondersteuning biedt voor rechthoekige gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="d1114-109">hello following samples are for Azure SQL but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="d1114-110">Wellicht hebt u tooadjust hello **type** van de bron- en Hallo **query** eigenschap (bijvoorbeeld: query in plaats van sqlReaderQuery) voor Hallo gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="d1114-110">You may have tooadjust hello **type** of source and hello **query** property (for example: query instead of sqlReaderQuery) for hello data store.</span></span>   

<span data-ttu-id="d1114-111">Normaal gesproken bij het lezen van relationele winkels, wilt u tooread alleen Hallo gegevens toothat segment overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="d1114-111">Usually, when reading from relational stores, you want tooread only hello data corresponding toothat slice.</span></span> <span data-ttu-id="d1114-112">Een manier toodo zou dus worden met behulp van Hallo WindowStart en WindowEnd systeemvariabelen beschikbaar in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d1114-112">A way toodo so would be by using hello WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="d1114-113">Meer informatie over Hallo variabelen en functies in Azure Data Factory hier in Hallo [Azure Data Factory - functies en systeemvariabelen](data-factory-functions-variables.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d1114-113">Read about hello variables and functions in Azure Data Factory here in hello [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="d1114-114">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d1114-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="d1114-115">Deze query leest de gegevens die uit tabel Hallo MyTable Hallo segment duur bereik (WindowStart -> WindowEnd) valt.</span><span class="sxs-lookup"><span data-stu-id="d1114-115">This query reads data that falls in hello slice duration range (WindowStart -> WindowEnd) from hello table MyTable.</span></span> <span data-ttu-id="d1114-116">Opnieuw uitvoeren van dit segment zou ook altijd voor zorgen dat dezelfde gegevens gelezen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1114-116">Rerun of this slice would also always ensure that hello same data is read.</span></span> 

<span data-ttu-id="d1114-117">In andere gevallen tooread Hallo gehele tabel kunt desgewenst en Hallo sqlReaderQuery kan als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="d1114-117">In other cases, you may wish tooread hello entire table and may define hello sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-toosqlsink"></a><span data-ttu-id="d1114-118">TooSqlSink herhaalbare schrijven</span><span class="sxs-lookup"><span data-stu-id="d1114-118">Repeatable write tooSqlSink</span></span>
<span data-ttu-id="d1114-119">Bij het kopiëren van gegevens te**Azure SQL/SQL-Server** uit andere gegevensarchieven, moet u tookeep herhaalbaarheid in gedachten tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="d1114-119">When copying data too**Azure SQL/SQL Server** from other data stores, you need tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="d1114-120">Bij het kopiëren van gegevens tooAzure SQL/SQL Server-Database, voegt de kopieeractiviteit Hallo gegevenstabel toohello sink standaard.</span><span class="sxs-lookup"><span data-stu-id="d1114-120">When copying data tooAzure SQL/SQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="d1114-121">Zeggen kunt u gegevens wilt kopiëren uit een CSV (door komma's gescheiden waarden) bestand met twee records toohello tabel in een Azure SQL/SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="d1114-121">Say, you are copying data from a CSV (comma-separated values) file containing two records toohello following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="d1114-122">Wanneer een segment wordt uitgevoerd, zijn de twee records Hallo gekopieerde toohello SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="d1114-122">When a slice runs, hello two records are copied toohello SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="d1114-123">Stel dat u fouten gevonden in het bronbestand en Hallo hoeveelheid omlaag buis van 2 too4 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d1114-123">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4.</span></span> <span data-ttu-id="d1114-124">Als u het gegevenssegment Hallo handmatig opnieuw voor deze periode, vindt u twee nieuwe records tooAzure SQL/SQL Server-Database toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d1114-124">If you rerun hello data slice for that period manually, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="d1114-125">In dit voorbeeld wordt ervan uitgegaan dat geen van de kolommen in tabel Hallo HALLO hallo primary key-beperking heeft.</span><span class="sxs-lookup"><span data-stu-id="d1114-125">This example assumes that none of hello columns in hello table has hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="d1114-126">tooavoid dit gedrag, moet u toospecify UPSERT semantiek met behulp van een Hallo na twee mechanismen:</span><span class="sxs-lookup"><span data-stu-id="d1114-126">tooavoid this behavior, you need toospecify UPSERT semantics by using one of hello following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="d1114-127">Methode 1: met behulp van sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d1114-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="d1114-128">U kunt Hallo **sqlWriterCleanupScript** eigenschap tooclean van gegevens uit Hallo sink tabel voordat u gegevens Hallo invoegt wanneer een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d1114-128">You can use hello **sqlWriterCleanupScript** property tooclean up data from hello sink table before inserting hello data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="d1114-129">Wanneer een segment wordt uitgevoerd, wordt de script voor opschoning van Hallo eerste toodelete gegevens die overeenkomt met toohello segment van de SQL-tabel Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d1114-129">When a slice runs, hello cleanup script is run first toodelete data that corresponds toohello slice from hello SQL table.</span></span> <span data-ttu-id="d1114-130">Hallo kopieeractiviteit voegt vervolgens de gegevens in Hallo SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="d1114-130">hello copy activity then inserts data into hello SQL Table.</span></span> <span data-ttu-id="d1114-131">Als het Hallo-segment wordt opnieuw uitgevoerd, Hallo hoeveelheid is bijgewerkt naar wens.</span><span class="sxs-lookup"><span data-stu-id="d1114-131">If hello slice is rerun, hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="d1114-132">Stel Hallo platte was record wordt verwijderd uit de oorspronkelijke csv Hallo.</span><span class="sxs-lookup"><span data-stu-id="d1114-132">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="d1114-133">Hallo-segment opnieuw uit te voeren resulteert vervolgens Hallo resultaat te volgen:</span><span class="sxs-lookup"><span data-stu-id="d1114-133">Then rerunning hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="d1114-134">Hallo kopieeractiviteit uitgevoerd Hallo opschonen script toodelete Hallo bijbehorende gegevens voor dit segment.</span><span class="sxs-lookup"><span data-stu-id="d1114-134">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="d1114-135">En vervolgens het Hallo-invoer wordt gelezen uit Hallo csv (die vervolgens bevat slechts één record) en ingevoegd Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="d1114-135">Then it read hello input from hello csv (which then contained only one record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="d1114-136">Methode 2: met behulp van sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d1114-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d1114-137">SliceIdentifierColumnName wordt momenteel niet ondersteund voor Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d1114-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="d1114-138">Hallo tweede mechanisme tooachieve herhaalbaarheid is door een specifieke kolom (sliceIdentifierColumnName) in Hallo doel tabel.</span><span class="sxs-lookup"><span data-stu-id="d1114-138">hello second mechanism tooachieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in hello target Table.</span></span> <span data-ttu-id="d1114-139">In deze kolom wordt gebruikt door Azure Data Factory tooensure Hallo bron- en doelserver gesynchroniseerd blijven.</span><span class="sxs-lookup"><span data-stu-id="d1114-139">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="d1114-140">Deze methode werkt wanneer er flexibiliteit bij het definiëren van de SQL-tabel doelschema Hallo of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d1114-140">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="d1114-141">In deze kolom wordt gebruikt door Azure Data Factory voor herhaalbaarheid doeleinden en in proces hello Azure Data Factory maakt geen geen schema toohello tabel wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d1114-141">This column is used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory does not make any schema changes toohello Table.</span></span> <span data-ttu-id="d1114-142">Manier toouse deze benadering:</span><span class="sxs-lookup"><span data-stu-id="d1114-142">Way toouse this approach:</span></span>

1. <span data-ttu-id="d1114-143">Een kolom van het type definieert **binair (32)** in Hallo doel-SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="d1114-143">Define a column of type **binary (32)** in hello destination SQL Table.</span></span> <span data-ttu-id="d1114-144">Er mag geen beperkingen voor deze kolom.</span><span class="sxs-lookup"><span data-stu-id="d1114-144">There should be no constraints on this column.</span></span> <span data-ttu-id="d1114-145">Laten we in deze kolom als AdfSliceIdentifier naam voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d1114-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="d1114-146">Brontabel:</span><span class="sxs-lookup"><span data-stu-id="d1114-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="d1114-147">Doeltabel:</span><span class="sxs-lookup"><span data-stu-id="d1114-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="d1114-148">Gebruik deze als volgt in Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="d1114-148">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="d1114-149">Azure Data Factory vult deze kolom aan de hand van de noodzaak tooensure Hallo bron- en doelserver gesynchroniseerd blijven.</span><span class="sxs-lookup"><span data-stu-id="d1114-149">Azure Data Factory populates this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="d1114-150">Hallo-waarden van deze kolom mag niet worden gebruikt buiten deze context.</span><span class="sxs-lookup"><span data-stu-id="d1114-150">hello values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="d1114-151">Hallo-gegevens voor Hallo opgegeven segment van Hallo doel-SQL-tabel vergelijkbare toomechanism 1, Kopieeractiviteit automatisch opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="d1114-151">Similar toomechanism 1, Copy Activity automatically cleans up hello data for hello given slice from hello destination SQL Table.</span></span> <span data-ttu-id="d1114-152">Vervolgens voegt de gegevens van de bron in de doeltabel toohello.</span><span class="sxs-lookup"><span data-stu-id="d1114-152">It then inserts data from source in toohello destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d1114-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d1114-153">Next steps</span></span>
<span data-ttu-id="d1114-154">Controleer Hallo connector artikelen die voor JSON-voorbeelden worden voltooid na:</span><span class="sxs-lookup"><span data-stu-id="d1114-154">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="d1114-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d1114-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="d1114-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d1114-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="d1114-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="d1114-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)