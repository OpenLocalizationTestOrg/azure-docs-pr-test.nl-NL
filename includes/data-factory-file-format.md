## <a name="specifying-formats"></a><span data-ttu-id="ead5a-101">Indelingen opgeven</span><span class="sxs-lookup"><span data-stu-id="ead5a-101">Specifying formats</span></span>
<span data-ttu-id="ead5a-102">Azure Data Factory ondersteunt de volgende bestandsindelingen:</span><span class="sxs-lookup"><span data-stu-id="ead5a-102">Azure Data Factory supports the following format types:</span></span>

* [<span data-ttu-id="ead5a-103">Tekstindeling</span><span class="sxs-lookup"><span data-stu-id="ead5a-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="ead5a-104">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="ead5a-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="ead5a-105">Avro-indeling</span><span class="sxs-lookup"><span data-stu-id="ead5a-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="ead5a-106">ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="ead5a-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="ead5a-107">Parquet-indeling</span><span class="sxs-lookup"><span data-stu-id="ead5a-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="ead5a-108">TextFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="ead5a-108">Specifying TextFormat</span></span>
<span data-ttu-id="ead5a-109">Als u de tekstbestanden wilt parseren of de gegevens in tekstindeling wilt schrijven, stelt u de eigenschap `format` `type` in op **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span></span> <span data-ttu-id="ead5a-110">U kunt ook de volgende **optionele** eigenschappen opgeven in het gedeelte `format`.</span><span class="sxs-lookup"><span data-stu-id="ead5a-110">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="ead5a-111">Raadpleeg het gedeelte [TextFormat-voorbeeld](#textformat-example) voor configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="ead5a-111">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="ead5a-112">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ead5a-112">Property</span></span> | <span data-ttu-id="ead5a-113">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ead5a-113">Description</span></span> | <span data-ttu-id="ead5a-114">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="ead5a-114">Allowed values</span></span> | <span data-ttu-id="ead5a-115">Vereist</span><span class="sxs-lookup"><span data-stu-id="ead5a-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ead5a-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="ead5a-116">columnDelimiter</span></span> |<span data-ttu-id="ead5a-117">Het teken dat wordt gebruikt voor het scheiden van kolommen in een bestand.</span><span class="sxs-lookup"><span data-stu-id="ead5a-117">The character used to separate columns in a file.</span></span> <span data-ttu-id="ead5a-118">U kunt overwegen om een zeldzaam niet-afdrukbaar teken te gebruiken dat waarschijnlijk niet in uw gegevens bestaat: bijvoorbeeld '\u0001', dat het begin van een kop aangeeft.</span><span class="sxs-lookup"><span data-stu-id="ead5a-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="ead5a-119">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ead5a-119">Only one character is allowed.</span></span> <span data-ttu-id="ead5a-120">De **standaardwaarde** is een **komma (',')**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-120">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="ead5a-121">Raadpleeg voor het gebruik van een Unicode-teken [Unicode-tekens](https://en.wikipedia.org/wiki/List_of_Unicode_characters) om de overeenkomstige code op te halen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="ead5a-122">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-122">No</span></span> |
| <span data-ttu-id="ead5a-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="ead5a-123">rowDelimiter</span></span> |<span data-ttu-id="ead5a-124">Het teken dat wordt gebruikt voor het scheiden van rijen in een bestand.</span><span class="sxs-lookup"><span data-stu-id="ead5a-124">The character used to separate rows in a file.</span></span> |<span data-ttu-id="ead5a-125">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ead5a-125">Only one character is allowed.</span></span> <span data-ttu-id="ead5a-126">De **standaardwaarde** is een van de volgende leeswaarden **['\r\n', '\r', '\n']** en de schrijfwaarde **'\r\n'**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="ead5a-127">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-127">No</span></span> |
| <span data-ttu-id="ead5a-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="ead5a-128">escapeChar</span></span> |<span data-ttu-id="ead5a-129">Dit speciale teken wordt gebruikt om een scheidingsteken voor kolommen van de inhoud van het invoerbestand om te zetten.</span><span class="sxs-lookup"><span data-stu-id="ead5a-129">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="ead5a-130">Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven.</span><span class="sxs-lookup"><span data-stu-id="ead5a-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="ead5a-131">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ead5a-131">Only one character is allowed.</span></span> <span data-ttu-id="ead5a-132">Er is geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="ead5a-132">No default value.</span></span> <br/><br/><span data-ttu-id="ead5a-133">Voorbeeld: als u kolommen scheidt met komma's (', '), maar u het kommateken in een tekst wilt gebruiken (voorbeeld: 'Hallo, wereld'), kunt u '$' als het omzettingsteken opgeven en in de bron de tekenreeks 'Hallo$, wereld' gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ead5a-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="ead5a-134">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-134">No</span></span> |
| <span data-ttu-id="ead5a-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="ead5a-135">quoteChar</span></span> |<span data-ttu-id="ead5a-136">Het teken dat wordt gebruikt om een tekenreekswaarde te citeren.</span><span class="sxs-lookup"><span data-stu-id="ead5a-136">The character used to quote a string value.</span></span> <span data-ttu-id="ead5a-137">De scheidingstekens voor kolommen en rijen binnen de aanhalingstekens worden beschouwd als onderdeel van de tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="ead5a-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="ead5a-138">Deze eigenschap is van toepassing op gegevenssets voor invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ead5a-138">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="ead5a-139">Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven.</span><span class="sxs-lookup"><span data-stu-id="ead5a-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="ead5a-140">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ead5a-140">Only one character is allowed.</span></span> <span data-ttu-id="ead5a-141">Er is geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="ead5a-141">No default value.</span></span> <br/><br/><span data-ttu-id="ead5a-142">Voorbeeld: als u kolommen scheidt met komma's (', '), maar u het kommateken in een tekst wilt gebruiken (voorbeeld: <Hallo, wereld>), kunt u " (dubbel aanhalingsteken) als het aanhalingsteken opgeven en de tekenreeks "Hallo, wereld" in de bron gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ead5a-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="ead5a-143">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-143">No</span></span> |
| <span data-ttu-id="ead5a-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="ead5a-144">nullValue</span></span> |<span data-ttu-id="ead5a-145">Een of meer tekens die worden gebruikt om een null-waarde te vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-145">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="ead5a-146">Een of meer tekens.</span><span class="sxs-lookup"><span data-stu-id="ead5a-146">One or more characters.</span></span> <span data-ttu-id="ead5a-147">De **standaardwaarden** zijn **'\N' en 'NULL'** voor lezen en **'\N'** voor schrijven.</span><span class="sxs-lookup"><span data-stu-id="ead5a-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="ead5a-148">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-148">No</span></span> |
| <span data-ttu-id="ead5a-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="ead5a-149">encodingName</span></span> |<span data-ttu-id="ead5a-150">Geef de coderingsnaam op.</span><span class="sxs-lookup"><span data-stu-id="ead5a-150">Specify the encoding name.</span></span> |<span data-ttu-id="ead5a-151">Een geldige coderingsnaam.</span><span class="sxs-lookup"><span data-stu-id="ead5a-151">A valid encoding name.</span></span> <span data-ttu-id="ead5a-152">Zie [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="ead5a-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="ead5a-153">Voorbeeld: windows 1250 of shift_jis.</span><span class="sxs-lookup"><span data-stu-id="ead5a-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="ead5a-154">De **standaardwaarde** is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-154">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="ead5a-155">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-155">No</span></span> |
| <span data-ttu-id="ead5a-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="ead5a-156">firstRowAsHeader</span></span> |<span data-ttu-id="ead5a-157">Hiermee geeft u op of de eerste rij als een header moet worden gezien.</span><span class="sxs-lookup"><span data-stu-id="ead5a-157">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="ead5a-158">Bij een gegevensset voor invoer leest Data Factory de eerste rij als een header.</span><span class="sxs-lookup"><span data-stu-id="ead5a-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="ead5a-159">Bij een gegevensset voor uitvoer schrijft Data Factory de eerste rij als een header.</span><span class="sxs-lookup"><span data-stu-id="ead5a-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="ead5a-160">Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="ead5a-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="ead5a-161">True</span><span class="sxs-lookup"><span data-stu-id="ead5a-161">True</span></span><br/><span data-ttu-id="ead5a-162">**False (standaard)**</span><span class="sxs-lookup"><span data-stu-id="ead5a-162">**False (default)**</span></span> |<span data-ttu-id="ead5a-163">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-163">No</span></span> |
| <span data-ttu-id="ead5a-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="ead5a-164">skipLineCount</span></span> |<span data-ttu-id="ead5a-165">Geeft het aantal rijen aan dat moet worden overgeslagen bij het lezen van gegevens in invoerbestanden.</span><span class="sxs-lookup"><span data-stu-id="ead5a-165">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="ead5a-166">Als zowel skipLineCount als firstRowAsHeader is opgegeven, worden de regels eerst overgeslagen en wordt de headerinformatie gelezen uit het invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="ead5a-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="ead5a-167">Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="ead5a-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="ead5a-168">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="ead5a-168">Integer</span></span> |<span data-ttu-id="ead5a-169">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-169">No</span></span> |
| <span data-ttu-id="ead5a-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="ead5a-170">treatEmptyAsNull</span></span> |<span data-ttu-id="ead5a-171">Hiermee geeft u aan of null of lege tekenreeks moeten worden behandeld als een null-waarde bij het lezen van gegevens uit een invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="ead5a-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="ead5a-172">**True (standaard)**</span><span class="sxs-lookup"><span data-stu-id="ead5a-172">**True (default)**</span></span><br/><span data-ttu-id="ead5a-173">False</span><span class="sxs-lookup"><span data-stu-id="ead5a-173">False</span></span> |<span data-ttu-id="ead5a-174">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="ead5a-175">Voorbeeld van TextFormat</span><span class="sxs-lookup"><span data-stu-id="ead5a-175">TextFormat example</span></span>
<span data-ttu-id="ead5a-176">Het volgende voorbeeld toont een aantal van de eigenschappen van de TextFormat-indeling.</span><span class="sxs-lookup"><span data-stu-id="ead5a-176">The following sample shows some of the format properties for TextFormat.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="ead5a-177">Gebruik een `escapeChar` in plaats van `quoteChar`, vervang de regel door `quoteChar` met het volgende escapeChar:</span><span class="sxs-lookup"><span data-stu-id="ead5a-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="ead5a-178">Scenario's voor het gebruik van firstRowAsHeader en skipLineCount</span><span class="sxs-lookup"><span data-stu-id="ead5a-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="ead5a-179">U kopieert vanuit een bron die geen bestand is, naar een tekstbestand en wilt een headerregel toevoegen die de metagegevens van het schema bevat (bijvoorbeeld: SQL-schema).</span><span class="sxs-lookup"><span data-stu-id="ead5a-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="ead5a-180">Geef voor `firstRowAsHeader` 'True' op in de uitvoergegevensset voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="ead5a-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="ead5a-181">U wilt kopiëren vanuit een tekstbestand met een headerregel naar een sink die geen bestand is en wilt die regel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="ead5a-182">Geef voor `firstRowAsHeader` 'True' op in de invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="ead5a-182">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="ead5a-183">U wilt kopiëren uit een tekstbestand en wilt een paar regels aan het begin overslaan die geen gegevens of headerinformatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="ead5a-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="ead5a-184">Geef `skipLineCount` op om aan te geven hoeveel regels er moeten worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="ead5a-185">Als de rest van het bestand een headerregel bevat, kunt u ook `firstRowAsHeader` opgeven.</span><span class="sxs-lookup"><span data-stu-id="ead5a-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="ead5a-186">Als zowel `skipLineCount` als `firstRowAsHeader` is opgegeven, worden de regels eerst overgeslagen en wordt de headerinformatie gelezen uit het invoerbestand</span><span class="sxs-lookup"><span data-stu-id="ead5a-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="ead5a-187">JsonFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="ead5a-187">Specifying JsonFormat</span></span>
<span data-ttu-id="ead5a-188">Naar **als JSON-bestanden voor importeren/exporteren-is naar/van Azure DB die Cosmos**, Zie [voor importeren/exporteren JSON-documenten](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) sectie in de Azure DB die Cosmos-connector met details.</span><span class="sxs-lookup"><span data-stu-id="ead5a-188">To **import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in the Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="ead5a-189">Als u de JSON-bestanden wilt parseren of de gegevens in JSON-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span></span> <span data-ttu-id="ead5a-190">U kunt ook de volgende **optionele** eigenschappen opgeven in het gedeelte `format`.</span><span class="sxs-lookup"><span data-stu-id="ead5a-190">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="ead5a-191">Zie het gedeelte [JsonFormat-voorbeeld](#jsonformat-example) voor configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="ead5a-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="ead5a-192">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ead5a-192">Property</span></span> | <span data-ttu-id="ead5a-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ead5a-193">Description</span></span> | <span data-ttu-id="ead5a-194">Vereist</span><span class="sxs-lookup"><span data-stu-id="ead5a-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ead5a-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="ead5a-195">filePattern</span></span> |<span data-ttu-id="ead5a-196">Hiermee geeft u het patroon aan van gegevens die zijn opgeslagen in elk JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="ead5a-196">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="ead5a-197">Toegestane waarden zijn **setOfObjects** en **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="ead5a-198">De **standaardwaarde** is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-198">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="ead5a-199">Zie het gedeelte [JSON-bestandpatronen](#json-file-patterns) voor meer informatie over deze patronen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="ead5a-200">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-200">No</span></span> |
| <span data-ttu-id="ead5a-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="ead5a-201">jsonNodeReference</span></span> | <span data-ttu-id="ead5a-202">Als u wilt bladeren en gegevens wilt ophalen uit de objecten in een matrixveld met hetzelfde patroon, geeft u het JSON-pad van die matrix op.</span><span class="sxs-lookup"><span data-stu-id="ead5a-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="ead5a-203">Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="ead5a-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="ead5a-204">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-204">No</span></span> |
| <span data-ttu-id="ead5a-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="ead5a-205">jsonPathDefinition</span></span> | <span data-ttu-id="ead5a-206">Hiermee geeft u de JSON-padexpressie aan voor elke kolomtoewijzing met een aangepaste kolomnaam (begin met een kleine letter).</span><span class="sxs-lookup"><span data-stu-id="ead5a-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="ead5a-207">Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. U kunt gegevens ophalen uit het object of een matrix.</span><span class="sxs-lookup"><span data-stu-id="ead5a-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="ead5a-208">Voor velden onder het hoofdobject begint u met root $; voor velden binnen de matrix die is gekozen door de eigenschap `jsonNodeReference`, begint u vanaf het element van de matrix.</span><span class="sxs-lookup"><span data-stu-id="ead5a-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="ead5a-209">Zie het gedeelte [JsonFormat-voorbeeld](#jsonformat-example) voor configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="ead5a-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="ead5a-210">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-210">No</span></span> |
| <span data-ttu-id="ead5a-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="ead5a-211">encodingName</span></span> |<span data-ttu-id="ead5a-212">Geef de coderingsnaam op.</span><span class="sxs-lookup"><span data-stu-id="ead5a-212">Specify the encoding name.</span></span> <span data-ttu-id="ead5a-213">Zie voor de lijst met geldige namen voor versleuteling [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="ead5a-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="ead5a-214">Bijvoorbeeld: windows 1250 of shift_jis.</span><span class="sxs-lookup"><span data-stu-id="ead5a-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="ead5a-215">De **standaardwaarde** is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-215">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="ead5a-216">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-216">No</span></span> |
| <span data-ttu-id="ead5a-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="ead5a-217">nestingSeparator</span></span> |<span data-ttu-id="ead5a-218">Teken dat wordt gebruikt voor het scheiden van geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="ead5a-218">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="ead5a-219">De standaardwaarde is '.' (punt).</span><span class="sxs-lookup"><span data-stu-id="ead5a-219">The default value is '.' (dot).</span></span> |<span data-ttu-id="ead5a-220">Nee</span><span class="sxs-lookup"><span data-stu-id="ead5a-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="ead5a-221">JSON-bestandpatronen</span><span class="sxs-lookup"><span data-stu-id="ead5a-221">JSON file patterns</span></span>

<span data-ttu-id="ead5a-222">Kopieerbewerkingen kunnen onderstaande patronen van JSON-bestanden parseren:</span><span class="sxs-lookup"><span data-stu-id="ead5a-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="ead5a-223">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="ead5a-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="ead5a-224">Elk bestand bevat één object of meerdere door regels gescheiden/samengevoegde objecten.</span><span class="sxs-lookup"><span data-stu-id="ead5a-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="ead5a-225">Wanneer deze optie is geselecteerd in een uitvoergegevensset, produceert de kopieerbewerking een enkel JSON-bestand met één object per regel (door regels gescheiden).</span><span class="sxs-lookup"><span data-stu-id="ead5a-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="ead5a-226">**voorbeeld van JSON-bestand met één object**</span><span class="sxs-lookup"><span data-stu-id="ead5a-226">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="ead5a-227">**voorbeeld van JSON-bestand dat door regels is gescheiden**</span><span class="sxs-lookup"><span data-stu-id="ead5a-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="ead5a-228">**voorbeeld van JSON-bestand met samengevoegde objecten**</span><span class="sxs-lookup"><span data-stu-id="ead5a-228">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="ead5a-229">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="ead5a-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="ead5a-230">Elk bestand bevat een matrix met objecten.</span><span class="sxs-lookup"><span data-stu-id="ead5a-230">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

#### <a name="jsonformat-example"></a><span data-ttu-id="ead5a-231">Voorbeeld van JsonFormat</span><span class="sxs-lookup"><span data-stu-id="ead5a-231">JsonFormat example</span></span>

<span data-ttu-id="ead5a-232">**Voorbeeld 1: gegevens uit JSON-bestanden kopiëren**</span><span class="sxs-lookup"><span data-stu-id="ead5a-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="ead5a-233">Hieronder ziet u twee soorten voorbeelden van het kopiëren van gegevens uit JSON-bestanden en de algemene punten om te onthouden:</span><span class="sxs-lookup"><span data-stu-id="ead5a-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span></span>

<span data-ttu-id="ead5a-234">**Voorbeeld 1: gegevens ophalen uit object en matrix**</span><span class="sxs-lookup"><span data-stu-id="ead5a-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="ead5a-235">In dit voorbeeld kunt u verwachten dat één JSON-hoofdobject wordt toegewezen aan één record in het tabelresultaat.</span><span class="sxs-lookup"><span data-stu-id="ead5a-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="ead5a-236">Als u een JSON-bestand hebt met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="ead5a-236">If you have a JSON file with the following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="ead5a-237">en u wilt het kopiëren naar een Azure SQL-tabel in de volgende indeling door gegevens te extraheren uit de objecten en matrix:</span><span class="sxs-lookup"><span data-stu-id="ead5a-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="ead5a-238">id</span><span class="sxs-lookup"><span data-stu-id="ead5a-238">id</span></span> | <span data-ttu-id="ead5a-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="ead5a-239">deviceType</span></span> | <span data-ttu-id="ead5a-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="ead5a-240">targetResourceType</span></span> | <span data-ttu-id="ead5a-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="ead5a-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="ead5a-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="ead5a-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ead5a-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="ead5a-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="ead5a-244">Pc</span><span class="sxs-lookup"><span data-stu-id="ead5a-244">PC</span></span> | <span data-ttu-id="ead5a-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="ead5a-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="ead5a-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="ead5a-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="ead5a-247">13/1/2017 11:24:37 uur</span><span class="sxs-lookup"><span data-stu-id="ead5a-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="ead5a-248">De invoergegevensset met het type **JsonFormat** wordt als volgt gedefinieerd: (gedeeltelijke definitie met alleen belangrijke onderdelen).</span><span class="sxs-lookup"><span data-stu-id="ead5a-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="ead5a-249">Met name:</span><span class="sxs-lookup"><span data-stu-id="ead5a-249">More specifically:</span></span>

- <span data-ttu-id="ead5a-250">Het gedeelte `structure` definieert de aangepaste kolomnamen en het bijbehorende gegevenstype tijdens het converteren van gegevens in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="ead5a-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="ead5a-251">Dit gedeelte is **optioneel**, tenzij u kolommen moet toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-251">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="ead5a-252">Zie het gedeelte [Een structuurdefinitie opgeven voor rechthoekige gegevenssets](#specifying-structure-definition-for-rectangular-datasets) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ead5a-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="ead5a-253">Met `jsonPathDefinition` geeft u het JSON-pad op voor elke kolom die aangeeft waar de gegevens moeten worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ead5a-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="ead5a-254">Voor het kopiëren van gegevens vanuit een matrix kunt u **array[x].property** gebruiken om de waarde van de opgegeven eigenschap op te halen uit het xth-object. U kunt ook **array[*].property** gebruiken om de waarde van een object met deze eigenschap te vinden.</span><span class="sxs-lookup"><span data-stu-id="ead5a-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="ead5a-255">**Voorbeeld 2: meerdere objecten met hetzelfde patroon uit een matrix toepassen**</span><span class="sxs-lookup"><span data-stu-id="ead5a-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="ead5a-256">In dit voorbeeld probeert u een JSON-hoofdobject te transformeren naar meerdere records in een tabelresultaat.</span><span class="sxs-lookup"><span data-stu-id="ead5a-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="ead5a-257">Als u een JSON-bestand hebt met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="ead5a-257">If you have a JSON file with the following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="ead5a-258">en u wilt het kopiëren naar een Azure SQL-tabel in de volgende indeling, door de gegevens binnen de matrix af te vlakken en samen te voegen met de algemene root-gegevens:</span><span class="sxs-lookup"><span data-stu-id="ead5a-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="ead5a-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="ead5a-259">ordernumber</span></span> | <span data-ttu-id="ead5a-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="ead5a-260">orderdate</span></span> | <span data-ttu-id="ead5a-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="ead5a-261">order_pd</span></span> | <span data-ttu-id="ead5a-262">order_price</span><span class="sxs-lookup"><span data-stu-id="ead5a-262">order_price</span></span> | <span data-ttu-id="ead5a-263">city</span><span class="sxs-lookup"><span data-stu-id="ead5a-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ead5a-264">01</span><span class="sxs-lookup"><span data-stu-id="ead5a-264">01</span></span> | <span data-ttu-id="ead5a-265">20170122</span><span class="sxs-lookup"><span data-stu-id="ead5a-265">20170122</span></span> | <span data-ttu-id="ead5a-266">P1</span><span class="sxs-lookup"><span data-stu-id="ead5a-266">P1</span></span> | <span data-ttu-id="ead5a-267">23</span><span class="sxs-lookup"><span data-stu-id="ead5a-267">23</span></span> | <span data-ttu-id="ead5a-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="ead5a-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="ead5a-269">01</span><span class="sxs-lookup"><span data-stu-id="ead5a-269">01</span></span> | <span data-ttu-id="ead5a-270">20170122</span><span class="sxs-lookup"><span data-stu-id="ead5a-270">20170122</span></span> | <span data-ttu-id="ead5a-271">P2</span><span class="sxs-lookup"><span data-stu-id="ead5a-271">P2</span></span> | <span data-ttu-id="ead5a-272">13</span><span class="sxs-lookup"><span data-stu-id="ead5a-272">13</span></span> | <span data-ttu-id="ead5a-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="ead5a-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="ead5a-274">01</span><span class="sxs-lookup"><span data-stu-id="ead5a-274">01</span></span> | <span data-ttu-id="ead5a-275">20170122</span><span class="sxs-lookup"><span data-stu-id="ead5a-275">20170122</span></span> | <span data-ttu-id="ead5a-276">P3</span><span class="sxs-lookup"><span data-stu-id="ead5a-276">P3</span></span> | <span data-ttu-id="ead5a-277">231</span><span class="sxs-lookup"><span data-stu-id="ead5a-277">231</span></span> | <span data-ttu-id="ead5a-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="ead5a-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="ead5a-279">De invoergegevensset met het type **JsonFormat** wordt als volgt gedefinieerd: (gedeeltelijke definitie met alleen belangrijke onderdelen).</span><span class="sxs-lookup"><span data-stu-id="ead5a-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="ead5a-280">Met name:</span><span class="sxs-lookup"><span data-stu-id="ead5a-280">More specifically:</span></span>

- <span data-ttu-id="ead5a-281">Het gedeelte `structure` definieert de aangepaste kolomnamen en het bijbehorende gegevenstype tijdens het converteren van gegevens in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="ead5a-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="ead5a-282">Dit gedeelte is **optioneel**, tenzij u kolommen moet toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-282">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="ead5a-283">Zie het gedeelte [Een structuurdefinitie opgeven voor rechthoekige gegevenssets](#specifying-structure-definition-for-rectangular-datasets) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ead5a-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="ead5a-284">Met `jsonNodeReference` geeft u aan dat moet worden gebladerd naar het object en dat er gegevens uit moeten worden opgehaald met hetzelfde patroon onder de **matrix** orderlines.</span><span class="sxs-lookup"><span data-stu-id="ead5a-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="ead5a-285">Met `jsonPathDefinition` geeft u het JSON-pad op voor elke kolom die aangeeft waar de gegevens moeten worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ead5a-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="ead5a-286">In dit voorbeeld bevinden 'ordernumber', 'orderdate' en 'city' zich onder het root-object. Het JSON-pad begint met '$.', terwijl 'order_pd' en 'order_price' worden gedefinieerd met het pad dat is afgeleid van het matrixelement zonder '$.'.</span><span class="sxs-lookup"><span data-stu-id="ead5a-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="ead5a-287">**Houd rekening met de volgende punten:**</span><span class="sxs-lookup"><span data-stu-id="ead5a-287">**Note the following points:**</span></span>

* <span data-ttu-id="ead5a-288">Als `structure` en `jsonPathDefinition` niet zijn gedefinieerd in de gegevensset van Data Factory, detecteert de kopieerbewerking het schema van het eerste object en wordt het hele object afgevlakt.</span><span class="sxs-lookup"><span data-stu-id="ead5a-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="ead5a-289">Als de JSON-invoer een matrix heeft, zet de kopieerbewerking de volledige matrix-waarde standaard om in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ead5a-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="ead5a-290">U kunt ervoor kiezen om er gegevens uit op te halen met behulp van `jsonNodeReference` en/of `jsonPathDefinition`, of deze stap over te slaan door deze niet op te geven in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="ead5a-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="ead5a-291">Als er dubbele namen op hetzelfde niveau voorkomen, gebruikt de kopieerbewerking de laatste.</span><span class="sxs-lookup"><span data-stu-id="ead5a-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="ead5a-292">Eigenschapnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="ead5a-292">Property names are case-sensitive.</span></span> <span data-ttu-id="ead5a-293">Twee eigenschappen met dezelfde naam maar met een verschil in hoofdletters en kleine letters worden behandeld als twee afzonderlijke eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="ead5a-294">**Voorbeeld 2: gegevens schrijven naar een JSON-bestand**</span><span class="sxs-lookup"><span data-stu-id="ead5a-294">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="ead5a-295">Als u de onderstaande tabel hebt in SQL-Database:</span><span class="sxs-lookup"><span data-stu-id="ead5a-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="ead5a-296">id</span><span class="sxs-lookup"><span data-stu-id="ead5a-296">id</span></span> | <span data-ttu-id="ead5a-297">order_date</span><span class="sxs-lookup"><span data-stu-id="ead5a-297">order_date</span></span> | <span data-ttu-id="ead5a-298">order_price</span><span class="sxs-lookup"><span data-stu-id="ead5a-298">order_price</span></span> | <span data-ttu-id="ead5a-299">order_by</span><span class="sxs-lookup"><span data-stu-id="ead5a-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ead5a-300">1</span><span class="sxs-lookup"><span data-stu-id="ead5a-300">1</span></span> | <span data-ttu-id="ead5a-301">20170119</span><span class="sxs-lookup"><span data-stu-id="ead5a-301">20170119</span></span> | <span data-ttu-id="ead5a-302">2000</span><span class="sxs-lookup"><span data-stu-id="ead5a-302">2000</span></span> | <span data-ttu-id="ead5a-303">David</span><span class="sxs-lookup"><span data-stu-id="ead5a-303">David</span></span> |
| <span data-ttu-id="ead5a-304">2</span><span class="sxs-lookup"><span data-stu-id="ead5a-304">2</span></span> | <span data-ttu-id="ead5a-305">20170120</span><span class="sxs-lookup"><span data-stu-id="ead5a-305">20170120</span></span> | <span data-ttu-id="ead5a-306">3500</span><span class="sxs-lookup"><span data-stu-id="ead5a-306">3500</span></span> | <span data-ttu-id="ead5a-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="ead5a-307">Patrick</span></span> |
| <span data-ttu-id="ead5a-308">3</span><span class="sxs-lookup"><span data-stu-id="ead5a-308">3</span></span> | <span data-ttu-id="ead5a-309">20170121</span><span class="sxs-lookup"><span data-stu-id="ead5a-309">20170121</span></span> | <span data-ttu-id="ead5a-310">4000</span><span class="sxs-lookup"><span data-stu-id="ead5a-310">4000</span></span> | <span data-ttu-id="ead5a-311">Jason</span><span class="sxs-lookup"><span data-stu-id="ead5a-311">Jason</span></span> |

<span data-ttu-id="ead5a-312">en voor elke record die u verwacht te schrijven naar een JSON-object in onderstaande indeling:</span><span class="sxs-lookup"><span data-stu-id="ead5a-312">and for each record, you expect to write to a JSON object in below format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="ead5a-313">De uitvoergegevensset met het type **JsonFormat** wordt als volgt gedefinieerd: (gedeeltelijke definitie met alleen belangrijke onderdelen).</span><span class="sxs-lookup"><span data-stu-id="ead5a-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="ead5a-314">Het gedeelte `structure` bepaalt met name de namen van aangepaste eigenschappen in het doelbestand, `nestingSeparator` (de standaardwaarde is '.') wordt gebruikt voor het identificeren van de nestlaag van de naam.</span><span class="sxs-lookup"><span data-stu-id="ead5a-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span></span> <span data-ttu-id="ead5a-315">Dit gedeelte is **optioneel**, tenzij u de naam van de eigenschap wilt wijzigen ten opzichte van de naam van de bronkolom of sommige eigenschappen wilt nesten.</span><span class="sxs-lookup"><span data-stu-id="ead5a-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

### <a name="specifying-avroformat"></a><span data-ttu-id="ead5a-316">AvroFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="ead5a-316">Specifying AvroFormat</span></span>
<span data-ttu-id="ead5a-317">Als u de Avro-bestanden wilt parseren of de gegevens in Avro-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="ead5a-318">U hoeft geen eigenschappen op te geven in het gedeelte Indeling binnen het gedeelte typeProperties.</span><span class="sxs-lookup"><span data-stu-id="ead5a-318">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="ead5a-319">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ead5a-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="ead5a-320">Als u de Avro-indeling wilt gebruiken in een Hive-tabel, kunt u de [Zelfstudie voor Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe) raadplegen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="ead5a-321">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="ead5a-321">Note the following points:</span></span>  

* <span data-ttu-id="ead5a-322">[Complexe gegevenstypen](http://avro.apache.org/docs/current/spec.html#schema_complex) worden niet ondersteund (records, enums, matrices, kaarten, samenvoegingen en vaste bestanden).</span><span class="sxs-lookup"><span data-stu-id="ead5a-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="ead5a-323">OrcFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="ead5a-323">Specifying OrcFormat</span></span>
<span data-ttu-id="ead5a-324">Als u de ORC-bestanden wilt parseren of de gegevens in ORC-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="ead5a-325">U hoeft geen eigenschappen op te geven in het gedeelte Indeling binnen het gedeelte typeProperties.</span><span class="sxs-lookup"><span data-stu-id="ead5a-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="ead5a-326">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ead5a-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="ead5a-327">Als u de ORC niet **ongewijzigd** kopieert tussen on-premises gegevensopslag en gegevensopslag in de cloud, moet u de JRE 8 (Java Runtime Environment) op de gatewaycomputer installeren.</span><span class="sxs-lookup"><span data-stu-id="ead5a-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="ead5a-328">Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway.</span><span class="sxs-lookup"><span data-stu-id="ead5a-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="ead5a-329">U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="ead5a-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="ead5a-330">Kies de juiste versie.</span><span class="sxs-lookup"><span data-stu-id="ead5a-330">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="ead5a-331">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="ead5a-331">Note the following points:</span></span>

* <span data-ttu-id="ead5a-332">Complexe gegevenstypen worden niet ondersteund (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="ead5a-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="ead5a-333">Een ORC-bestand heeft drie [opties voor compressie](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="ead5a-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="ead5a-334">Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="ead5a-335">Hierbij wordt de compressiecodec in de metagegevens gebruikt om de gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-335">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="ead5a-336">Bij het schrijven naar een ORC-bestand kiest Data Factory echter ZLIB, de standaardinstelling voor ORC.</span><span class="sxs-lookup"><span data-stu-id="ead5a-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="ead5a-337">Er is momenteel geen optie om dit gedrag te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="ead5a-337">Currently, there is no option to override this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="ead5a-338">ParquetFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="ead5a-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="ead5a-339">Als u de Parquet-bestanden wilt parseren of de gegevens in Parquet-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ead5a-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="ead5a-340">U hoeft geen eigenschappen op te geven in het gedeelte Indeling binnen het gedeelte typeProperties.</span><span class="sxs-lookup"><span data-stu-id="ead5a-340">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="ead5a-341">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ead5a-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="ead5a-342">Als u de Parquet niet **ongewijzigd** kopieert tussen on-premises gegevensopslag en gegevensopslag in de cloud, moet u de JRE 8 (Java Runtime Environment) op de gatewaycomputer installeren.</span><span class="sxs-lookup"><span data-stu-id="ead5a-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="ead5a-343">Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway.</span><span class="sxs-lookup"><span data-stu-id="ead5a-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="ead5a-344">U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="ead5a-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="ead5a-345">Kies de juiste versie.</span><span class="sxs-lookup"><span data-stu-id="ead5a-345">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="ead5a-346">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="ead5a-346">Note the following points:</span></span>

* <span data-ttu-id="ead5a-347">Complexe gegevenstypen worden niet ondersteund (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="ead5a-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="ead5a-348">Parquet-bestanden hebben de volgende opties voor compressie: NONE, SNAPPY, GZIP en LZO.</span><span class="sxs-lookup"><span data-stu-id="ead5a-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="ead5a-349">Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="ead5a-350">Hierbij wordt de compressiecodec in de metagegevens gebruikt om de gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="ead5a-350">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="ead5a-351">Bij het schrijven naar een Parquet-bestand kiest Data Factory echter SNAPPY, de standaardinstelling voor Parquet.</span><span class="sxs-lookup"><span data-stu-id="ead5a-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="ead5a-352">Er is momenteel geen optie om dit gedrag te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="ead5a-352">Currently, there is no option to override this behavior.</span></span>
