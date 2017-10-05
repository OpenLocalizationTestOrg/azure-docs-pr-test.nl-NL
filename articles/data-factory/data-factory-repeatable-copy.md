---
title: Herhaalbare kopie in Azure Data Factory | Microsoft Docs
description: "Informatie over het voorkomen van duplicaten, ondanks dat is meer dan één keer worden uitgevoerd in een segment dat gegevens worden gekopieerd."
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
ms.openlocfilehash: 5b88a235915bf35fec701eee4a5f80beb4a67632
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="5bff5-103">Herhaalbare kopie in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5bff5-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="5bff5-104">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="5bff5-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="5bff5-105">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="5bff5-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="5bff5-106">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5bff5-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="5bff5-107">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="5bff5-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="5bff5-108">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bff5-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="5bff5-109">De volgende voorbeelden zijn voor Azure SQL, maar zijn van toepassing op een gegevensopslag die ondersteuning biedt voor rechthoekige gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="5bff5-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="5bff5-110">Wellicht hebt u om aan te passen de **type** van bron- en de **query** eigenschap (bijvoorbeeld: query in plaats van sqlReaderQuery) voor de gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="5bff5-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="5bff5-111">Normaal gesproken bij het lezen van relationele winkels, wilt u lezen alleen de gegevens die overeenkomt met dat segment.</span><span class="sxs-lookup"><span data-stu-id="5bff5-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="5bff5-112">Een manier om dit te doen zou met behulp van de WindowStart en WindowEnd systeemvariabelen beschikbaar in Azure Data Factory zijn.</span><span class="sxs-lookup"><span data-stu-id="5bff5-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="5bff5-113">Meer informatie over de variabelen en functies in Azure Data Factory hier in de [Azure Data Factory - functies en systeemvariabelen](data-factory-functions-variables.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="5bff5-114">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5bff5-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="5bff5-115">Deze query leest de gegevens die in het segment duur bereik (WindowStart -> WindowEnd) uit de tabel MijnTabel valt.</span><span class="sxs-lookup"><span data-stu-id="5bff5-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="5bff5-116">Opnieuw uitvoeren van dit segment zou ook altijd voor zorgen dat dezelfde gegevens gelezen is.</span><span class="sxs-lookup"><span data-stu-id="5bff5-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="5bff5-117">In andere gevallen wilt lezen van de gehele tabel en de sqlReaderQuery kan als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="5bff5-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="5bff5-118">Herhaalbare schrijfbewerking naar SqlSink</span><span class="sxs-lookup"><span data-stu-id="5bff5-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="5bff5-119">Bij het kopiëren van gegevens naar **Azure SQL/SQL-Server** uit andere gegevensarchieven, moet u rekening moet houden herhaalbaarheid om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="5bff5-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="5bff5-120">Bij het kopiëren van gegevens naar Azure SQL/SQL Server-Database, de kopieeractiviteit worden gegevens toegevoegd aan de tabel sink standaard.</span><span class="sxs-lookup"><span data-stu-id="5bff5-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="5bff5-121">Stel, u gegevens wilt kopiëren uit een CSV (door komma's gescheiden waarden)-bestand met twee records aan de volgende tabel in een Azure SQL/SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="5bff5-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="5bff5-122">Wanneer een segment wordt uitgevoerd, worden de twee records gekopieerd naar de SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="5bff5-123">Stel dat u fouten gevonden in de bron-bestand en de hoeveelheid omlaag buis uit 2 tot 4 bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5bff5-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="5bff5-124">Als u het gegevenssegment handmatig opnieuw voor deze periode, vindt u twee nieuwe records die zijn toegevoegd aan Azure SQL/SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="5bff5-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="5bff5-125">In dit voorbeeld wordt ervan uitgegaan dat geen van de kolommen in de tabel de primary key-beperking heeft.</span><span class="sxs-lookup"><span data-stu-id="5bff5-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5bff5-126">Om te voorkomen dat dit probleem, moet u UPSERT semantiek opgeven met behulp van een van de volgende twee mechanismen:</span><span class="sxs-lookup"><span data-stu-id="5bff5-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="5bff5-127">Methode 1: met behulp van sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="5bff5-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="5bff5-128">U kunt de **sqlWriterCleanupScript** eigenschap opschonen van gegevens uit de tabel sink voordat de gegevens worden ingevoegd wanneer een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bff5-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="5bff5-129">Wanneer een segment wordt uitgevoerd, wordt het script voor opschoning eerst uitvoeren om gegevens die overeenkomt met het segment uit de SQL-tabel te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5bff5-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="5bff5-130">De kopieeractiviteit voegt vervolgens de gegevens in de SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="5bff5-131">Als het segment opnieuw, de hoeveelheid wordt bijgewerkt naar wens.</span><span class="sxs-lookup"><span data-stu-id="5bff5-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5bff5-132">Stel dat de platte was is verwijderd uit de oorspronkelijke csv.</span><span class="sxs-lookup"><span data-stu-id="5bff5-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="5bff5-133">Vervolgens het segment opnieuw uit te voeren, zou het volgende resultaat opleveren:</span><span class="sxs-lookup"><span data-stu-id="5bff5-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="5bff5-134">Het script voor opschoning van voor het verwijderen van de bijbehorende gegevens voor dat segment hebt uitgevoerd met de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="5bff5-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="5bff5-135">Vervolgens wordt de invoer uit de csv lezen (die vervolgens bevat slechts één record) en het ingevoegd in de tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="5bff5-136">Methode 2: met behulp van sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="5bff5-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5bff5-137">SliceIdentifierColumnName wordt momenteel niet ondersteund voor Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5bff5-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="5bff5-138">De tweede methode om het bereiken van herhaalbaarheid is door een specifieke kolom (sliceIdentifierColumnName) in de doel-tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="5bff5-139">In deze kolom zou worden gebruikt door Azure Data Factory om te controleren of dat de bron- en doelserver gesynchroniseerd blijven.</span><span class="sxs-lookup"><span data-stu-id="5bff5-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="5bff5-140">Deze methode werkt wanneer er flexibiliteit bij het definiëren van het schema van de SQL-tabel doel of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5bff5-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="5bff5-141">In deze kolom wordt gebruikt door Azure Data Factory voor herhaalbaarheid doeleinden en in het proces Azure Data Factory maakt geen eventuele wijzigingen in het schema met de tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="5bff5-142">Manier voor het gebruik van deze benadering:</span><span class="sxs-lookup"><span data-stu-id="5bff5-142">Way to use this approach:</span></span>

