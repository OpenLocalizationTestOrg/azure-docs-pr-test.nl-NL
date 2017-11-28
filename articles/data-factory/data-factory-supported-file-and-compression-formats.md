---
title: Bestands- en compressie-notaties in Azure Data Factory | Microsoft Docs
description: Meer informatie over de ondersteunde bestandsindelingen in Azure Data Factory.
keywords: "BLOB-gegevens, azure-blob kopiëren"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="49a93-104">Bestands- en compressie indelingen die worden ondersteund door Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="49a93-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="49a93-105">*In dit onderwerp is van toepassing op de volgende connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [bestandssysteem](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), en [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="49a93-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="49a93-106">Azure Data Factory ondersteunt de volgende bestandstypen: indeling:</span><span class="sxs-lookup"><span data-stu-id="49a93-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="49a93-107">Tekstopmaak</span><span class="sxs-lookup"><span data-stu-id="49a93-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="49a93-108">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="49a93-109">Avro-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="49a93-110">ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="49a93-111">Parketvloeren-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="49a93-112">Tekstopmaak</span><span class="sxs-lookup"><span data-stu-id="49a93-112">Text format</span></span>
<span data-ttu-id="49a93-113">Als u wilt lezen uit een tekstbestand of schrijven naar een tekstbestand, stelt u de `type` eigenschap in de `format` sectie van de gegevensset **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="49a93-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="49a93-114">U kunt ook de volgende **optionele** eigenschappen opgeven in het gedeelte `format`.</span><span class="sxs-lookup"><span data-stu-id="49a93-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="49a93-115">Raadpleeg het gedeelte [TextFormat-voorbeeld](#textformat-example) voor configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="49a93-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="49a93-116">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="49a93-116">Property</span></span> | <span data-ttu-id="49a93-117">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="49a93-117">Description</span></span> | <span data-ttu-id="49a93-118">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="49a93-118">Allowed values</span></span> | <span data-ttu-id="49a93-119">Vereist</span><span class="sxs-lookup"><span data-stu-id="49a93-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="49a93-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="49a93-120">columnDelimiter</span></span> |<span data-ttu-id="49a93-121">Het teken dat wordt gebruikt voor het scheiden van kolommen in een bestand.</span><span class="sxs-lookup"><span data-stu-id="49a93-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="49a93-122">U kunt overwegen een zeldzame niet-afdrukbare tekens die mogelijk waarschijnlijk bestaan niet in uw gegevens te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49a93-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="49a93-123">Geef bijvoorbeeld '\u0001', waarmee de Start van kop (SOH).</span><span class="sxs-lookup"><span data-stu-id="49a93-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="49a93-124">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="49a93-124">Only one character is allowed.</span></span> <span data-ttu-id="49a93-125">De **standaardwaarde** is een **komma (',')**.</span><span class="sxs-lookup"><span data-stu-id="49a93-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="49a93-126">Raadpleeg voor het gebruik van een Unicode-teken [Unicode-tekens](https://en.wikipedia.org/wiki/List_of_Unicode_characters) de overeenkomstige code ophalen voor deze.</span><span class="sxs-lookup"><span data-stu-id="49a93-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="49a93-127">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-127">No</span></span> |
| <span data-ttu-id="49a93-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="49a93-128">rowDelimiter</span></span> |<span data-ttu-id="49a93-129">Het teken dat wordt gebruikt voor het scheiden van rijen in een bestand.</span><span class="sxs-lookup"><span data-stu-id="49a93-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="49a93-130">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="49a93-130">Only one character is allowed.</span></span> <span data-ttu-id="49a93-131">De **standaardwaarde** is een van de volgende leeswaarden **['\r\n', '\r', '\n']** en de schrijfwaarde **'\r\n'**.</span><span class="sxs-lookup"><span data-stu-id="49a93-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="49a93-132">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-132">No</span></span> |
| <span data-ttu-id="49a93-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="49a93-133">escapeChar</span></span> |<span data-ttu-id="49a93-134">Dit speciale teken wordt gebruikt om een scheidingsteken voor kolommen van de inhoud van het invoerbestand om te zetten.</span><span class="sxs-lookup"><span data-stu-id="49a93-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="49a93-135">Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven.</span><span class="sxs-lookup"><span data-stu-id="49a93-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="49a93-136">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="49a93-136">Only one character is allowed.</span></span> <span data-ttu-id="49a93-137">Er is geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="49a93-137">No default value.</span></span> <br/><br/><span data-ttu-id="49a93-138">Voorbeeld: als u kolommen scheidt met komma's (', '), maar u het kommateken in een tekst wilt gebruiken (voorbeeld: 'Hallo, wereld'), kunt u '$' als het omzettingsteken opgeven en in de bron de tekenreeks 'Hallo$, wereld' gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49a93-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="49a93-139">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-139">No</span></span> |
| <span data-ttu-id="49a93-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="49a93-140">quoteChar</span></span> |<span data-ttu-id="49a93-141">Het teken dat wordt gebruikt om een tekenreekswaarde te citeren.</span><span class="sxs-lookup"><span data-stu-id="49a93-141">The character used to quote a string value.</span></span> <span data-ttu-id="49a93-142">De scheidingstekens voor kolommen en rijen binnen de aanhalingstekens worden beschouwd als onderdeel van de tekenreekswaarde.</span><span class="sxs-lookup"><span data-stu-id="49a93-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="49a93-143">Deze eigenschap is van toepassing op gegevenssets voor invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="49a93-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="49a93-144">Het is niet mogelijk om zowel escapeChar als quoteChar voor een tabel op te geven.</span><span class="sxs-lookup"><span data-stu-id="49a93-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="49a93-145">Er is slechts één teken toegestaan.</span><span class="sxs-lookup"><span data-stu-id="49a93-145">Only one character is allowed.</span></span> <span data-ttu-id="49a93-146">Er is geen standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="49a93-146">No default value.</span></span> <br/><br/><span data-ttu-id="49a93-147">Voorbeeld: als u kolommen scheidt met komma's (', '), maar u het kommateken in een tekst wilt gebruiken (voorbeeld: <Hallo, wereld>), kunt u " (dubbel aanhalingsteken) als het aanhalingsteken opgeven en de tekenreeks "Hallo, wereld" in de bron gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49a93-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="49a93-148">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-148">No</span></span> |
| <span data-ttu-id="49a93-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="49a93-149">nullValue</span></span> |<span data-ttu-id="49a93-150">Een of meer tekens die worden gebruikt om een null-waarde te vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="49a93-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="49a93-151">Een of meer tekens.</span><span class="sxs-lookup"><span data-stu-id="49a93-151">One or more characters.</span></span> <span data-ttu-id="49a93-152">De **standaardwaarden** zijn **'\N' en 'NULL'** voor lezen en **'\N'** voor schrijven.</span><span class="sxs-lookup"><span data-stu-id="49a93-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="49a93-153">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-153">No</span></span> |
| <span data-ttu-id="49a93-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="49a93-154">encodingName</span></span> |<span data-ttu-id="49a93-155">Geef de coderingsnaam op.</span><span class="sxs-lookup"><span data-stu-id="49a93-155">Specify the encoding name.</span></span> |<span data-ttu-id="49a93-156">Een geldige coderingsnaam.</span><span class="sxs-lookup"><span data-stu-id="49a93-156">A valid encoding name.</span></span> <span data-ttu-id="49a93-157">Zie [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="49a93-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="49a93-158">Voorbeeld: windows 1250 of shift_jis.</span><span class="sxs-lookup"><span data-stu-id="49a93-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="49a93-159">De **standaardwaarde** is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="49a93-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="49a93-160">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-160">No</span></span> |
| <span data-ttu-id="49a93-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="49a93-161">firstRowAsHeader</span></span> |<span data-ttu-id="49a93-162">Hiermee geeft u op of de eerste rij als een header moet worden gezien.</span><span class="sxs-lookup"><span data-stu-id="49a93-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="49a93-163">Bij een gegevensset voor invoer leest Data Factory de eerste rij als een header.</span><span class="sxs-lookup"><span data-stu-id="49a93-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="49a93-164">Bij een gegevensset voor uitvoer schrijft Data Factory de eerste rij als een header.</span><span class="sxs-lookup"><span data-stu-id="49a93-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="49a93-165">Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="49a93-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="49a93-166">True</span><span class="sxs-lookup"><span data-stu-id="49a93-166">True</span></span><br/><span data-ttu-id="49a93-167"><b>False (standaard)</b></span><span class="sxs-lookup"><span data-stu-id="49a93-167"><b>False (default)</b></span></span> |<span data-ttu-id="49a93-168">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-168">No</span></span> |
| <span data-ttu-id="49a93-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="49a93-169">skipLineCount</span></span> |<span data-ttu-id="49a93-170">Geeft het aantal rijen aan dat moet worden overgeslagen bij het lezen van gegevens in invoerbestanden.</span><span class="sxs-lookup"><span data-stu-id="49a93-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="49a93-171">Als zowel skipLineCount als firstRowAsHeader is opgegeven, worden de regels eerst overgeslagen en wordt de headerinformatie gelezen uit het invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="49a93-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="49a93-172">Zie [Gebruiksscenario's`firstRowAsHeader` en `skipLineCount` ](#scenarios-for-using-firstrowasheader-and-skiplinecount) voor voorbeeldscenario's.</span><span class="sxs-lookup"><span data-stu-id="49a93-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="49a93-173">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="49a93-173">Integer</span></span> |<span data-ttu-id="49a93-174">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-174">No</span></span> |
| <span data-ttu-id="49a93-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="49a93-175">treatEmptyAsNull</span></span> |<span data-ttu-id="49a93-176">Hiermee geeft u aan of null of lege tekenreeks moeten worden behandeld als een null-waarde bij het lezen van gegevens uit een invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="49a93-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="49a93-177">**True (standaard)**</span><span class="sxs-lookup"><span data-stu-id="49a93-177">**True (default)**</span></span><br/><span data-ttu-id="49a93-178">False</span><span class="sxs-lookup"><span data-stu-id="49a93-178">False</span></span> |<span data-ttu-id="49a93-179">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="49a93-180">Voorbeeld van TextFormat</span><span class="sxs-lookup"><span data-stu-id="49a93-180">TextFormat example</span></span>
<span data-ttu-id="49a93-181">In de volgende JSON-definitie voor een gegevensset, worden enkele van de optionele eigenschappen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="49a93-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

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

<span data-ttu-id="49a93-182">Gebruik een `escapeChar` in plaats van `quoteChar`, vervang de regel door `quoteChar` met het volgende escapeChar:</span><span class="sxs-lookup"><span data-stu-id="49a93-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="49a93-183">Scenario's voor het gebruik van firstRowAsHeader en skipLineCount</span><span class="sxs-lookup"><span data-stu-id="49a93-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="49a93-184">U kopieert vanuit een bron die geen bestand is, naar een tekstbestand en wilt een headerregel toevoegen die de metagegevens van het schema bevat (bijvoorbeeld: SQL-schema).</span><span class="sxs-lookup"><span data-stu-id="49a93-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="49a93-185">Geef voor `firstRowAsHeader` 'True' op in de uitvoergegevensset voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="49a93-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="49a93-186">U wilt kopiëren vanuit een tekstbestand met een headerregel naar een sink die geen bestand is en wilt die regel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="49a93-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="49a93-187">Geef voor `firstRowAsHeader` 'True' op in de invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="49a93-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="49a93-188">U wilt kopiëren uit een tekstbestand en wilt een paar regels aan het begin overslaan die geen gegevens of headerinformatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="49a93-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="49a93-189">Geef `skipLineCount` op om aan te geven hoeveel regels er moeten worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="49a93-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="49a93-190">Als de rest van het bestand een headerregel bevat, kunt u ook `firstRowAsHeader` opgeven.</span><span class="sxs-lookup"><span data-stu-id="49a93-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="49a93-191">Als zowel `skipLineCount` als `firstRowAsHeader` is opgegeven, worden de regels eerst overgeslagen en wordt de headerinformatie gelezen uit het invoerbestand</span><span class="sxs-lookup"><span data-stu-id="49a93-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="49a93-192">JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-192">JSON format</span></span>
<span data-ttu-id="49a93-193">Naar **importeren/exporteren als een JSON-bestand-is naar/van Azure DB die Cosmos**, het Zie [voor importeren/exporteren JSON-documenten](data-factory-azure-documentdb-connector.md#importexport-json-documents) in sectie [gegevens verplaatsen naar/van Azure DB die Cosmos](data-factory-azure-documentdb-connector.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="49a93-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="49a93-194">Als u wilt voor het parseren van de JSON-bestanden of de gegevens te schrijven in JSON-indeling, stelt de `type` eigenschap in de `format` sectie naar **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="49a93-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="49a93-195">U kunt ook de volgende **optionele** eigenschappen opgeven in het gedeelte `format`.</span><span class="sxs-lookup"><span data-stu-id="49a93-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="49a93-196">Zie het gedeelte [JsonFormat-voorbeeld](#jsonformat-example) voor configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="49a93-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="49a93-197">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="49a93-197">Property</span></span> | <span data-ttu-id="49a93-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="49a93-198">Description</span></span> | <span data-ttu-id="49a93-199">Vereist</span><span class="sxs-lookup"><span data-stu-id="49a93-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49a93-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="49a93-200">filePattern</span></span> |<span data-ttu-id="49a93-201">Hiermee geeft u het patroon aan van gegevens die zijn opgeslagen in elk JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="49a93-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="49a93-202">Toegestane waarden zijn **setOfObjects** en **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="49a93-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="49a93-203">De **standaardwaarde** is **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="49a93-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="49a93-204">Zie het gedeelte [JSON-bestandpatronen](#json-file-patterns) voor meer informatie over deze patronen.</span><span class="sxs-lookup"><span data-stu-id="49a93-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="49a93-205">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-205">No</span></span> |
| <span data-ttu-id="49a93-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="49a93-206">jsonNodeReference</span></span> | <span data-ttu-id="49a93-207">Als u wilt bladeren en gegevens wilt ophalen uit de objecten in een matrixveld met hetzelfde patroon, geeft u het JSON-pad van die matrix op.</span><span class="sxs-lookup"><span data-stu-id="49a93-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="49a93-208">Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="49a93-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="49a93-209">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-209">No</span></span> |
| <span data-ttu-id="49a93-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="49a93-210">jsonPathDefinition</span></span> | <span data-ttu-id="49a93-211">Hiermee geeft u de JSON-padexpressie aan voor elke kolomtoewijzing met een aangepaste kolomnaam (begin met een kleine letter).</span><span class="sxs-lookup"><span data-stu-id="49a93-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="49a93-212">Deze eigenschap wordt alleen ondersteund bij het kopiëren van gegevens uit JSON-bestanden. U kunt gegevens ophalen uit het object of een matrix.</span><span class="sxs-lookup"><span data-stu-id="49a93-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="49a93-213">Voor velden onder het hoofdobject begint u met root $; voor velden binnen de matrix die is gekozen door de eigenschap `jsonNodeReference`, begint u vanaf het element van de matrix.</span><span class="sxs-lookup"><span data-stu-id="49a93-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="49a93-214">Zie het gedeelte [JsonFormat-voorbeeld](#jsonformat-example) voor configuratie-instructies.</span><span class="sxs-lookup"><span data-stu-id="49a93-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="49a93-215">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-215">No</span></span> |
| <span data-ttu-id="49a93-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="49a93-216">encodingName</span></span> |<span data-ttu-id="49a93-217">Geef de coderingsnaam op.</span><span class="sxs-lookup"><span data-stu-id="49a93-217">Specify the encoding name.</span></span> <span data-ttu-id="49a93-218">Zie voor de lijst met geldige namen voor versleuteling [De eigenschap Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="49a93-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="49a93-219">Bijvoorbeeld: windows 1250 of shift_jis.</span><span class="sxs-lookup"><span data-stu-id="49a93-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="49a93-220">De **standaardwaarde** is **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="49a93-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="49a93-221">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-221">No</span></span> |
| <span data-ttu-id="49a93-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="49a93-222">nestingSeparator</span></span> |<span data-ttu-id="49a93-223">Teken dat wordt gebruikt voor het scheiden van geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="49a93-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="49a93-224">De standaardwaarde is '.' (punt).</span><span class="sxs-lookup"><span data-stu-id="49a93-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="49a93-225">Nee</span><span class="sxs-lookup"><span data-stu-id="49a93-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="49a93-226">JSON-bestandpatronen</span><span class="sxs-lookup"><span data-stu-id="49a93-226">JSON file patterns</span></span>

<span data-ttu-id="49a93-227">De volgende patronen van JSON-bestanden kan worden geparseerd door kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="49a93-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="49a93-228">**Type I: setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="49a93-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="49a93-229">Elk bestand bevat één object of meerdere door regels gescheiden/samengevoegde objecten.</span><span class="sxs-lookup"><span data-stu-id="49a93-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="49a93-230">Wanneer deze optie is geselecteerd in een uitvoergegevensset, produceert de kopieerbewerking een enkel JSON-bestand met één object per regel (door regels gescheiden).</span><span class="sxs-lookup"><span data-stu-id="49a93-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="49a93-231">**voorbeeld van JSON-bestand met één object**</span><span class="sxs-lookup"><span data-stu-id="49a93-231">**single object JSON example**</span></span>

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

    * <span data-ttu-id="49a93-232">**voorbeeld van JSON-bestand dat door regels is gescheiden**</span><span class="sxs-lookup"><span data-stu-id="49a93-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="49a93-233">**voorbeeld van JSON-bestand met samengevoegde objecten**</span><span class="sxs-lookup"><span data-stu-id="49a93-233">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="49a93-234">**Type II: arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="49a93-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="49a93-235">Elk bestand bevat een matrix met objecten.</span><span class="sxs-lookup"><span data-stu-id="49a93-235">Each file contains an array of objects.</span></span>

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

### <a name="jsonformat-example"></a><span data-ttu-id="49a93-236">Voorbeeld van JsonFormat</span><span class="sxs-lookup"><span data-stu-id="49a93-236">JsonFormat example</span></span>

<span data-ttu-id="49a93-237">**Voorbeeld 1: gegevens uit JSON-bestanden kopiëren**</span><span class="sxs-lookup"><span data-stu-id="49a93-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="49a93-238">Zie de volgende twee steekproeven bij het kopiëren van gegevens van JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="49a93-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="49a93-239">De algemene verwijst naar Let op:</span><span class="sxs-lookup"><span data-stu-id="49a93-239">The generic points to note:</span></span>

<span data-ttu-id="49a93-240">**Voorbeeld 1: gegevens ophalen uit object en matrix**</span><span class="sxs-lookup"><span data-stu-id="49a93-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="49a93-241">In dit voorbeeld kunt u verwachten dat één JSON-hoofdobject wordt toegewezen aan één record in het tabelresultaat.</span><span class="sxs-lookup"><span data-stu-id="49a93-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="49a93-242">Als u een JSON-bestand hebt met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="49a93-242">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="49a93-243">en u wilt het kopiëren naar een Azure SQL-tabel in de volgende indeling door gegevens te extraheren uit de objecten en matrix:</span><span class="sxs-lookup"><span data-stu-id="49a93-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="49a93-244">id</span><span class="sxs-lookup"><span data-stu-id="49a93-244">id</span></span> | <span data-ttu-id="49a93-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="49a93-245">deviceType</span></span> | <span data-ttu-id="49a93-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="49a93-246">targetResourceType</span></span> | <span data-ttu-id="49a93-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="49a93-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="49a93-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="49a93-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="49a93-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="49a93-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="49a93-250">Pc</span><span class="sxs-lookup"><span data-stu-id="49a93-250">PC</span></span> | <span data-ttu-id="49a93-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="49a93-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="49a93-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="49a93-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="49a93-253">13/1/2017 11:24:37 uur</span><span class="sxs-lookup"><span data-stu-id="49a93-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="49a93-254">De invoergegevensset met het type **JsonFormat** wordt als volgt gedefinieerd: (gedeeltelijke definitie met alleen belangrijke onderdelen).</span><span class="sxs-lookup"><span data-stu-id="49a93-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="49a93-255">Met name:</span><span class="sxs-lookup"><span data-stu-id="49a93-255">More specifically:</span></span>

- <span data-ttu-id="49a93-256">Het gedeelte `structure` definieert de aangepaste kolomnamen en het bijbehorende gegevenstype tijdens het converteren van gegevens in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="49a93-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="49a93-257">Dit gedeelte is **optioneel**, tenzij u kolommen moet toewijzen.</span><span class="sxs-lookup"><span data-stu-id="49a93-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="49a93-258">Zie [bronkolommen gegevensset toewijzen aan bestemming gegevensset kolommen](data-factory-map-columns.md) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="49a93-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="49a93-259">Met `jsonPathDefinition` geeft u het JSON-pad op voor elke kolom die aangeeft waar de gegevens moeten worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="49a93-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="49a93-260">Voor het kopiëren van gegevens vanuit een matrix kunt u **array[x].property** gebruiken om de waarde van de opgegeven eigenschap op te halen uit het xth-object. U kunt ook **array[*].property** gebruiken om de waarde van een object met deze eigenschap te vinden.</span><span class="sxs-lookup"><span data-stu-id="49a93-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="49a93-261">**Voorbeeld 2: meerdere objecten met hetzelfde patroon uit een matrix toepassen**</span><span class="sxs-lookup"><span data-stu-id="49a93-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="49a93-262">In dit voorbeeld probeert u een JSON-hoofdobject te transformeren naar meerdere records in een tabelresultaat.</span><span class="sxs-lookup"><span data-stu-id="49a93-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="49a93-263">Als u een JSON-bestand hebt met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="49a93-263">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="49a93-264">en u wilt het kopiëren naar een Azure SQL-tabel in de volgende indeling, door de gegevens binnen de matrix af te vlakken en samen te voegen met de algemene root-gegevens:</span><span class="sxs-lookup"><span data-stu-id="49a93-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="49a93-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="49a93-265">ordernumber</span></span> | <span data-ttu-id="49a93-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="49a93-266">orderdate</span></span> | <span data-ttu-id="49a93-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="49a93-267">order_pd</span></span> | <span data-ttu-id="49a93-268">order_price</span><span class="sxs-lookup"><span data-stu-id="49a93-268">order_price</span></span> | <span data-ttu-id="49a93-269">city</span><span class="sxs-lookup"><span data-stu-id="49a93-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="49a93-270">01</span><span class="sxs-lookup"><span data-stu-id="49a93-270">01</span></span> | <span data-ttu-id="49a93-271">20170122</span><span class="sxs-lookup"><span data-stu-id="49a93-271">20170122</span></span> | <span data-ttu-id="49a93-272">P1</span><span class="sxs-lookup"><span data-stu-id="49a93-272">P1</span></span> | <span data-ttu-id="49a93-273">23</span><span class="sxs-lookup"><span data-stu-id="49a93-273">23</span></span> | <span data-ttu-id="49a93-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="49a93-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="49a93-275">01</span><span class="sxs-lookup"><span data-stu-id="49a93-275">01</span></span> | <span data-ttu-id="49a93-276">20170122</span><span class="sxs-lookup"><span data-stu-id="49a93-276">20170122</span></span> | <span data-ttu-id="49a93-277">P2</span><span class="sxs-lookup"><span data-stu-id="49a93-277">P2</span></span> | <span data-ttu-id="49a93-278">13</span><span class="sxs-lookup"><span data-stu-id="49a93-278">13</span></span> | <span data-ttu-id="49a93-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="49a93-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="49a93-280">01</span><span class="sxs-lookup"><span data-stu-id="49a93-280">01</span></span> | <span data-ttu-id="49a93-281">20170122</span><span class="sxs-lookup"><span data-stu-id="49a93-281">20170122</span></span> | <span data-ttu-id="49a93-282">P3</span><span class="sxs-lookup"><span data-stu-id="49a93-282">P3</span></span> | <span data-ttu-id="49a93-283">231</span><span class="sxs-lookup"><span data-stu-id="49a93-283">231</span></span> | <span data-ttu-id="49a93-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="49a93-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="49a93-285">De invoergegevensset met het type **JsonFormat** wordt als volgt gedefinieerd: (gedeeltelijke definitie met alleen belangrijke onderdelen).</span><span class="sxs-lookup"><span data-stu-id="49a93-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="49a93-286">Met name:</span><span class="sxs-lookup"><span data-stu-id="49a93-286">More specifically:</span></span>

- <span data-ttu-id="49a93-287">Het gedeelte `structure` definieert de aangepaste kolomnamen en het bijbehorende gegevenstype tijdens het converteren van gegevens in tabelvorm.</span><span class="sxs-lookup"><span data-stu-id="49a93-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="49a93-288">Dit gedeelte is **optioneel**, tenzij u kolommen moet toewijzen.</span><span class="sxs-lookup"><span data-stu-id="49a93-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="49a93-289">Zie [bronkolommen gegevensset toewijzen aan bestemming gegevensset kolommen](data-factory-map-columns.md) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="49a93-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="49a93-290">Met `jsonNodeReference` geeft u aan dat moet worden gebladerd naar het object en dat er gegevens uit moeten worden opgehaald met hetzelfde patroon onder de **matrix** orderlines.</span><span class="sxs-lookup"><span data-stu-id="49a93-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="49a93-291">Met `jsonPathDefinition` geeft u het JSON-pad op voor elke kolom die aangeeft waar de gegevens moeten worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="49a93-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="49a93-292">In dit voorbeeld bevinden 'ordernumber', 'orderdate' en 'city' zich onder het root-object. Het JSON-pad begint met '$.', terwijl 'order_pd' en 'order_price' worden gedefinieerd met het pad dat is afgeleid van het matrixelement zonder '$.'.</span><span class="sxs-lookup"><span data-stu-id="49a93-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="49a93-293">**Houd rekening met de volgende punten:**</span><span class="sxs-lookup"><span data-stu-id="49a93-293">**Note the following points:**</span></span>

* <span data-ttu-id="49a93-294">Als `structure` en `jsonPathDefinition` niet zijn gedefinieerd in de gegevensset van Data Factory, detecteert de kopieerbewerking het schema van het eerste object en wordt het hele object afgevlakt.</span><span class="sxs-lookup"><span data-stu-id="49a93-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="49a93-295">Als de JSON-invoer een matrix heeft, zet de kopieerbewerking de volledige matrix-waarde standaard om in een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="49a93-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="49a93-296">U kunt ervoor kiezen om er gegevens uit op te halen met behulp van `jsonNodeReference` en/of `jsonPathDefinition`, of deze stap over te slaan door deze niet op te geven in `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="49a93-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="49a93-297">Als er dubbele namen op hetzelfde niveau voorkomen, gebruikt de kopieerbewerking de laatste.</span><span class="sxs-lookup"><span data-stu-id="49a93-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="49a93-298">Eigenschapnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="49a93-298">Property names are case-sensitive.</span></span> <span data-ttu-id="49a93-299">Twee eigenschappen met dezelfde naam maar met een verschil in hoofdletters en kleine letters worden behandeld als twee afzonderlijke eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="49a93-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="49a93-300">**Voorbeeld 2: gegevens schrijven naar een JSON-bestand**</span><span class="sxs-lookup"><span data-stu-id="49a93-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="49a93-301">Als u de volgende tabel in SQL-Database hebt:</span><span class="sxs-lookup"><span data-stu-id="49a93-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="49a93-302">id</span><span class="sxs-lookup"><span data-stu-id="49a93-302">id</span></span> | <span data-ttu-id="49a93-303">order_date</span><span class="sxs-lookup"><span data-stu-id="49a93-303">order_date</span></span> | <span data-ttu-id="49a93-304">order_price</span><span class="sxs-lookup"><span data-stu-id="49a93-304">order_price</span></span> | <span data-ttu-id="49a93-305">order_by</span><span class="sxs-lookup"><span data-stu-id="49a93-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="49a93-306">1</span><span class="sxs-lookup"><span data-stu-id="49a93-306">1</span></span> | <span data-ttu-id="49a93-307">20170119</span><span class="sxs-lookup"><span data-stu-id="49a93-307">20170119</span></span> | <span data-ttu-id="49a93-308">2000</span><span class="sxs-lookup"><span data-stu-id="49a93-308">2000</span></span> | <span data-ttu-id="49a93-309">David</span><span class="sxs-lookup"><span data-stu-id="49a93-309">David</span></span> |
| <span data-ttu-id="49a93-310">2</span><span class="sxs-lookup"><span data-stu-id="49a93-310">2</span></span> | <span data-ttu-id="49a93-311">20170120</span><span class="sxs-lookup"><span data-stu-id="49a93-311">20170120</span></span> | <span data-ttu-id="49a93-312">3500</span><span class="sxs-lookup"><span data-stu-id="49a93-312">3500</span></span> | <span data-ttu-id="49a93-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="49a93-313">Patrick</span></span> |
| <span data-ttu-id="49a93-314">3</span><span class="sxs-lookup"><span data-stu-id="49a93-314">3</span></span> | <span data-ttu-id="49a93-315">20170121</span><span class="sxs-lookup"><span data-stu-id="49a93-315">20170121</span></span> | <span data-ttu-id="49a93-316">4000</span><span class="sxs-lookup"><span data-stu-id="49a93-316">4000</span></span> | <span data-ttu-id="49a93-317">Jason</span><span class="sxs-lookup"><span data-stu-id="49a93-317">Jason</span></span> |

<span data-ttu-id="49a93-318">en voor elke record die u verwacht te schrijven naar een JSON-object in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="49a93-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
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

<span data-ttu-id="49a93-319">De uitvoergegevensset met het type **JsonFormat** wordt als volgt gedefinieerd: (gedeeltelijke definitie met alleen belangrijke onderdelen).</span><span class="sxs-lookup"><span data-stu-id="49a93-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="49a93-320">Meer specifiek, `structure` sectie worden de namen van aangepaste eigenschappen gedefinieerd in doelbestand, `nestingSeparator` (standaardwaarde is ".") worden gebruikt voor het identificeren van de geneste-laag van de naam.</span><span class="sxs-lookup"><span data-stu-id="49a93-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="49a93-321">Dit gedeelte is **optioneel**, tenzij u de naam van de eigenschap wilt wijzigen ten opzichte van de naam van de bronkolom of sommige eigenschappen wilt nesten.</span><span class="sxs-lookup"><span data-stu-id="49a93-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

## <a name="avro-format"></a><span data-ttu-id="49a93-322">AVRO-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-322">AVRO format</span></span>
<span data-ttu-id="49a93-323">Als u de Avro-bestanden wilt parseren of de gegevens in Avro-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="49a93-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="49a93-324">U hoeft geen eigenschappen op te geven in het gedeelte Indeling binnen het gedeelte typeProperties.</span><span class="sxs-lookup"><span data-stu-id="49a93-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="49a93-325">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="49a93-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="49a93-326">Als u de Avro-indeling wilt gebruiken in een Hive-tabel, kunt u de [Zelfstudie voor Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe) raadplegen.</span><span class="sxs-lookup"><span data-stu-id="49a93-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="49a93-327">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="49a93-327">Note the following points:</span></span>  

* <span data-ttu-id="49a93-328">[Complexe gegevenstypen](http://avro.apache.org/docs/current/spec.html#schema_complex) worden niet ondersteund (registreert enums, matrices, kaarten, samenvoegingen, en vaste).</span><span class="sxs-lookup"><span data-stu-id="49a93-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="49a93-329">ORC-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-329">ORC format</span></span>
<span data-ttu-id="49a93-330">Als u de ORC-bestanden wilt parseren of de gegevens in ORC-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="49a93-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="49a93-331">U hoeft geen eigenschappen op te geven in het gedeelte Indeling binnen het gedeelte typeProperties.</span><span class="sxs-lookup"><span data-stu-id="49a93-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="49a93-332">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="49a93-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="49a93-333">Als u de ORC niet **ongewijzigd** kopieert tussen on-premises gegevensopslag en gegevensopslag in de cloud, moet u de JRE 8 (Java Runtime Environment) op de gatewaycomputer installeren.</span><span class="sxs-lookup"><span data-stu-id="49a93-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="49a93-334">Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway.</span><span class="sxs-lookup"><span data-stu-id="49a93-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="49a93-335">U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="49a93-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="49a93-336">Kies de juiste versie.</span><span class="sxs-lookup"><span data-stu-id="49a93-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="49a93-337">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="49a93-337">Note the following points:</span></span>

* <span data-ttu-id="49a93-338">Complexe gegevenstypen worden niet ondersteund (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="49a93-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="49a93-339">Een ORC-bestand heeft drie [opties voor compressie](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="49a93-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="49a93-340">Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="49a93-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="49a93-341">Hierbij wordt de compressiecodec in de metagegevens gebruikt om de gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="49a93-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="49a93-342">Bij het schrijven naar een ORC-bestand kiest Data Factory echter ZLIB, de standaardinstelling voor ORC.</span><span class="sxs-lookup"><span data-stu-id="49a93-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="49a93-343">Er is momenteel geen optie om dit gedrag te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="49a93-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="49a93-344">Parketvloeren-indeling</span><span class="sxs-lookup"><span data-stu-id="49a93-344">Parquet format</span></span>
<span data-ttu-id="49a93-345">Als u de Parquet-bestanden wilt parseren of de gegevens in Parquet-indeling wilt schrijven, stelt u de eigenschap `format` `type` in op **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="49a93-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="49a93-346">U hoeft geen eigenschappen op te geven in het gedeelte Indeling binnen het gedeelte typeProperties.</span><span class="sxs-lookup"><span data-stu-id="49a93-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="49a93-347">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="49a93-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="49a93-348">Als u de Parquet niet **ongewijzigd** kopieert tussen on-premises gegevensopslag en gegevensopslag in de cloud, moet u de JRE 8 (Java Runtime Environment) op de gatewaycomputer installeren.</span><span class="sxs-lookup"><span data-stu-id="49a93-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="49a93-349">Een 64-bits-gateway vereist 64-bits JRE en 32-bits JRE is vereist voor een 32-bits-gateway.</span><span class="sxs-lookup"><span data-stu-id="49a93-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="49a93-350">U vindt beide versies [hier](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="49a93-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="49a93-351">Kies de juiste versie.</span><span class="sxs-lookup"><span data-stu-id="49a93-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="49a93-352">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="49a93-352">Note the following points:</span></span>

* <span data-ttu-id="49a93-353">Complexe gegevenstypen worden niet ondersteund (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="49a93-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="49a93-354">Parquet-bestanden hebben de volgende opties voor compressie: NONE, SNAPPY, GZIP en LZO.</span><span class="sxs-lookup"><span data-stu-id="49a93-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="49a93-355">Data Factory ondersteunt het lezen van gegevens uit ORC-bestanden in een van deze gecomprimeerde indelingen.</span><span class="sxs-lookup"><span data-stu-id="49a93-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="49a93-356">Hierbij wordt de compressiecodec in de metagegevens gebruikt om de gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="49a93-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="49a93-357">Bij het schrijven naar een Parquet-bestand kiest Data Factory echter SNAPPY, de standaardinstelling voor Parquet.</span><span class="sxs-lookup"><span data-stu-id="49a93-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="49a93-358">Er is momenteel geen optie om dit gedrag te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="49a93-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="49a93-359">Compressieondersteuning</span><span class="sxs-lookup"><span data-stu-id="49a93-359">Compression support</span></span>
<span data-ttu-id="49a93-360">Verwerking van grote gegevenssets kan leiden tot i/o en netwerk knelpunten.</span><span class="sxs-lookup"><span data-stu-id="49a93-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="49a93-361">Daarom kunt gecomprimeerde gegevens via stores niet alleen versnellen gegevensoverdracht via het netwerk en schijfruimte te besparen, maar ook aanzienlijke prestatieverbeteringen bij het verwerken van big data te brengen.</span><span class="sxs-lookup"><span data-stu-id="49a93-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="49a93-362">Compressie wordt momenteel ondersteund voor de opgeslagen gegevens op basis van bestanden zoals Azure Blob- of On-premises bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="49a93-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="49a93-363">Als u compressie voor een gegevensset, gebruiken de **compressie** eigenschap in de gegevensset JSON zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="49a93-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="49a93-364">Stel dat de voorbeeldgegevensset wordt gebruikt als de uitvoer van een kopieeractiviteit, wordt de kopieerbewerking de uitvoergegevens, comprimeren met GZIP codec met optimale verhouding en vervolgens de gecomprimeerde gegevens schrijven naar een bestand met de naam pagecounts.csv.gz in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="49a93-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="49a93-365">Compressie-instellingen worden niet ondersteund voor gegevens in de **AvroFormat**, **OrcFormat**, of **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="49a93-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="49a93-366">Bij het lezen van bestanden in de volgende indelingen worden Data Factory detecteert en de compressiecodec gebruikt in de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="49a93-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="49a93-367">Bij het schrijven naar de bestanden in de volgende indelingen, kiest Data Factory de codec standaard compressie voor die indeling.</span><span class="sxs-lookup"><span data-stu-id="49a93-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="49a93-368">Bijvoorbeeld, ZLIB voor OrcFormat en SNAPPY voor ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="49a93-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="49a93-369">De **compressie** sectie heeft twee eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="49a93-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="49a93-370">**Type:** de compressiecodec die kan worden **GZIP**, **Deflate**, **BZIP2**, of **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="49a93-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="49a93-371">**Niveau:** de compressieverhouding die kan worden **optimale** of **snelst**.</span><span class="sxs-lookup"><span data-stu-id="49a93-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="49a93-372">**Snelste:** de compressie-bewerking moet uitvoeren zo snel mogelijk, zelfs als het resulterende bestand is niet optimaal gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="49a93-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="49a93-373">**Optimale**: de compressie-bewerking moet worden optimaal gecomprimeerd, zelfs als de bewerking duurt het langer om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="49a93-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="49a93-374">Zie voor meer informatie [compressieniveau](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="49a93-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="49a93-375">Wanneer u opgeeft `compression` eigenschap in een JSON-invoer gegevensset, de pijplijn gecomprimeerde gegevens van de bron; kan lezen en wanneer u de eigenschap in een uitvoergegevensset JSON opgeeft, met de kopieerbewerking gecomprimeerde gegevens kunt schrijven naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="49a93-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="49a93-376">Hier volgen enkele voorbeeldscenario's:</span><span class="sxs-lookup"><span data-stu-id="49a93-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="49a93-377">Lees GZIP gecomprimeerde gegevens van een Azure-blob decomprimeren en result-gegevens schrijven naar een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="49a93-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="49a93-378">U definieert de invoer Azure Blob-gegevensset met de `compression` `type` JSON eigenschap GZIP.</span><span class="sxs-lookup"><span data-stu-id="49a93-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="49a93-379">Gegevens lezen uit een tekstbestand van on-premises bestandssysteem, comprimeren met behulp van GZip-indeling en de gecomprimeerde gegevens schrijven naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="49a93-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="49a93-380">U definieert een uitvoer-Azure Blob-gegevensset met de `compression` `type` JSON eigenschap GZip.</span><span class="sxs-lookup"><span data-stu-id="49a93-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="49a93-381">ZIP-bestand lezen van FTP-server decomprimeren ophalen van de bestanden in en de bestanden neerzetten in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="49a93-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="49a93-382">Definieert u een FTP-invoergegevensset met de `compression` `type` JSON eigenschap ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="49a93-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="49a93-383">Lezen van een GZIP-gecomprimeerde gegevens van een Azure-blob, decomprimeren, comprimeren met behulp van BZIP2 en result-gegevens schrijven naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="49a93-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="49a93-384">U definieert de invoer Azure Blob-gegevensset met `compression` `type` ingesteld op GZIP en de uitvoergegevensset met `compression` `type` ingesteld op BZIP2 in dit geval.</span><span class="sxs-lookup"><span data-stu-id="49a93-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="49a93-385">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49a93-385">Next steps</span></span>
<span data-ttu-id="49a93-386">Zie de volgende artikelen voor bestandsgebaseerde gegevensarchieven die door Azure Data Factory worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="49a93-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="49a93-387">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="49a93-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="49a93-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="49a93-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="49a93-389">FTP</span><span class="sxs-lookup"><span data-stu-id="49a93-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="49a93-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="49a93-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="49a93-391">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="49a93-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="49a93-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="49a93-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
