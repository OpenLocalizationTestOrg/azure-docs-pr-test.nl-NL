## <a name="specifying-formats"></a><span data-ttu-id="db42a-101">Indelingen opgeven</span><span class="sxs-lookup"><span data-stu-id="db42a-101">Specifying formats</span></span>
<span data-ttu-id="db42a-102">Azure Data Factory ondersteunt Hallo indelingstypen te volgen:</span><span class="sxs-lookup"><span data-stu-id="db42a-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="db42a-103">Tekstindeling</span><span class="sxs-lookup"><span data-stu-id="db42a-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="db42a-104">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="db42a-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="db42a-105">Avro-indeling</span><span class="sxs-lookup"><span data-stu-id="db42a-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="db42a-106">ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="db42a-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="db42a-107">Parquet-indeling</span><span class="sxs-lookup"><span data-stu-id="db42a-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="db42a-108">TextFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="db42a-108">Specifying TextFormat</span></span>
<span data-ttu-id="db42a-109">Als u wilt dat tooparse Hallo tekstbestanden of Hallo-gegevens in tekstindeling schrijven, ingesteld Hallo `format` `type` eigenschap te**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="db42a-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="db42a-110">U kunt ook opgeven Hallo volgende **optionele** eigenschappen in Hallo `format` sectie.</span><span class="sxs-lookup"><span data-stu-id="db42a-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="db42a-111">Zie [TextFormat voorbeeld](#textformat-example) sectie over het tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="db42a-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="db42a-112">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="db42a-112">Property</span></span> | <span data-ttu-id="db42a-113">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="db42a-113">Description</span></span> | <span data-ttu-id="db42a-114">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="db42a-114">Allowed values</span></span> | <span data-ttu-id="db42a-115">Vereist</span><span class="sxs-lookup"><span data-stu-id="db42a-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db42a-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="db42a-116">columnDelimiter</span></span> |<span data-ttu-id="db42a-117">Hallo teken tooseparate kolommen in een bestand gebruikt.</span><span class="sxs-lookup"><span data-stu-id="db42a-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="db42a-118">Kunt u overwegen toouse een zeldzame niet-afdrukbaar teken die waarschijnlijk niet voorkomt in uw gegevens: bijvoorbeeld '\u0001' waarmee de Start van kop (SOH) opgeven.</span><span class="sxs-lookup"><span data-stu-id="db42a-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="db42a-119">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="db42a-119">Only one character is allowed.</span></span> <span data-ttu-id="db42a-120">Hallo **standaard** waarde is **met door komma's (',')**.</span><span class="sxs-lookup"><span data-stu-id="db42a-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="db42a-121">toouse een Unicode-teken te verwijzen[Unicode-tekens](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello overeenkomstige code voor deze.</span><span class="sxs-lookup"><span data-stu-id="db42a-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="db42a-122">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-122">No</span></span> |
| <span data-ttu-id="db42a-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="db42a-123">rowDelimiter</span></span> |<span data-ttu-id="db42a-124">Hallo teken tooseparate rijen in een bestand gebruikt.</span><span class="sxs-lookup"><span data-stu-id="db42a-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="db42a-125">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="db42a-125">Only one character is allowed.</span></span> <span data-ttu-id="db42a-126">Hallo **standaard** waarde is een van de volgende waarden op lezen Hallo: **['\r\n', '\r', '\n']** en **'\r\n'** op schrijven.</span><span class="sxs-lookup"><span data-stu-id="db42a-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="db42a-127">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-127">No</span></span> |
| <span data-ttu-id="db42a-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="db42a-128">escapeChar</span></span> |<span data-ttu-id="db42a-129">Hallo speciaal teken tooescape een kolomscheidingsteken in inhoud van invoerbestand Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="db42a-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="db42a-130">Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven.</span><span class="sxs-lookup"><span data-stu-id="db42a-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="db42a-131">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="db42a-131">Only one character is allowed.</span></span> <span data-ttu-id="db42a-132">Er is geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="db42a-132">No default value.</span></span> <br/><br/><span data-ttu-id="db42a-133">Voorbeeld: als er een door komma's (', ') als scheidingsteken voor Hallo kolommen, maar u toohave hello kommateken in de tekst hello wilt (voorbeeld: "Hallo, wereld"), kunt u definiëren '$' als Hallo escape-teken en gebruiken van de tekenreeks "$Hallo, wereld" in de Hallo bron.</span><span class="sxs-lookup"><span data-stu-id="db42a-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="db42a-134">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-134">No</span></span> |
| <span data-ttu-id="db42a-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="db42a-135">quoteChar</span></span> |<span data-ttu-id="db42a-136">Hallo teken gebruikt tooquote een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="db42a-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="db42a-137">Hallo kolom en rij scheidingstekens binnen de aanhalingstekens Hallo zou worden beschouwd als onderdeel van Hallo string-waarde.</span><span class="sxs-lookup"><span data-stu-id="db42a-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="db42a-138">Deze eigenschap is van toepassing tooboth invoer- en uitvoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="db42a-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="db42a-139">Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven.</span><span class="sxs-lookup"><span data-stu-id="db42a-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="db42a-140">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="db42a-140">Only one character is allowed.</span></span> <span data-ttu-id="db42a-141">Er is geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="db42a-141">No default value.</span></span> <br/><br/><span data-ttu-id="db42a-142">Bijvoorbeeld, als er een door komma's (', ') als scheidingsteken voor Hallo kolommen, maar u toohave kommateken in de tekst hello wilt (voorbeeld: < Hallo, wereld >), kunt u definiëren ' (dubbel aanhalingsteken) als Hallo aanhalingsteken en gebruiken van Hallo tekenreeks "Hallo, wereld" in hello bron.</span><span class="sxs-lookup"><span data-stu-id="db42a-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="db42a-143">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-143">No</span></span> |
| <span data-ttu-id="db42a-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="db42a-144">nullValue</span></span> |<span data-ttu-id="db42a-145">Een of meer tekens gebruikt toorepresent een null-waarde.</span><span class="sxs-lookup"><span data-stu-id="db42a-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="db42a-146">Een of meer tekens.</span><span class="sxs-lookup"><span data-stu-id="db42a-146">One or more characters.</span></span> <span data-ttu-id="db42a-147">Hallo **standaard** waarden zijn **'\N' en 'NULL'** bij lezen en **'\N'** op schrijven.</span><span class="sxs-lookup"><span data-stu-id="db42a-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="db42a-148">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-148">No</span></span> |
| <span data-ttu-id="db42a-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="db42a-149">encodingName</span></span> |<span data-ttu-id="db42a-150">Hallo coderingsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="db42a-150">Specify hello encoding name.</span></span> |<span data-ttu-id="db42a-151">Een geldige coderingsnaam.</span><span class="sxs-lookup"><span data-stu-id="db42a-151">A valid encoding name.</span></span> <span data-ttu-id="db42a-152">Zie [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="db42a-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="db42a-153">Voorbeeld: windows 1250 of shift_jis.</span><span class="sxs-lookup"><span data-stu-id="db42a-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="db42a-154">Hallo **standaard** waarde is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="db42a-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="db42a-155">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-155">No</span></span> |
| <span data-ttu-id="db42a-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="db42a-156">firstRowAsHeader</span></span> |<span data-ttu-id="db42a-157">Hiermee geeft u op of tooconsider Hallo eerste rij als een koptekst.</span><span class="sxs-lookup"><span data-stu-id="db42a-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="db42a-158">Bij een gegevensset voor invoer leest Data Factory de eerste rij als een header.</span><span class="sxs-lookup"><span data-stu-id="db42a-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="db42a-159">Bij een gegevensset voor uitvoer schrijft Data Factory de eerste rij als een header.</span><span class="sxs-lookup"><span data-stu-id="db42a-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="db42a-160">Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="db42a-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="db42a-161">True</span><span class="sxs-lookup"><span data-stu-id="db42a-161">True</span></span><br/><span data-ttu-id="db42a-162">**False (standaard)**</span><span class="sxs-lookup"><span data-stu-id="db42a-162">**False (default)**</span></span> |<span data-ttu-id="db42a-163">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-163">No</span></span> |
| <span data-ttu-id="db42a-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="db42a-164">skipLineCount</span></span> |<span data-ttu-id="db42a-165">Geeft het aantal rijen tooskip Hallo bij het lezen van gegevens uit invoerbestanden.</span><span class="sxs-lookup"><span data-stu-id="db42a-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="db42a-166">Als zowel skipLineCount en firstRowAsHeader zijn opgegeven, Hallo regels eerst worden overgeslagen en wordt Hallo koptekstgegevens gelezen uit het invoerbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="db42a-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="db42a-167">Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="db42a-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="db42a-168">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="db42a-168">Integer</span></span> |<span data-ttu-id="db42a-169">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-169">No</span></span> |
| <span data-ttu-id="db42a-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="db42a-170">treatEmptyAsNull</span></span> |<span data-ttu-id="db42a-171">Hiermee geeft u op of tootreat null of lege tekenreeks als een null-waarde wanneer lezen van gegevens uit een bestand voor invoer.</span><span class="sxs-lookup"><span data-stu-id="db42a-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="db42a-172">**True (standaard)**</span><span class="sxs-lookup"><span data-stu-id="db42a-172">**True (default)**</span></span><br/><span data-ttu-id="db42a-173">False</span><span class="sxs-lookup"><span data-stu-id="db42a-173">False</span></span> |<span data-ttu-id="db42a-174">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="db42a-175">Voorbeeld van TextFormat</span><span class="sxs-lookup"><span data-stu-id="db42a-175">TextFormat example</span></span>
<span data-ttu-id="db42a-176">Hallo volgende voorbeeld ziet u enkele eigenschappen Hallo voor TextFormat.</span><span class="sxs-lookup"><span data-stu-id="db42a-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="db42a-177">toouse een `escapeChar` in plaats van `quoteChar`, vervang Hallo regel met `quoteChar` Hello escapeChar te volgen:</span><span class="sxs-lookup"><span data-stu-id="db42a-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="db42a-178">Scenario's voor het gebruik van firstRowAsHeader en skipLineCount</span><span class="sxs-lookup"><span data-stu-id="db42a-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="db42a-179">U kopieert uit een tekstbestand voor niet-bestandsbron tooa en tooadd een kopregel die Hallo schemametagegevens bevatten (bijvoorbeeld: SQL-schema).</span><span class="sxs-lookup"><span data-stu-id="db42a-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="db42a-180">Geef `firstRowAsHeader` als waar zijn in de uitvoergegevensset Hallo voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="db42a-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="db42a-181">U kopieert uit een tekstbestand met een header regel tooa niet bestand sink en wilt toodrop die regel.</span><span class="sxs-lookup"><span data-stu-id="db42a-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="db42a-182">Geef `firstRowAsHeader` echte in Hallo invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="db42a-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="db42a-183">U kopieert uit een tekstbestand en tooskip een paar regels aan begin Hallo die geen gegevens of header-gegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="db42a-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="db42a-184">Geef `skipLineCount` tooindicate Hallo aantal regels toobe overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="db42a-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="db42a-185">Als Hallo rest van Hallo-bestand een kopregel bevat, u kunt ook opgeven `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="db42a-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="db42a-186">Als beide `skipLineCount` en `firstRowAsHeader` zijn opgegeven, Hallo regels eerst worden overgeslagen en wordt Hallo koptekstgegevens gelezen uit het invoerbestand Hallo</span><span class="sxs-lookup"><span data-stu-id="db42a-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="db42a-187">JsonFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="db42a-187">Specifying JsonFormat</span></span>
<span data-ttu-id="db42a-188">te**als JSON-bestanden voor importeren/exporteren-is naar/van Azure DB die Cosmos**, Zie [voor importeren/exporteren JSON-documenten](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) sectie in hello Azure Cosmos DB connector met details.</span><span class="sxs-lookup"><span data-stu-id="db42a-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="db42a-189">Als u wilt dat tooparse Hallo JSON-bestanden of Hallo-gegevens in JSON-indeling schrijven, stel Hallo `format` `type` eigenschap te**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="db42a-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="db42a-190">U kunt ook opgeven Hallo volgende **optionele** eigenschappen in Hallo `format` sectie.</span><span class="sxs-lookup"><span data-stu-id="db42a-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="db42a-191">Zie [JsonFormat voorbeeld](#jsonformat-example) sectie over het tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="db42a-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="db42a-192">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="db42a-192">Property</span></span> | <span data-ttu-id="db42a-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="db42a-193">Description</span></span> | <span data-ttu-id="db42a-194">Vereist</span><span class="sxs-lookup"><span data-stu-id="db42a-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="db42a-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="db42a-195">filePattern</span></span> |<span data-ttu-id="db42a-196">Hallo-patroon van de gegevens die zijn opgeslagen in elk JSON-bestand aangeven.</span><span class="sxs-lookup"><span data-stu-id="db42a-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="db42a-197">Toegestane waarden zijn **setOfObjects** en **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="db42a-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="db42a-198">Hallo **standaard** waarde is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="db42a-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="db42a-199">Zie het gedeelte [JSON-bestandpatronen](#json-file-patterns) voor meer informatie over deze patronen.</span><span class="sxs-lookup"><span data-stu-id="db42a-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="db42a-200">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-200">No</span></span> |
| <span data-ttu-id="db42a-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="db42a-201">jsonNodeReference</span></span> | <span data-ttu-id="db42a-202">Als u tooiterate wilt en gegevens uit het Hallo-objecten in een matrix ophalen veld Hello hetzelfde patroon, geeft u Hallo JSON-pad van de matrix.</span><span class="sxs-lookup"><span data-stu-id="db42a-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="db42a-203">Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="db42a-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="db42a-204">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-204">No</span></span> |
| <span data-ttu-id="db42a-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="db42a-205">jsonPathDefinition</span></span> | <span data-ttu-id="db42a-206">Hallo JSON-pad-expressie voor elke kolomtoewijzing met een aangepaste kolomnaam (start met kleine) opgeven.</span><span class="sxs-lookup"><span data-stu-id="db42a-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="db42a-207">Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. U kunt gegevens ophalen uit het object of een matrix.</span><span class="sxs-lookup"><span data-stu-id="db42a-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="db42a-208">Voor velden onder hoofdobject beginnen met hoofdmap $; voor velden binnen het Hallo-matrix door gekozen `jsonNodeReference` begin vanaf matrixelement Hallo-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="db42a-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="db42a-209">Zie [JsonFormat voorbeeld](#jsonformat-example) sectie over het tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="db42a-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="db42a-210">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-210">No</span></span> |
| <span data-ttu-id="db42a-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="db42a-211">encodingName</span></span> |<span data-ttu-id="db42a-212">Hallo coderingsnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="db42a-212">Specify hello encoding name.</span></span> <span data-ttu-id="db42a-213">Zie voor Hallo lijst met geldige namen voor codering: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) eigenschap.</span><span class="sxs-lookup"><span data-stu-id="db42a-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="db42a-214">Bijvoorbeeld: windows 1250 of shift_jis.</span><span class="sxs-lookup"><span data-stu-id="db42a-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="db42a-215">Hallo **standaard** waarde is: **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="db42a-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="db42a-216">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-216">No</span></span> |
| <span data-ttu-id="db42a-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="db42a-217">nestingSeparator</span></span> |<span data-ttu-id="db42a-218">Teken gebruikte tooseparate aantal geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="db42a-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="db42a-219">Hallo-standaardwaarde is '.' (punt).</span><span class="sxs-lookup"><span data-stu-id="db42a-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="db42a-220">Nee</span><span class="sxs-lookup"><span data-stu-id="db42a-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="db42a-221">JSON-bestandpatronen</span><span class="sxs-lookup"><span data-stu-id="db42a-221">JSON file patterns</span></span>

<span data-ttu-id="db42a-222">Kopieerbewerkingen kunnen onderstaande patronen van JSON-bestanden parseren:</span><span class="sxs-lookup"><span data-stu-id="db42a-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="db42a-223">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="db42a-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="db42a-224">Elk bestand bevat één object of meerdere door regels gescheiden/samengevoegde objecten.</span><span class="sxs-lookup"><span data-stu-id="db42a-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="db42a-225">Wanneer deze optie is geselecteerd in een uitvoergegevensset, produceert de kopieerbewerking een enkel JSON-bestand met één object per regel (door regels gescheiden).</span><span class="sxs-lookup"><span data-stu-id="db42a-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="db42a-226">**voorbeeld van JSON-bestand met één object**</span><span class="sxs-lookup"><span data-stu-id="db42a-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="db42a-227">**voorbeeld van JSON-bestand dat door regels is gescheiden**</span><span class="sxs-lookup"><span data-stu-id="db42a-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="db42a-228">**voorbeeld van JSON-bestand met samengevoegde objecten**</span><span class="sxs-lookup"><span data-stu-id="db42a-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="db42a-229">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="db42a-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="db42a-230">Elk bestand bevat een matrix met objecten.</span><span class="sxs-lookup"><span data-stu-id="db42a-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="db42a-231">Voorbeeld van JsonFormat</span><span class="sxs-lookup"><span data-stu-id="db42a-231">JsonFormat example</span></span>

<span data-ttu-id="db42a-232">**Voorbeeld 1: gegevens uit JSON-bestanden kopiëren**</span><span class="sxs-lookup"><span data-stu-id="db42a-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="db42a-233">Hieronder twee soorten voorbeelden vindt u bij het kopiëren van gegevens van JSON-bestanden en algemene punten toonote Hallo:</span><span class="sxs-lookup"><span data-stu-id="db42a-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="db42a-234">**Voorbeeld 1: gegevens ophalen uit object en matrix**</span><span class="sxs-lookup"><span data-stu-id="db42a-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="db42a-235">In dit voorbeeld verwacht u dat een hoofdmap JSON-object toegewezen toosingle record in tabelvorm resultatenset.</span><span class="sxs-lookup"><span data-stu-id="db42a-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="db42a-236">Als u een JSON-bestand Hello volgende inhoud hebt:</span><span class="sxs-lookup"><span data-stu-id="db42a-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="db42a-237">en u wilt dat deze naar een Azure SQL-tabel in de volgende Hallo-indeling, door het extraheren van gegevens uit zowel objecten als matrix toocopy:</span><span class="sxs-lookup"><span data-stu-id="db42a-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="db42a-238">id</span><span class="sxs-lookup"><span data-stu-id="db42a-238">id</span></span> | <span data-ttu-id="db42a-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="db42a-239">deviceType</span></span> | <span data-ttu-id="db42a-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="db42a-240">targetResourceType</span></span> | <span data-ttu-id="db42a-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="db42a-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="db42a-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="db42a-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="db42a-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="db42a-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="db42a-244">Pc</span><span class="sxs-lookup"><span data-stu-id="db42a-244">PC</span></span> | <span data-ttu-id="db42a-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="db42a-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="db42a-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="db42a-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="db42a-247">13/1/2017 11:24:37 uur</span><span class="sxs-lookup"><span data-stu-id="db42a-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="db42a-248">Hallo invoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen).</span><span class="sxs-lookup"><span data-stu-id="db42a-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="db42a-249">Met name:</span><span class="sxs-lookup"><span data-stu-id="db42a-249">More specifically:</span></span>

- <span data-ttu-id="db42a-250">`structure`sectie definieert Hallo aangepast kolomnamen en het bijbehorende gegevenstype Hallo tijdens het converteren van tootabular gegevens.</span><span class="sxs-lookup"><span data-stu-id="db42a-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="db42a-251">Deze sectie is **optionele** tenzij u de kolomtoewijzing toodo hoeft.</span><span class="sxs-lookup"><span data-stu-id="db42a-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="db42a-252">Zie het gedeelte [Een structuurdefinitie opgeven voor rechthoekige gegevenssets](#specifying-structure-definition-for-rectangular-datasets) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db42a-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="db42a-253">`jsonPathDefinition`Hiermee geeft u Hallo JSON-pad voor elke kolom waarmee wordt aangegeven waar tooextract Hallo gegevens uit.</span><span class="sxs-lookup"><span data-stu-id="db42a-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="db42a-254">toocopy gegevens van een matrix, kunt u **matrix [x] .property** tooextract waarde Hallo gegeven eigenschap Hallo x objecten of u kunt gebruiken  **matrix [*] .property** toofind Hallo-waarde van een object met deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="db42a-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="db42a-255">**Voorbeeld 2: toepassing kruislingse meerdere objecten met dezelfde patroon van een matrix Hallo**</span><span class="sxs-lookup"><span data-stu-id="db42a-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="db42a-256">In dit voorbeeld kunt u één hoofdmap JSON-object tootransform in meerdere records in tabelvorm resultaat verwacht.</span><span class="sxs-lookup"><span data-stu-id="db42a-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="db42a-257">Als u een JSON-bestand Hello volgende inhoud hebt:</span><span class="sxs-lookup"><span data-stu-id="db42a-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="db42a-258">en u wilt dat deze naar een Azure SQL-tabel in de volgende Hallo-indeling, door het Hallo-gegevens binnen de matrix Hallo afvlakken toocopy cross join met Hallo algemene hoofdmap gegevens:</span><span class="sxs-lookup"><span data-stu-id="db42a-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="db42a-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="db42a-259">ordernumber</span></span> | <span data-ttu-id="db42a-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="db42a-260">orderdate</span></span> | <span data-ttu-id="db42a-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="db42a-261">order_pd</span></span> | <span data-ttu-id="db42a-262">order_price</span><span class="sxs-lookup"><span data-stu-id="db42a-262">order_price</span></span> | <span data-ttu-id="db42a-263">city</span><span class="sxs-lookup"><span data-stu-id="db42a-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="db42a-264">01</span><span class="sxs-lookup"><span data-stu-id="db42a-264">01</span></span> | <span data-ttu-id="db42a-265">20170122</span><span class="sxs-lookup"><span data-stu-id="db42a-265">20170122</span></span> | <span data-ttu-id="db42a-266">P1</span><span class="sxs-lookup"><span data-stu-id="db42a-266">P1</span></span> | <span data-ttu-id="db42a-267">23</span><span class="sxs-lookup"><span data-stu-id="db42a-267">23</span></span> | <span data-ttu-id="db42a-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="db42a-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="db42a-269">01</span><span class="sxs-lookup"><span data-stu-id="db42a-269">01</span></span> | <span data-ttu-id="db42a-270">20170122</span><span class="sxs-lookup"><span data-stu-id="db42a-270">20170122</span></span> | <span data-ttu-id="db42a-271">P2</span><span class="sxs-lookup"><span data-stu-id="db42a-271">P2</span></span> | <span data-ttu-id="db42a-272">13</span><span class="sxs-lookup"><span data-stu-id="db42a-272">13</span></span> | <span data-ttu-id="db42a-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="db42a-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="db42a-274">01</span><span class="sxs-lookup"><span data-stu-id="db42a-274">01</span></span> | <span data-ttu-id="db42a-275">20170122</span><span class="sxs-lookup"><span data-stu-id="db42a-275">20170122</span></span> | <span data-ttu-id="db42a-276">P3</span><span class="sxs-lookup"><span data-stu-id="db42a-276">P3</span></span> | <span data-ttu-id="db42a-277">231</span><span class="sxs-lookup"><span data-stu-id="db42a-277">231</span></span> | <span data-ttu-id="db42a-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="db42a-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="db42a-279">Hallo invoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen).</span><span class="sxs-lookup"><span data-stu-id="db42a-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="db42a-280">Met name:</span><span class="sxs-lookup"><span data-stu-id="db42a-280">More specifically:</span></span>

- <span data-ttu-id="db42a-281">`structure`sectie definieert Hallo aangepast kolomnamen en het bijbehorende gegevenstype Hallo tijdens het converteren van tootabular gegevens.</span><span class="sxs-lookup"><span data-stu-id="db42a-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="db42a-282">Deze sectie is **optionele** tenzij u de kolomtoewijzing toodo hoeft.</span><span class="sxs-lookup"><span data-stu-id="db42a-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="db42a-283">Zie het gedeelte [Een structuurdefinitie opgeven voor rechthoekige gegevenssets](#specifying-structure-definition-for-rectangular-datasets) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="db42a-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="db42a-284">`jsonNodeReference`Hiermee wordt aangegeven tooiterate en gegevens te extraheren uit het Hallo-objecten met dezelfde patroon onder Hallo **matrix** orderlines.</span><span class="sxs-lookup"><span data-stu-id="db42a-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="db42a-285">`jsonPathDefinition`Hiermee geeft u Hallo JSON-pad voor elke kolom waarmee wordt aangegeven waar tooextract Hallo gegevens uit.</span><span class="sxs-lookup"><span data-stu-id="db42a-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="db42a-286">In dit voorbeeld zijn 'ordernumber', 'orderdate' en 'plaats' onder hoofdobject met JSON-pad beginnen met "$.", terwijl 'order_pd' en 'order_price' worden gedefinieerd met het pad dat is afgeleid van een matrixelement Hallo zonder "$"..</span><span class="sxs-lookup"><span data-stu-id="db42a-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="db42a-287">**Houd er rekening mee Hallo volgende punten:**</span><span class="sxs-lookup"><span data-stu-id="db42a-287">**Note hello following points:**</span></span>

* <span data-ttu-id="db42a-288">Als hello `structure` en `jsonPathDefinition` zijn niet gedefinieerd in de Data Factory-gegevensset hello, hello Kopieeractiviteit detecteert schema van de eerste object Hallo Hallo en plat Hallo gehele object.</span><span class="sxs-lookup"><span data-stu-id="db42a-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="db42a-289">Als Hallo JSON-invoer een matrix heeft, standaard zet Hallo Kopieeractiviteit Hallo volledige Matrixwaarde in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="db42a-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="db42a-290">U kunt tooextract gegevens met behulp van `jsonNodeReference` en/of `jsonPathDefinition`, of door op te geven niet in overslaan `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="db42a-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="db42a-291">Als er dubbele namen op hetzelfde niveau hello, Hallo Kopieeractiviteit uitgelicht Hallo laatste.</span><span class="sxs-lookup"><span data-stu-id="db42a-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="db42a-292">Eigenschapnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="db42a-292">Property names are case-sensitive.</span></span> <span data-ttu-id="db42a-293">Twee eigenschappen met dezelfde naam maar met een verschil in hoofdletters en kleine letters worden behandeld als twee afzonderlijke eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="db42a-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="db42a-294">**Voorbeeld 2: Schrijven tooJSON gegevensbestand**</span><span class="sxs-lookup"><span data-stu-id="db42a-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="db42a-295">Als u de onderstaande tabel hebt in SQL-Database:</span><span class="sxs-lookup"><span data-stu-id="db42a-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="db42a-296">id</span><span class="sxs-lookup"><span data-stu-id="db42a-296">id</span></span> | <span data-ttu-id="db42a-297">order_date</span><span class="sxs-lookup"><span data-stu-id="db42a-297">order_date</span></span> | <span data-ttu-id="db42a-298">order_price</span><span class="sxs-lookup"><span data-stu-id="db42a-298">order_price</span></span> | <span data-ttu-id="db42a-299">order_by</span><span class="sxs-lookup"><span data-stu-id="db42a-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="db42a-300">1</span><span class="sxs-lookup"><span data-stu-id="db42a-300">1</span></span> | <span data-ttu-id="db42a-301">20170119</span><span class="sxs-lookup"><span data-stu-id="db42a-301">20170119</span></span> | <span data-ttu-id="db42a-302">2000</span><span class="sxs-lookup"><span data-stu-id="db42a-302">2000</span></span> | <span data-ttu-id="db42a-303">David</span><span class="sxs-lookup"><span data-stu-id="db42a-303">David</span></span> |
| <span data-ttu-id="db42a-304">2</span><span class="sxs-lookup"><span data-stu-id="db42a-304">2</span></span> | <span data-ttu-id="db42a-305">20170120</span><span class="sxs-lookup"><span data-stu-id="db42a-305">20170120</span></span> | <span data-ttu-id="db42a-306">3500</span><span class="sxs-lookup"><span data-stu-id="db42a-306">3500</span></span> | <span data-ttu-id="db42a-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="db42a-307">Patrick</span></span> |
| <span data-ttu-id="db42a-308">3</span><span class="sxs-lookup"><span data-stu-id="db42a-308">3</span></span> | <span data-ttu-id="db42a-309">20170121</span><span class="sxs-lookup"><span data-stu-id="db42a-309">20170121</span></span> | <span data-ttu-id="db42a-310">4000</span><span class="sxs-lookup"><span data-stu-id="db42a-310">4000</span></span> | <span data-ttu-id="db42a-311">Jason</span><span class="sxs-lookup"><span data-stu-id="db42a-311">Jason</span></span> |

<span data-ttu-id="db42a-312">en voor elke record verwacht toowrite tooa JSON-object in de onderstaande indeling:</span><span class="sxs-lookup"><span data-stu-id="db42a-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="db42a-313">Hallo uitvoergegevensset met **JsonFormat** type is als volgt gedefinieerd: (gedeeltelijke definitie met alleen relevante Hallo delen).</span><span class="sxs-lookup"><span data-stu-id="db42a-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="db42a-314">Meer specifiek, `structure` sectie Hallo aangepast eigenschapnamen worden gedefinieerd in doelbestand, `nestingSeparator` (standaardwaarde is '. ') worden gebruikte tooidentify Hallo nest laag uit Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="db42a-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="db42a-315">Deze sectie is **optionele** tenzij u wilt vergelijken met de naam van bronkolom Hallo-eigenschapsnaam voor toochange of sommige Hallo-eigenschappen worden genest.</span><span class="sxs-lookup"><span data-stu-id="db42a-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="db42a-316">AvroFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="db42a-316">Specifying AvroFormat</span></span>
<span data-ttu-id="db42a-317">Als u wilt dat tooparse hello Avro bestanden of Hallo-gegevens in de Avro-indeling schrijven, ingesteld Hallo `format` `type` eigenschap te**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="db42a-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="db42a-318">U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify.</span><span class="sxs-lookup"><span data-stu-id="db42a-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="db42a-319">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db42a-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="db42a-320">toouse Avro-indeling in een Hive-tabel, kunt u verwijzen te[van Apache Hive zelfstudie](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="db42a-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="db42a-321">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="db42a-321">Note hello following points:</span></span>  

* <span data-ttu-id="db42a-322">[Complexe gegevenstypen](http://avro.apache.org/docs/current/spec.html#schema_complex) worden niet ondersteund (records, enums, matrices, kaarten, samenvoegingen en vaste bestanden).</span><span class="sxs-lookup"><span data-stu-id="db42a-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="db42a-323">OrcFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="db42a-323">Specifying OrcFormat</span></span>
<span data-ttu-id="db42a-324">Als u wilt dat tooparse hello ORC-bestanden of Hallo-gegevens in ORC-indeling schrijven, ingesteld Hallo `format` `type` eigenschap te**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="db42a-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="db42a-325">U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify.</span><span class="sxs-lookup"><span data-stu-id="db42a-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="db42a-326">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db42a-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="db42a-327">Als u geen ORC-bestanden kopieert **als-is** tussen on-premises en cloud gegevensarchieven, moet u tooinstall Hallo JRE 8 (Java Runtime Environment) op uw computer met de gateway.</span><span class="sxs-lookup"><span data-stu-id="db42a-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="db42a-328">Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway.</span><span class="sxs-lookup"><span data-stu-id="db42a-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="db42a-329">U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="db42a-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="db42a-330">Hallo juiste wachtwoord kiezen.</span><span class="sxs-lookup"><span data-stu-id="db42a-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="db42a-331">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="db42a-331">Note hello following points:</span></span>

* <span data-ttu-id="db42a-332">Complexe gegevenstypen worden niet ondersteund (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="db42a-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="db42a-333">Een ORC-bestand heeft drie [opties voor compressie](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="db42a-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="db42a-334">Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="db42a-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="db42a-335">Hierbij Hallo compressie codec bevindt zich in Hallo metagegevens tooread Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="db42a-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="db42a-336">Echter, bij het schrijven van tooan ORC bestand Data Factory kiest ZLIB, dit is de standaardoptie Hallo voor ORC.</span><span class="sxs-lookup"><span data-stu-id="db42a-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="db42a-337">Er is momenteel geen optie toooverride dit gedrag.</span><span class="sxs-lookup"><span data-stu-id="db42a-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="db42a-338">ParquetFormat opgeven</span><span class="sxs-lookup"><span data-stu-id="db42a-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="db42a-339">Als u tooparse Hallo parketvloeren bestanden wilt of Hallo-gegevens in de indeling parketvloeren schrijven, ingesteld Hallo `format` `type` eigenschap te**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="db42a-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="db42a-340">U hoeft geen eigenschappen in Hallo indeling sectie binnen Hallo typeProperties sectie niet toospecify.</span><span class="sxs-lookup"><span data-stu-id="db42a-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="db42a-341">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db42a-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="db42a-342">Als u geen parketvloeren bestanden kopieert **als-is** tussen on-premises en cloud gegevensarchieven, moet u tooinstall Hallo JRE 8 (Java Runtime Environment) op uw computer met de gateway.</span><span class="sxs-lookup"><span data-stu-id="db42a-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="db42a-343">Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway.</span><span class="sxs-lookup"><span data-stu-id="db42a-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="db42a-344">U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="db42a-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="db42a-345">Hallo juiste wachtwoord kiezen.</span><span class="sxs-lookup"><span data-stu-id="db42a-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="db42a-346">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="db42a-346">Note hello following points:</span></span>

* <span data-ttu-id="db42a-347">Complexe gegevenstypen worden niet ondersteund (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="db42a-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="db42a-348">Parketvloeren bestand heeft Hallo volgend opties voor compressie: NONE, SNAPPY GZIP en LZO.</span><span class="sxs-lookup"><span data-stu-id="db42a-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="db42a-349">Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="db42a-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="db42a-350">Hallo compressiecodec wordt gebruikt in Hallo metagegevens tooread Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="db42a-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="db42a-351">Echter bij het schrijven van tooa parketvloeren bestand kiest Data Factory SNAPPY, dit is de standaardoptie Hallo voor parketvloeren-indeling.</span><span class="sxs-lookup"><span data-stu-id="db42a-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="db42a-352">Er is momenteel geen optie toooverride dit gedrag.</span><span class="sxs-lookup"><span data-stu-id="db42a-352">Currently, there is no option toooverride this behavior.</span></span>