1. <span data-ttu-id="5bff5-143">Een kolom van het type definieert **binair (32)** in de doel-SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="5bff5-144">Er mag geen beperkingen voor deze kolom.</span><span class="sxs-lookup"><span data-stu-id="5bff5-144">There should be no constraints on this column.</span></span> <span data-ttu-id="5bff5-145">Laten we in deze kolom als AdfSliceIdentifier naam voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5bff5-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="5bff5-146">Brontabel:</span><span class="sxs-lookup"><span data-stu-id="5bff5-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="5bff5-147">Doeltabel:</span><span class="sxs-lookup"><span data-stu-id="5bff5-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="5bff5-148">Gebruik deze als volgt in de kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="5bff5-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="5bff5-149">Azure Data Factory vult deze kolom aan de hand van de noodzaak om te controleren of dat de bron- en doelserver gesynchroniseerd blijven.</span><span class="sxs-lookup"><span data-stu-id="5bff5-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="5bff5-150">De waarden van deze kolom mag niet worden gebruikt buiten deze context.</span><span class="sxs-lookup"><span data-stu-id="5bff5-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="5bff5-151">Net als bij mechanisme 1, Kopieeractiviteit ruimt automatisch de gegevens voor het opgegeven segment van de doel-SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="5bff5-152">Vervolgens worden ingevoegd gegevens uit de gegevensbron in de doeltabel.</span><span class="sxs-lookup"><span data-stu-id="5bff5-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5bff5-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5bff5-153">Next steps</span></span>
<span data-ttu-id="5bff5-154">Bekijk de volgende connector artikelen die voor volledige JSON-voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="5bff5-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="5bff5-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5bff5-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="5bff5-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5bff5-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="5bff5-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="5bff5-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)