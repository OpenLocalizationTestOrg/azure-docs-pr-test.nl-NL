## <a name="repeatability-during-copy"></a><span data-ttu-id="fd356-101">Herhaalbaarheid tijdens het kopiëren</span><span class="sxs-lookup"><span data-stu-id="fd356-101">Repeatability during Copy</span></span>
<span data-ttu-id="fd356-102">Wanneer een behoeften tookeep herhaalbaarheid kopiëren van gegevens tooAzure SQL/SQL-Server van andere gegevens opslaat in gedachten tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="fd356-102">When copying data tooAzure SQL/SQL Server from other data stores one needs tookeep repeatability in mind tooavoid unintended outcomes.</span></span> 

<span data-ttu-id="fd356-103">Bij het kopiëren van gegevens tooAzure SQL/SQL Server-Database, wordt de kopieerbewerking door standaard APPEND Hallo gegevensset toohello sink tabel standaard.</span><span class="sxs-lookup"><span data-stu-id="fd356-103">When copying data tooAzure SQL/SQL Server Database, copy activity will by default APPEND hello data set toohello sink table by default.</span></span> <span data-ttu-id="fd356-104">Bijvoorbeeld, bij het kopiëren van gegevens uit een CSV (door komma's gescheiden waarden) bestand gegevensbron met twee registreert tooAzure SQL/SQL Server-Database, is dit welke Hallo tabel lijkt:</span><span class="sxs-lookup"><span data-stu-id="fd356-104">For example, when copying data from a CSV (comma separated values data) file source containing two records tooAzure SQL/SQL Server Database, this is what hello table looks like:</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="fd356-105">Stel dat u fouten in het bronbestand als het aantal bijgewerkte Hallo omlaag buis van 2 too4 gevonden in het bronbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd356-105">Suppose you found errors in source file and updated hello quantity of Down Tube from 2 too4 in hello source file.</span></span> <span data-ttu-id="fd356-106">Als u het gegevenssegment Hallo opnieuw voor deze periode uitvoeren, vindt u twee nieuwe records tooAzure SQL/SQL Server-Database toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fd356-106">If you re-run hello data slice for that period, you’ll find two new records appended tooAzure SQL/SQL Server Database.</span></span> <span data-ttu-id="fd356-107">Hallo hieronder wordt ervan uitgegaan dat geen van de kolommen in tabel Hallo HALLO hallo primary key-beperking heeft.</span><span class="sxs-lookup"><span data-stu-id="fd356-107">hello below assumes none of hello columns in hello table have hello primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="fd356-108">tooavoid, moet u toospecify UPSERT semantiek dankzij het gebruik van een van de Hallo hieronder 2 mechanismen die hieronder vermeld.</span><span class="sxs-lookup"><span data-stu-id="fd356-108">tooavoid this, you will need toospecify UPSERT semantics by leveraging one of hello below 2 mechanisms stated below.</span></span>

> [!NOTE]
> <span data-ttu-id="fd356-109">Een segment kan automatisch worden opnieuw uitgevoerd in Azure Data Factory volgens het beleid voor opnieuw proberen Hallo opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fd356-109">A slice can be re-run automatically in Azure Data Factory as per hello retry policy specified.</span></span>
> 
> 

### <a name="mechanism-1"></a><span data-ttu-id="fd356-110">Methode 1</span><span class="sxs-lookup"><span data-stu-id="fd356-110">Mechanism 1</span></span>
<span data-ttu-id="fd356-111">U kunt gebruikmaken van **sqlWriterCleanupScript** eigenschap toofirst opschonen actie uitvoeren wanneer een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fd356-111">You can leverage **sqlWriterCleanupScript** property toofirst perform cleanup action when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="fd356-112">Hallo script voor opschoning zou worden uitgevoerd tijdens het kopiëren van een bepaald segment die Hallo gegevens uit Hallo SQL-tabel overeenkomende toothat segment verwijderen zou eerste.</span><span class="sxs-lookup"><span data-stu-id="fd356-112">hello cleanup script would be executed first during copy for a given slice which would delete hello data from hello SQL Table corresponding toothat slice.</span></span> <span data-ttu-id="fd356-113">Hallo-activiteit wordt vervolgens Hallo gegevens invoegen in Hallo SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="fd356-113">hello activity will subsequently insert hello data into hello SQL Table.</span></span> 

<span data-ttu-id="fd356-114">Als het Hallo-segment is nu opnieuw uitvoeren, dan hebt u Hallo hoeveelheid wordt bijgewerkt vindt als gewenst.</span><span class="sxs-lookup"><span data-stu-id="fd356-114">If hello slice is now re-run, then you will find hello quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="fd356-115">Stel Hallo platte was record wordt verwijderd uit de oorspronkelijke csv Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd356-115">Suppose hello Flat Washer record is removed from hello original csv.</span></span> <span data-ttu-id="fd356-116">Vervolgens resulteert opnieuw uit te voeren Hallo segment Hallo resultaat te volgen:</span><span class="sxs-lookup"><span data-stu-id="fd356-116">Then re-running hello slice would produce hello following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
<span data-ttu-id="fd356-117">Niets nieuwe had toobe gedaan.</span><span class="sxs-lookup"><span data-stu-id="fd356-117">Nothing new had toobe done.</span></span> <span data-ttu-id="fd356-118">Hallo kopieeractiviteit uitgevoerd Hallo opschonen script toodelete Hallo bijbehorende gegevens voor dit segment.</span><span class="sxs-lookup"><span data-stu-id="fd356-118">hello copy activity ran hello cleanup script toodelete hello corresponding data for that slice.</span></span> <span data-ttu-id="fd356-119">En vervolgens het Hallo-invoer wordt gelezen uit Hallo csv (inhoudt vervolgens slechts 1 record) en ingevoegd Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="fd356-119">Then it read hello input from hello csv (which then contained only 1 record) and inserted it into hello Table.</span></span> 

### <a name="mechanism-2"></a><span data-ttu-id="fd356-120">Mechanisme 2</span><span class="sxs-lookup"><span data-stu-id="fd356-120">Mechanism 2</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fd356-121">sliceIdentifierColumnName wordt niet ondersteund voor Azure SQL Data Warehouse op dit moment.</span><span class="sxs-lookup"><span data-stu-id="fd356-121">sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse at this time.</span></span> 

<span data-ttu-id="fd356-122">Een ander mechanisme tooachieve herhaalbaarheid is door een specifieke kolom (**sliceIdentifierColumnName**) in Hallo doel tabel.</span><span class="sxs-lookup"><span data-stu-id="fd356-122">Another mechanism tooachieve repeatability is by having a dedicated column (**sliceIdentifierColumnName**) in hello target Table.</span></span> <span data-ttu-id="fd356-123">In deze kolom wordt gebruikt door Azure Data Factory tooensure Hallo bron- en doelserver gesynchroniseerd blijven.</span><span class="sxs-lookup"><span data-stu-id="fd356-123">This column would be used by Azure Data Factory tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="fd356-124">Deze methode werkt wanneer er flexibiliteit bij het definiëren van de SQL-tabel doelschema Hallo of wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fd356-124">This approach works when there is flexibility in changing or defining hello destination SQL Table schema.</span></span> 

<span data-ttu-id="fd356-125">In deze kolom wordt gebruikt door Azure Data Factory voor herhaalbaarheid doeleinden en in proces hello Azure Data Factory niet brengt geen schema toohello tabel wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="fd356-125">This column would be used by Azure Data Factory for repeatability purposes and in hello process Azure Data Factory will not make any schema changes toohello Table.</span></span> <span data-ttu-id="fd356-126">Manier toouse deze benadering:</span><span class="sxs-lookup"><span data-stu-id="fd356-126">Way toouse this approach:</span></span>

1. <span data-ttu-id="fd356-127">Een kolom van het type binaire (32) definiëren in Hallo doel-SQL-tabel.</span><span class="sxs-lookup"><span data-stu-id="fd356-127">Define a column of type binary (32) in hello destination SQL Table.</span></span> <span data-ttu-id="fd356-128">Er mag geen beperkingen voor deze kolom.</span><span class="sxs-lookup"><span data-stu-id="fd356-128">There should be no constraints on this column.</span></span> <span data-ttu-id="fd356-129">Laten we in deze kolom als 'ColumnForADFuseOnly' naam voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fd356-129">Let's name this column as ‘ColumnForADFuseOnly’ for this example.</span></span>
2. <span data-ttu-id="fd356-130">Gebruik deze als volgt in Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="fd356-130">Use it in hello copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

<span data-ttu-id="fd356-131">Azure Data Factory wordt gevuld in deze kolom aan de hand van de noodzaak tooensure Hallo bron- en doelserver gesynchroniseerd blijven.</span><span class="sxs-lookup"><span data-stu-id="fd356-131">Azure Data Factory will populate this column as per its need tooensure hello source and destination stay synchronized.</span></span> <span data-ttu-id="fd356-132">Hallo-waarden van deze kolom mag niet buiten deze context worden gebruikt door de gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd356-132">hello values of this column should not be used outside of this context by hello user.</span></span> 

<span data-ttu-id="fd356-133">Vergelijkbare toomechanism 1, Kopieeractiviteit wordt automatisch eerste opschonen Hallo-gegevens voor Hallo opgegeven segment van Hallo doel-SQL-tabel en voer de kopieeractiviteit Hallo normaal tooinsert Hallo gegevens uit de bron toodestination voor dit segment.</span><span class="sxs-lookup"><span data-stu-id="fd356-133">Similar toomechanism 1, Copy Activity will automatically first clean up hello data for hello given slice from hello destination SQL Table and then run hello copy activity normally tooinsert hello data from source toodestination for that slice.</span></span> 

