---
title: aaaU SQL programmeerbaarheid handleiding voor Azure Data Lake | Microsoft Docs
description: Meer informatie over Hallo set van services in Azure Data Lake waarmee u toocreate een platform voor big data cloud-gebaseerde.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="b321a-103">Handleiding voor het programmeren van U-SQL</span><span class="sxs-lookup"><span data-stu-id="b321a-103">U-SQL programmability guide</span></span>

<span data-ttu-id="b321a-104">U-SQL is een querytaal die ontworpen voor big data-type van werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="b321a-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="b321a-105">Een van de unieke kenmerken Hallo van U-SQL is Hallo combinatie van Hallo SQL-achtige declaratieve taal met Hallo uitbreiden en programmeren die wordt geleverd door C#.</span><span class="sxs-lookup"><span data-stu-id="b321a-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="b321a-106">In deze handleiding richten we op Hallo uitbreiden en programmeren van Hallo U-SQL-taal die wordt ingeschakeld met C#.</span><span class="sxs-lookup"><span data-stu-id="b321a-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="b321a-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b321a-107">Requirements</span></span>

<span data-ttu-id="b321a-108">Download en installeer [Azure Data Lake Tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="b321a-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="b321a-109">Aan de slag met U-SQL</span><span class="sxs-lookup"><span data-stu-id="b321a-109">Get started with U-SQL</span></span>  

<span data-ttu-id="b321a-110">Bekijk Hallo volgende U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="b321a-110">Let’s look at hello following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="b321a-111">Hiermee definieert u een rijenset aangeroepen @a en maakt een rijenset aangeroepen @results van @a.</span><span class="sxs-lookup"><span data-stu-id="b321a-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="b321a-112">C#-typen en expressies in de U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="b321a-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="b321a-113">Een U-SQL-expressie is een expressie C# in combinatie met logische U-SQL-bewerkingen zoals `AND`, `OR`, en `NOT`.</span><span class="sxs-lookup"><span data-stu-id="b321a-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="b321a-114">U-SQL-expressies kunnen worden gebruikt met SELECT-, uitpakken, waarin, ONDERVINDT, GROEPEREN en DECLAREREN.</span><span class="sxs-lookup"><span data-stu-id="b321a-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="b321a-115">Bijvoorbeeld parseert Hallo na script een tekenreeks een DateTime-waarde in Hallo SELECT-component.</span><span class="sxs-lookup"><span data-stu-id="b321a-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="b321a-116">Hallo parseert volgende script een tekenreeks in een instructie DECLARE een DateTime-waarde.</span><span class="sxs-lookup"><span data-stu-id="b321a-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="b321a-117">C#-expressies gebruiken voor de conversie van het gegevenstype</span><span class="sxs-lookup"><span data-stu-id="b321a-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="b321a-118">Hallo volgende voorbeeld laat zien hoe u een conversie van datum-/ kunt doen met behulp van C#-expressies.</span><span class="sxs-lookup"><span data-stu-id="b321a-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="b321a-119">In dit scenario is datetime tekenreeksgegevens geconverteerde toostandard datetime met de notatie van de tijd 00:00:00 middernacht.</span><span class="sxs-lookup"><span data-stu-id="b321a-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="b321a-120">C#-expressies gebruiken voor de datum van vandaag</span><span class="sxs-lookup"><span data-stu-id="b321a-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="b321a-121">toopull datum van vandaag, kunnen we gebruiken Hallo C#-expressie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="b321a-122">Hier volgt een voorbeeld van hoe toouse deze expressie in een script:</span><span class="sxs-lookup"><span data-stu-id="b321a-122">Here's an example of how toouse this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="b321a-123">Met behulp van .NET-assembly 's</span><span class="sxs-lookup"><span data-stu-id="b321a-123">Using .NET assemblies</span></span>
<span data-ttu-id="b321a-124">U-SQL-uitbreidbaarheidsmodel is sterk afhankelijk van Hallo mogelijkheid tooadd aangepaste code.</span><span class="sxs-lookup"><span data-stu-id="b321a-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="b321a-125">Op dit moment kunt biedt U-SQL u eenvoudige manieren tooadd uw eigen Microsoft. De code op basis van NET (met name, C#).</span><span class="sxs-lookup"><span data-stu-id="b321a-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="b321a-126">U kunt echter ook aangepaste code die geschreven in .NET-talen, zoals of traditiegetrouw F # toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b321a-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="b321a-127">Registreren van een .NET-assembly</span><span class="sxs-lookup"><span data-stu-id="b321a-127">Register a .NET assembly</span></span>

<span data-ttu-id="b321a-128">Hallo CREATE ASSEMBLY instructie tooplace een .NET-assembly in een U-SQL-Database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b321a-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="b321a-129">Nadat een assembly een database is, kunnen U-SQL-scripts die assembly's gebruiken met behulp van Hallo referentie-ASSEMBLY-instructie.</span><span class="sxs-lookup"><span data-stu-id="b321a-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="b321a-130">Hallo van de volgende code wordt getoond hoe tooregister een assembly:</span><span class="sxs-lookup"><span data-stu-id="b321a-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="b321a-131">Hallo van de volgende code wordt getoond hoe tooreference een assembly:</span><span class="sxs-lookup"><span data-stu-id="b321a-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="b321a-132">Raadpleeg Hallo [assembly registration instructies](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) die worden in dit onderwerp in meer detail behandeld.</span><span class="sxs-lookup"><span data-stu-id="b321a-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="b321a-133">Assembly-versiebeheer gebruiken</span><span class="sxs-lookup"><span data-stu-id="b321a-133">Use assembly versioning</span></span>
<span data-ttu-id="b321a-134">U-SQL gebruikt op dit moment Hallo .NET Framework versie 4.5.</span><span class="sxs-lookup"><span data-stu-id="b321a-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="b321a-135">Dus zorg ervoor dat uw eigen assembly's compatibel met deze versie van Hallo-runtime zijn.</span><span class="sxs-lookup"><span data-stu-id="b321a-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="b321a-136">Zoals eerder gezegd code van de U-SQL wordt uitgevoerd in een 64-bits (x 64)-indeling.</span><span class="sxs-lookup"><span data-stu-id="b321a-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="b321a-137">Dus zorg ervoor dat uw code gecompileerde toorun op x64.</span><span class="sxs-lookup"><span data-stu-id="b321a-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="b321a-138">Anders krijgt u een onjuiste indelingsfout Hallo eerder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b321a-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="b321a-139">Elke assembly DLL-bestand geüpload en resource-bestand, zoals een andere runtime, een systeemeigen assembly of een configuratiebestand mag maximaal 400 MB.</span><span class="sxs-lookup"><span data-stu-id="b321a-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="b321a-140">totale grootte van de Hallo van geïmplementeerde resources, hetzij via RESOURCE implementeren of een verwijzingen tooassemblies en de bijbehorende extra bestanden niet meer dan 3 GB.</span><span class="sxs-lookup"><span data-stu-id="b321a-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="b321a-141">Ten slotte Opmerking elke U-SQL-database mogen slechts één versie van de opgegeven assembly's.</span><span class="sxs-lookup"><span data-stu-id="b321a-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="b321a-142">Bijvoorbeeld, als u zowel versie 7 als versie 8 Hallo NewtonSoft Json.Net-bibliotheek moet, moet u tooregister ze in twee verschillende databases.</span><span class="sxs-lookup"><span data-stu-id="b321a-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="b321a-143">Bovendien kan elk script alleen tooone versie van een bepaalde assembly DLL verwijzen.</span><span class="sxs-lookup"><span data-stu-id="b321a-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="b321a-144">In dit opzicht volgt U-SQL Hallo C#-assembly beheer- en versiebeheer semantiek.</span><span class="sxs-lookup"><span data-stu-id="b321a-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="b321a-145">Gebruik van de gebruiker gedefinieerde functies: UDF</span><span class="sxs-lookup"><span data-stu-id="b321a-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="b321a-146">U-SQL-gebruiker gedefinieerde functies of UDF, programmeert routines die parameters accepteren, het uitvoeren van een actie (zoals een complexe berekening) en het Hallo resultaat van deze actie als wanneer u een waarde te retourneren.</span><span class="sxs-lookup"><span data-stu-id="b321a-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="b321a-147">Hallo retourneren waarde van UDF kan alleen één scalair zijn.</span><span class="sxs-lookup"><span data-stu-id="b321a-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="b321a-148">U-SQL-UDF kan worden aangeroepen in base U-SQL-script zoals elke andere C# scalaire functie.</span><span class="sxs-lookup"><span data-stu-id="b321a-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="b321a-149">Het is raadzaam dat u de gebruiker gedefinieerde U-SQL-functies als initialiseren **openbare** en **statische**.</span><span class="sxs-lookup"><span data-stu-id="b321a-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="b321a-150">Eerste bekijken we Hallo eenvoudig voorbeeld van het maken van een UDF.</span><span class="sxs-lookup"><span data-stu-id="b321a-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="b321a-151">In dit scenario use case moet toodetermine Hallo fiscale periode, met inbegrip van Hallo Boekkwartaal en boekmaand van Hallo eerste aanmelden voor een specifieke gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="b321a-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="b321a-152">Hallo is eerste boekmaand van Hallo jaar in ons scenario juni.</span><span class="sxs-lookup"><span data-stu-id="b321a-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="b321a-153">toocalculate fiscale periode, stellen we Hallo C#-functie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="b321a-154">Gewoon boekmaand en kwartaal berekend en retourneert een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="b321a-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="b321a-155">We gebruiken 'Q1:P1' voor juni, Hallo eerste maand van Hallo eerste kwartaal.</span><span class="sxs-lookup"><span data-stu-id="b321a-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="b321a-156">Voor juli moeten we gebruiken 'Q1:P2', enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b321a-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="b321a-157">Dit is een reguliere C#-functie we continu toouse zijn in de U-SQL-project.</span><span class="sxs-lookup"><span data-stu-id="b321a-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="b321a-158">Hier ziet u hoe Hallo code-behind sectie eruitziet in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="b321a-158">Here is how hello code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="b321a-159">Nu gaan we toocall deze functie van Hallo base U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="b321a-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="b321a-160">toodo, hebben we tooprovide na een volledig gekwalificeerde naam voor de functie hello, inclusief Hallo-naamruimte die in dit geval NameSpace.Class.Function(parameter) is.</span><span class="sxs-lookup"><span data-stu-id="b321a-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="b321a-161">Hieronder vindt u Hallo werkelijke U-SQL base script:</span><span class="sxs-lookup"><span data-stu-id="b321a-161">Following is hello actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="b321a-162">Dit is het uitvoerbestand Hallo Hallo uitvoeren van scripts:</span><span class="sxs-lookup"><span data-stu-id="b321a-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="b321a-163">Dit voorbeeld wordt een eenvoudig gebruik van inline UDF in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b321a-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="b321a-164">Status tussen UDF aanroepen houden</span><span class="sxs-lookup"><span data-stu-id="b321a-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="b321a-165">U-SQL C# programmeerbare objecten kunnen worden meer geavanceerde, met behulp van interactiviteit via Hallo code-behind globale variabelen.</span><span class="sxs-lookup"><span data-stu-id="b321a-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="b321a-166">Bekijk Hallo use case bedrijfsscenario te volgen.</span><span class="sxs-lookup"><span data-stu-id="b321a-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="b321a-167">In grote organisaties kunnen gebruikers schakelen tussen varianten van interne toepassingen.</span><span class="sxs-lookup"><span data-stu-id="b321a-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="b321a-168">Voorbeelden Microsoft Dynamics CRM en Power BI.</span><span class="sxs-lookup"><span data-stu-id="b321a-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="b321a-169">Klanten kunt tooapply een analyse telemetrie van hoe gebruikers tussen verschillende toepassingen schakelen, welke gebruik Hallo trends weet, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b321a-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="b321a-170">Hello dient voor bedrijven Hallo toooptimize toepassingsgebruik.</span><span class="sxs-lookup"><span data-stu-id="b321a-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="b321a-171">Ze ook verstandig toocombine verschillende toepassingen of specifieke routines voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="b321a-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="b321a-172">tooachieve deze doelstelling krijgen we hebben toodetermine sessie-id's en vertragingstijd tussen Hallo laatste sessie die is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="b321a-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="b321a-173">We moet toofind een vorige aanmelden en wijs deze aanmelden tooall-sessies die worden gegenereerd toohello dezelfde toepassing.</span><span class="sxs-lookup"><span data-stu-id="b321a-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="b321a-174">Hallo eerste uitdaging is dat base U-SQL-script niet is toegestaan ons tooapply berekeningen via al berekende kolommen met de functie LAG.</span><span class="sxs-lookup"><span data-stu-id="b321a-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="b321a-175">Hallo tweede uitdaging is dat we tookeep Hallo bepaalde sessie voor alle sessies binnen Hallo hebben dezelfde periode.</span><span class="sxs-lookup"><span data-stu-id="b321a-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="b321a-176">toosolve dit probleem, gebruiken we een globale variabele in een code-behind-sectie: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="b321a-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="b321a-177">Deze globale variabele is toegepaste toohello volledige rijenset tijdens de uitvoering van het script.</span><span class="sxs-lookup"><span data-stu-id="b321a-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="b321a-178">Hier volgt Hallo code-behind sectie van ons U-SQL-programma:</span><span class="sxs-lookup"><span data-stu-id="b321a-178">Here is hello code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="b321a-179">In dit voorbeeld toont de globale variabele Hallo `static public string globalSession;` gebruikt in Hallo `getStampUserSession` functie en het ophalen van opnieuw geïnitialiseerd elke keer Hallo sessie parameter wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b321a-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="b321a-180">Hallo base U-SQL-script is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-180">hello U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="b321a-181">De functie `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` hier tijdens de Hallo tweede geheugen rijenset berekening wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b321a-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="b321a-182">Dit wordt doorgegeven Hallo `UserSessionTimestamp` kolom en retourneert de waarde pas Hallo `UserSessionTimestamp` is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="b321a-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="b321a-183">Hallo-uitvoerbestand is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-183">hello output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="b321a-184">In dit voorbeeld demonstreert een gecompliceerdere use case-scenario waarin we een globale variabele gebruiken in een code-behind sectie die is toegepast toohello hele geheugen rijenset.</span><span class="sxs-lookup"><span data-stu-id="b321a-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="b321a-185">Gebruik van de gebruiker gedefinieerde typen: UDT</span><span class="sxs-lookup"><span data-stu-id="b321a-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="b321a-186">Gebruiker gedefinieerde typen of UDT, is een andere programmeerbaarheidsfunctie van U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b321a-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="b321a-187">U-SQL-UDT fungeert als een reguliere C# gebruiker gedefinieerd type.</span><span class="sxs-lookup"><span data-stu-id="b321a-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="b321a-188">C# is een sterk getypeerde taal waarmee ingebouwde en aangepaste gebruiker gedefinieerde typen hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b321a-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="b321a-189">U-SQL kan niet impliciet serialiseren of deserialiseren willekeurige UDT's wanneer Hallo UDT wordt doorgegeven tussen hoekpunten in rijensets.</span><span class="sxs-lookup"><span data-stu-id="b321a-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="b321a-190">Dit betekent dat Hallo gebruiker tooprovide een expliciete formatter met Hallo IFormatter-interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="b321a-191">Dit biedt U-SQL Hallo serialiseren en deserialiseren methoden voor het Hallo UDT.</span><span class="sxs-lookup"><span data-stu-id="b321a-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="b321a-192">Serialiseren U-SQL ingebouwde extractie- en outputters momenteel kan niet of deserialiseren UDT gegevens tooor zelfs Hallo IFormatter set bestanden.</span><span class="sxs-lookup"><span data-stu-id="b321a-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="b321a-193">Wanneer u schrijft UDT gegevensbestand tooa Hello uitvoer-instructie of gelezen heeft met een zelfstandig uitpakken, hebt u toopass als een tekenreeks of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="b321a-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="b321a-194">Vervolgens aanroepen Hallo serialisatie en expliciet code (dat wil zeggen, de Hallo UDT ToString() methode) heeft het deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="b321a-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="b321a-195">Gebruiker gedefinieerde extractie- en outputters op Hallo andere kunnen hand, lezen en schrijven UDT's.</span><span class="sxs-lookup"><span data-stu-id="b321a-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="b321a-196">Als we toouse UDT in zelfstandig uitpakken of OUTPUTTER (buiten het vorige selecteren), proberen zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b321a-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="b321a-197">We ontvangen Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="b321a-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="b321a-198">toowork met UDT in outputter we hebben tooserialize het toostring met methode ToString() hello of een aangepaste outputter maken.</span><span class="sxs-lookup"><span data-stu-id="b321a-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="b321a-199">UDT's worden momenteel niet gebruikt in de GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="b321a-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="b321a-200">Als UDT wordt gebruikt in de GROUP BY, wordt de volgende fout Hallo gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="b321a-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="b321a-201">een UDT toodefine, hebben we naar:</span><span class="sxs-lookup"><span data-stu-id="b321a-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="b321a-202">Hallo naamruimten volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b321a-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="b321a-203">Voeg `Microsoft.Analytics.Interfaces`, die is vereist voor Hallo UDT-interfaces.</span><span class="sxs-lookup"><span data-stu-id="b321a-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="b321a-204">Bovendien `System.IO` mogelijk nodig toodefine hello IFormatter interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="b321a-205">Een type gebruikt gedefinieerd met het kenmerk SqlUserDefinedType definiëren.</span><span class="sxs-lookup"><span data-stu-id="b321a-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="b321a-206">**SqlUserDefinedType** gebruikte toomark de definitie van een type in een assembly als een gebruiker gedefinieerde type (UDT) is in de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="b321a-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="b321a-207">Hallo-eigenschappen op Hallo kenmerk weerspiegelen Hallo fysieke kenmerken van Hallo UDT.</span><span class="sxs-lookup"><span data-stu-id="b321a-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="b321a-208">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-208">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-209">SqlUserDefinedType is een vereist kenmerk voor UDT-definitie.</span><span class="sxs-lookup"><span data-stu-id="b321a-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="b321a-210">Hallo-constructor van Hallo klasse:</span><span class="sxs-lookup"><span data-stu-id="b321a-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="b321a-211">SqlUserDefinedTypeAttribute (type-indeling)</span><span class="sxs-lookup"><span data-stu-id="b321a-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="b321a-212">Typ formatter: parameter toodefine een formatter UDT--vereist in het bijzonder Hallo type Hallo `IFormatter` interface hier moet worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b321a-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="b321a-213">Typische UDT vereist ook definitie van Hallo IFormatter interface, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="b321a-214">Hallo `IFormatter` interface serialiseert en ongedaan serialiseert een objectgrafiek met Hallo hoofdtype van \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="b321a-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="b321a-215">\<typeparam name = "T" > Hallo hoofdtype voor Hallo object grafiek tooserialize en te deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="b321a-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="b321a-216">**Deserialiseren**: ongedaan serialiseert Hallo gegevens op Hallo opgegeven stroom en reconstitutes Hallo graph-objecten.</span><span class="sxs-lookup"><span data-stu-id="b321a-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="b321a-217">**Serialiseren**: een object of de grafiek van objecten, serialiseert Hello opgegeven hoofdmap toohello opgegeven stroom.</span><span class="sxs-lookup"><span data-stu-id="b321a-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="b321a-218">`MyType`exemplaar: exemplaar van het Hallo-type.</span><span class="sxs-lookup"><span data-stu-id="b321a-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="b321a-219">`IColumnWriter`schrijver / `IColumnReader` lezer: Hallo onderliggende stroom van de kolom.</span><span class="sxs-lookup"><span data-stu-id="b321a-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="b321a-220">`ISerializationContext`context: Enum die definieert een aantal vlaggen waarmee de Hallo bron of bestemming context voor Hallo stroom tijdens de serialisatie wordt.</span><span class="sxs-lookup"><span data-stu-id="b321a-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="b321a-221">**Tussenliggende**: Hiermee geeft u op die Hallo bron of bestemming context is geen permanente opslag.</span><span class="sxs-lookup"><span data-stu-id="b321a-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="b321a-222">**Persistentie**: Hiermee geeft u op die Hallo bron of bestemming context is een persistente archief.</span><span class="sxs-lookup"><span data-stu-id="b321a-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="b321a-223">Als een reguliere C#-type, een U-SQL-UDT-definitie kunt opnemen overschrijvingen voor operators zoals +/ == /! =.</span><span class="sxs-lookup"><span data-stu-id="b321a-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="b321a-224">Het kan ook betekenen dat statische methoden.</span><span class="sxs-lookup"><span data-stu-id="b321a-224">It can also include static methods.</span></span> <span data-ttu-id="b321a-225">Bijvoorbeeld, als we gaan toouse deze UDT als een parameter tooa statistische functie MIN U-SQL, we hebben toodefine < operator overschrijven.</span><span class="sxs-lookup"><span data-stu-id="b321a-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="b321a-226">Eerder in deze handleiding wordt gedemonstreerd een voorbeeld van de fiscale periode-id van de specifieke datum Hallo Hallo indeling Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="b321a-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="b321a-227">Hallo volgende voorbeeld ziet u hoe toodefine een aangepast type voor fiscale periode waarden.</span><span class="sxs-lookup"><span data-stu-id="b321a-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="b321a-228">Hieronder volgt een voorbeeld van een code-behind sectie met aangepaste UDT en IFormatter-interface:</span><span class="sxs-lookup"><span data-stu-id="b321a-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="b321a-229">Hallo gedefinieerd type bevat twee getallen: kwartaal en maand.</span><span class="sxs-lookup"><span data-stu-id="b321a-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="b321a-230">Operators == /! = / > / < en statische methode ToString() Hier worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="b321a-231">Zoals eerder gezegd, UDT kan worden gebruikt in expressies voor SELECT, maar kan niet worden gebruikt in OUTPUTTER/zelfstandig uitpakken zonder aangepaste serialisatie.</span><span class="sxs-lookup"><span data-stu-id="b321a-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="b321a-232">Het bevat toobe geserialiseerd als een tekenreeks met ToString() of gebruikt met een aangepaste OUTPUTTER/zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="b321a-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="b321a-233">Nu gaan we gebruik van UDT bespreken.</span><span class="sxs-lookup"><span data-stu-id="b321a-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="b321a-234">In een sectie code-behind we onze GetFiscalPeriod functie toohello volgende gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="b321a-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="b321a-235">Zoals u ziet, wordt het Hallo-waarde van het type van onze FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="b321a-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="b321a-236">Hier bieden we een voorbeeld van hoe de toouse is verder in base U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="b321a-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="b321a-237">In dit voorbeeld laat zien dat verschillende vormen van UDT-aanroep van U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="b321a-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="b321a-238">Hier volgt een voorbeeld van een volledige code-behind-sectie:</span><span class="sxs-lookup"><span data-stu-id="b321a-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="b321a-239">Gebruik van de gebruiker gedefinieerde aggregaties: UDAGG</span><span class="sxs-lookup"><span data-stu-id="b321a-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="b321a-240">Gebruiker gedefinieerde aggregaties zijn niet out-of-the-box met U-SQL is geen aggregatie-gerelateerde functies die zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="b321a-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="b321a-241">Hallo voorbeeld kan worden een cumulatieve tooperform aangepaste math berekeningen, samenvoegingen van tekenreeksen bewerkingen met tekenreeksen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="b321a-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="b321a-242">definitie van de gebruiker gedefinieerde cumulatieve basisklasse Hallo is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-242">hello user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="b321a-243">**SqlUserDefinedAggregate** geeft aan dat het Hallo-type moet worden geregistreerd als een gebruiker gedefinieerde aggregatie.</span><span class="sxs-lookup"><span data-stu-id="b321a-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="b321a-244">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-244">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-245">SqlUserDefinedType kenmerk **optionele** voor UDAGG definitie.</span><span class="sxs-lookup"><span data-stu-id="b321a-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="b321a-246">Hallo basisklasse kunt u abstracte parameters toopass drie: twee als invoerparameters en één als Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="b321a-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="b321a-247">Hallo-gegevenstypen zijn variabel en tijdens klassenovername moeten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-247">hello data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="b321a-248">**Init** roept eenmaal voor elke groep tijdens berekening.</span><span class="sxs-lookup"><span data-stu-id="b321a-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="b321a-249">Het biedt een initialisatieroutine voor elke groep aggregatie.</span><span class="sxs-lookup"><span data-stu-id="b321a-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="b321a-250">**Verzamelt** één keer uitgevoerd voor elke waarde.</span><span class="sxs-lookup"><span data-stu-id="b321a-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="b321a-251">Biedt de belangrijkste functionaliteit Hallo voor Hallo aggregatie-algoritme.</span><span class="sxs-lookup"><span data-stu-id="b321a-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="b321a-252">Het kan gebruikte tooaggregate waarden met verschillende gegevenstypen die zijn gedefinieerd tijdens klassenovername zijn.</span><span class="sxs-lookup"><span data-stu-id="b321a-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="b321a-253">Deze kan twee parameters van de variabele gegevenstypen accepteren.</span><span class="sxs-lookup"><span data-stu-id="b321a-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="b321a-254">**Beëindigen** eenmaal per groep aan Hallo einde van het verwerken van toooutput Hallo resultaat voor elke groep aggregatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="b321a-255">toodeclare juiste invoer en uitvoer-gegevenstypen, gebruikt de klassendefinitie Hallo als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="b321a-256">T1: De eerste parameter tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="b321a-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="b321a-257">T2: De eerste parameter tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="b321a-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="b321a-258">TResult: Retourtype van beëindigen</span><span class="sxs-lookup"><span data-stu-id="b321a-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="b321a-259">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b321a-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="b321a-260">of</span><span class="sxs-lookup"><span data-stu-id="b321a-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="b321a-261">Gebruik UDAGG in U-SQL</span><span class="sxs-lookup"><span data-stu-id="b321a-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="b321a-262">toouse UDAGG, eerst Definieer dit in code-behind of ernaar verwijzen vanuit Hallo-bestaande programmeerbaarheid DLL zoals hierboven besproken.</span><span class="sxs-lookup"><span data-stu-id="b321a-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="b321a-263">Gebruik vervolgens Hallo de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="b321a-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="b321a-264">Hier volgt een voorbeeld van UDAGG:</span><span class="sxs-lookup"><span data-stu-id="b321a-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="b321a-265">En U-SQL-script gebaseerd:</span><span class="sxs-lookup"><span data-stu-id="b321a-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="b321a-266">In dit scenario use case samenvoegen we klasse GUID's voor specifieke gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="b321a-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="b321a-267">Gebruik van de gebruiker gedefinieerde objecten: UDO</span><span class="sxs-lookup"><span data-stu-id="b321a-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="b321a-268">U-SQL kunt u toodefine aangepaste programmeerbaarheid objecten, die de gebruiker gedefinieerde objecten of UDO worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="b321a-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="b321a-269">Hallo Hier volgt een lijst met UDO in U-SQL:</span><span class="sxs-lookup"><span data-stu-id="b321a-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="b321a-270">Gebruiker gedefinieerde extractie</span><span class="sxs-lookup"><span data-stu-id="b321a-270">User-defined extractors</span></span>
    * <span data-ttu-id="b321a-271">Uitpakken per rij</span><span class="sxs-lookup"><span data-stu-id="b321a-271">Extract row by row</span></span>
    * <span data-ttu-id="b321a-272">Tooimplement gegevens uitpakken van bestanden met aangepaste gestructureerde gebruikt</span><span class="sxs-lookup"><span data-stu-id="b321a-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="b321a-273">Gebruiker gedefinieerde outputters</span><span class="sxs-lookup"><span data-stu-id="b321a-273">User-defined outputters</span></span>
    * <span data-ttu-id="b321a-274">Uitvoer per rij</span><span class="sxs-lookup"><span data-stu-id="b321a-274">Output row by row</span></span>
    * <span data-ttu-id="b321a-275">Gebruikt de aangepaste gegevenstypen toooutput of aangepaste bestandsindelingen</span><span class="sxs-lookup"><span data-stu-id="b321a-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="b321a-276">Gebruiker gedefinieerde processors</span><span class="sxs-lookup"><span data-stu-id="b321a-276">User-defined processors</span></span>
    * <span data-ttu-id="b321a-277">Één rij en produceert één rij</span><span class="sxs-lookup"><span data-stu-id="b321a-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="b321a-278">Gebruikte tooreduce Hallo aantal kolommen of produceren van nieuwe kolommen met waarden die zijn afgeleid van een bestaande set kolommen</span><span class="sxs-lookup"><span data-stu-id="b321a-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="b321a-279">Gebruiker gedefinieerde appliers</span><span class="sxs-lookup"><span data-stu-id="b321a-279">User-defined appliers</span></span>
    * <span data-ttu-id="b321a-280">Één rij en produceert 0 toon rijen</span><span class="sxs-lookup"><span data-stu-id="b321a-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="b321a-281">Gebruikt met buitenste/CROSS toepassen</span><span class="sxs-lookup"><span data-stu-id="b321a-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="b321a-282">Gebruiker gedefinieerde combiners</span><span class="sxs-lookup"><span data-stu-id="b321a-282">User-defined combiners</span></span>
    * <span data-ttu-id="b321a-283">Combineert rijensets--gebruiker gedefinieerde JOINs</span><span class="sxs-lookup"><span data-stu-id="b321a-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="b321a-284">Gebruiker gedefinieerde verkleiningstoestellen</span><span class="sxs-lookup"><span data-stu-id="b321a-284">User-defined reducers</span></span>
    * <span data-ttu-id="b321a-285">N rijen en produceert één rij</span><span class="sxs-lookup"><span data-stu-id="b321a-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="b321a-286">Tooreduce hello aantal rijen dat wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="b321a-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="b321a-287">UDO wordt normaal gesproken expliciet aangeroepen in de U-SQL-script als onderdeel van Hallo U-SQL-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="b321a-288">UITPAKKEN</span><span class="sxs-lookup"><span data-stu-id="b321a-288">EXTRACT</span></span>
* <span data-ttu-id="b321a-289">UITVOER</span><span class="sxs-lookup"><span data-stu-id="b321a-289">OUTPUT</span></span>
* <span data-ttu-id="b321a-290">PROCES</span><span class="sxs-lookup"><span data-stu-id="b321a-290">PROCESS</span></span>
* <span data-ttu-id="b321a-291">COMBINEREN</span><span class="sxs-lookup"><span data-stu-id="b321a-291">COMBINE</span></span>
* <span data-ttu-id="b321a-292">VERMINDEREN</span><span class="sxs-lookup"><span data-stu-id="b321a-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="b321a-293">De UDO zijn beperkt tooconsume 0,5 Gb geheugen.</span><span class="sxs-lookup"><span data-stu-id="b321a-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="b321a-294">Deze beperking geheugen toolocal uitvoeringen niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="b321a-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="b321a-295">Gebruik van de gebruiker gedefinieerde extractie</span><span class="sxs-lookup"><span data-stu-id="b321a-295">Use user-defined extractors</span></span>
<span data-ttu-id="b321a-296">U-SQL kunt u tooimport externe gegevens door het gebruik van een instructie uitpakken.</span><span class="sxs-lookup"><span data-stu-id="b321a-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="b321a-297">Een instructie EXTRACT kunt ingebouwde UDO extractie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b321a-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="b321a-298">*Extractors.Text()*: extractie van tekstbestanden met scheidingstekens van andere coderingen biedt.</span><span class="sxs-lookup"><span data-stu-id="b321a-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="b321a-299">*Extractors.Csv()*: uitpakken van het bestand met door komma's gescheiden waarden (CSV)-bestanden van andere coderingen biedt.</span><span class="sxs-lookup"><span data-stu-id="b321a-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="b321a-300">*Extractors.Tsv()*: extractie van tabblad gescheiden waarden (TSV)-bestanden van andere coderingen biedt.</span><span class="sxs-lookup"><span data-stu-id="b321a-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="b321a-301">Het kan zijn nuttig toodevelop een aangepaste zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="b321a-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="b321a-302">Dit kan nuttig zijn bij het importeren van gegevens als we willen toodo van Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="b321a-303">Invoer gegevens wijzigen door het splitsen van kolommen en afzonderlijke waarden te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b321a-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="b321a-304">Hallo processorfunctionaliteit is het beter voor het combineren van kolommen.</span><span class="sxs-lookup"><span data-stu-id="b321a-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="b321a-305">Niet-gestructureerde gegevens zoals webpagina's en e-mailberichten of niet semi-gestructureerde gegevens, zoals XML/JSON parseren.</span><span class="sxs-lookup"><span data-stu-id="b321a-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="b321a-306">Parseren van gegevens in niet-ondersteunde codering.</span><span class="sxs-lookup"><span data-stu-id="b321a-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="b321a-307">een gebruiker gedefinieerde zelfstandig uitpakken, toodefine of USIEF, moeten we toocreate een `IExtractor` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="b321a-308">Alle parameters toohello zelfstandig uitpakken, zoals gedefinieerd in de constructor van de klasse Hallo Hallo toobe kolom/rij scheidingstekens en codering, moeten worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="b321a-309">Hallo `IExtractor` interface moet ook een definitie voor Hallo bevatten `IEnumerable<IRow>` overschrijven als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="b321a-310">Hallo **SqlUserDefinedExtractor** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een door de gebruiker gedefinieerde zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="b321a-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="b321a-311">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-311">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-312">SqlUserDefinedExtractor is een optionele kenmerk voor de definitie van USIEF.</span><span class="sxs-lookup"><span data-stu-id="b321a-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="b321a-313">Het toodefine AtomicFileProcessing eigenschap gebruikt voor Hallo USIEF object.</span><span class="sxs-lookup"><span data-stu-id="b321a-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="b321a-314">BOOL AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="b321a-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="b321a-315">**de waarde True** = geeft aan dat deze zelfstandig uitpakken atomic invoerbestanden (JSON, XML,...) is vereist</span><span class="sxs-lookup"><span data-stu-id="b321a-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="b321a-316">**False** = geeft aan dat deze zelfstandig uitpakken geschikt is voor gesplitste / gedistribueerde bestanden (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="b321a-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="b321a-317">Hallo USIEF programmeerbaarheid hoofdobjecten zijn **invoer** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="b321a-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="b321a-318">Hallo invoerobject is gebruikte tooenumerate invoergegevens als `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="b321a-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="b321a-319">Hallo uitvoer-object is de uitvoergegevens gebruikte tooset als gevolg van Hallo zelfstandig uitpakken activiteit.</span><span class="sxs-lookup"><span data-stu-id="b321a-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="b321a-320">Hallo invoergegevens toegankelijk is via `System.IO.Stream` en `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="b321a-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="b321a-321">Voor invoerkolommen-opsomming splitsen we eerst Hallo invoerstroom met behulp van een rijscheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="b321a-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="b321a-322">Vervolgens verder rij invoer in kolom delen gesplitst.</span><span class="sxs-lookup"><span data-stu-id="b321a-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="b321a-323">tooset uitvoergegevens, gebruiken we Hallo `output.Set` methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="b321a-324">Het is belangrijk toounderstand die aangepaste zelfstandig uitpakken Hallo levert alleen kolommen en waarden die zijn gedefinieerd met de Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b321a-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="b321a-325">Aanroep van methode instellen.</span><span class="sxs-lookup"><span data-stu-id="b321a-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="b321a-326">Hallo werkelijke zelfstandig uitpakken uitvoer wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="b321a-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="b321a-327">Dit is Hallo zelfstandig uitpakken voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b321a-327">Following is hello extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="b321a-328">In dit scenario use case Hallo zelfstandig uitpakken genereert Hallo GUID voor kolom 'guid' en zet Hallo-waarden van 'gebruiker' kolom tooupper case.</span><span class="sxs-lookup"><span data-stu-id="b321a-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="b321a-329">Aangepaste extractie kunnen gecompliceerdere resultaten opleveren door invoergegevens geparseerd en bewerkt.</span><span class="sxs-lookup"><span data-stu-id="b321a-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="b321a-330">Hieronder vindt u base U-SQL-script dat gebruikmaakt van een aangepaste zelfstandig uitpakken:</span><span class="sxs-lookup"><span data-stu-id="b321a-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="b321a-331">Gebruik van de gebruiker gedefinieerde outputters</span><span class="sxs-lookup"><span data-stu-id="b321a-331">Use user-defined outputters</span></span>
<span data-ttu-id="b321a-332">Gebruiker gedefinieerde outputter is een andere U-SQL-UDO waarmee u tooextend ingebouwde U-SQL-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="b321a-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="b321a-333">Vergelijkbare toohello zelfstandig uitpakken, er zijn verschillende ingebouwde outputters.</span><span class="sxs-lookup"><span data-stu-id="b321a-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="b321a-334">*Outputters.Text()*: schrijft gegevens toodelimited tekstbestanden van andere coderingen.</span><span class="sxs-lookup"><span data-stu-id="b321a-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="b321a-335">*Outputters.Csv()*: schrijft gegevens toocomma gescheiden waarden (CSV)-bestanden van andere coderingen.</span><span class="sxs-lookup"><span data-stu-id="b321a-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="b321a-336">*Outputters.Tsv()*: schrijft gegevens tootab gescheiden waarden (TSV)-bestanden van andere coderingen.</span><span class="sxs-lookup"><span data-stu-id="b321a-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="b321a-337">Aangepaste outputter kunt u toowrite gegevens in een aangepaste gedefinieerde indeling.</span><span class="sxs-lookup"><span data-stu-id="b321a-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="b321a-338">Dit kan handig zijn voor Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="b321a-339">Schrijven van toosemi gestructureerde of ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="b321a-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="b321a-340">Coderingen schrijven van gegevens niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b321a-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="b321a-341">Uitvoergegevens te wijzigen of toevoegen van aangepaste kenmerken.</span><span class="sxs-lookup"><span data-stu-id="b321a-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="b321a-342">toodefine door gebruiker gedefinieerde outputter, moeten we toocreate hello `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="b321a-343">Hieronder vindt u Hallo base `IOutputter` implementatie van klasse:</span><span class="sxs-lookup"><span data-stu-id="b321a-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="b321a-344">Alle invoer parameters toohello outputter, zoals kolom/rij scheidingstekens, codering, enzovoort, moeten toobe gedefinieerd in de constructor Hallo van Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="b321a-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="b321a-345">Hallo `IOutputter` interface moet ook een definitie voor bevatten `void Output` overschrijven.</span><span class="sxs-lookup"><span data-stu-id="b321a-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="b321a-346">Hallo-kenmerk `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` kan eventueel worden ingesteld voor verwerking-atomic-bestand.</span><span class="sxs-lookup"><span data-stu-id="b321a-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="b321a-347">Zie de volgende details Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b321a-347">For more information, see hello following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="b321a-348">`Output`voor elke rij invoer wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="b321a-348">`Output` is called for each input row.</span></span> <span data-ttu-id="b321a-349">Deze retourneert Hallo `IUnstructuredWriter output` rijenset.</span><span class="sxs-lookup"><span data-stu-id="b321a-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="b321a-350">Hallo Constructor klasse wordt gebruikt toopass parameters toohello gebruiker gedefinieerde outputter.</span><span class="sxs-lookup"><span data-stu-id="b321a-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="b321a-351">`Close`wordt gebruikt toooptionally toorelease dure status overschrijven of bepalen wanneer de laatste rij Hallo is geschreven.</span><span class="sxs-lookup"><span data-stu-id="b321a-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="b321a-352">**SqlUserDefinedOutputter** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een gebruiker gedefinieerde outputter.</span><span class="sxs-lookup"><span data-stu-id="b321a-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="b321a-353">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-353">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-354">SqlUserDefinedOutputter is een optionele kenmerk voor een definitie van de gebruiker gedefinieerde outputter.</span><span class="sxs-lookup"><span data-stu-id="b321a-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="b321a-355">Deze toodefine hello AtomicFileProcessing eigenschap gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b321a-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="b321a-356">BOOL AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="b321a-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="b321a-357">**de waarde True** = geeft aan dat deze outputter atomic uitvoerbestanden (JSON, XML,...) is vereist</span><span class="sxs-lookup"><span data-stu-id="b321a-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="b321a-358">**False** = geeft aan dat deze outputter geschikt is voor gesplitste / gedistribueerde bestanden (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="b321a-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="b321a-359">Hallo belangrijkste programmeerbaarheid objecten zijn **rij** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="b321a-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="b321a-360">Hallo **rij** -object is de uitvoergegevens gebruikte tooenumerate als `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="b321a-361">**Uitvoer** gebruikte tooset toohello doel uitvoergegevensbestand is.</span><span class="sxs-lookup"><span data-stu-id="b321a-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="b321a-362">Hallo uitvoergegevens toegankelijk is via Hallo `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="b321a-363">Uitvoergegevens is een rij tegelijk doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b321a-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="b321a-364">Hallo afzonderlijke waarden worden geïnventariseerd door het aanroepen van Get-methode van de interface IRow Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="b321a-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="b321a-365">Afzonderlijke kolomnamen kunnen worden bepaald door het aanroepen van `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="b321a-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="b321a-366">Deze aanpak kunt u een flexibele outputter voor elke metagegevensschema toobuild.</span><span class="sxs-lookup"><span data-stu-id="b321a-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="b321a-367">Hallo uitvoergegevens is geschreven in toofile `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="b321a-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="b321a-368">Hallo-stroom is parameterset te`output.BaseStrea` als onderdeel van `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="b321a-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="b321a-369">Houd er rekening mee dat het is belangrijk tooflush Hallo buffer toohello gegevensbestand na elke iteratie rij.</span><span class="sxs-lookup"><span data-stu-id="b321a-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="b321a-370">Bovendien Hallo `StreamWriter` object moet worden gebruikt met Hallo beschikbare kenmerk ingeschakeld (standaard) en Hallo **met** sleutelwoord:</span><span class="sxs-lookup"><span data-stu-id="b321a-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="b321a-371">Anders expliciet worden aangeroepen methode Flush() na elke iteratie.</span><span class="sxs-lookup"><span data-stu-id="b321a-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="b321a-372">We zien in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="b321a-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="b321a-373">Kopteksten en voetteksten ingesteld voor de gebruiker gedefinieerde outputter</span><span class="sxs-lookup"><span data-stu-id="b321a-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="b321a-374">een koptekst tooset gebruiken één iteratie uitvoering stroom.</span><span class="sxs-lookup"><span data-stu-id="b321a-374">tooset a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="b321a-375">Hallo-code in Hallo eerst `if (isHeaderRow)` blok wordt slechts één keer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="b321a-376">Gebruik voor voettekst Hallo Hallo verwijzing toohello exemplaar van `System.IO.Stream` object (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="b321a-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="b321a-377">Schrijf Hallo voettekst in Hallo Close() methode Hallo `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="b321a-378">(Zie Hallo voorbeeld te volgen voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="b321a-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="b321a-379">Hieronder volgt een voorbeeld van een gebruiker gedefinieerde outputter:</span><span class="sxs-lookup"><span data-stu-id="b321a-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="b321a-380">En base U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="b321a-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="b321a-381">Dit is een HTML-outputter een HTML-bestand gemaakt met gegevens in een tabel.</span><span class="sxs-lookup"><span data-stu-id="b321a-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="b321a-382">Outputter aanroepen vanuit base U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="b321a-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="b321a-383">een aangepaste outputter van Hallo base U-SQL-script toocall, Hallo nieuw exemplaar van Hallo outputter object heeft toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b321a-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="b321a-384">maken van een exemplaar van Hallo tooavoid object base script maken we een wrapper functie, zoals wordt weergegeven in het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b321a-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="b321a-385">De oorspronkelijke aanroep Hallo ziet in dit geval er Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b321a-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="b321a-386">Gebruiker gedefinieerde processors gebruiken</span><span class="sxs-lookup"><span data-stu-id="b321a-386">Use user-defined processors</span></span>
<span data-ttu-id="b321a-387">Gebruiker gedefinieerde processor- of UDP, is een type van U-SQL-UDO waarmee u tooprocess Hallo binnenkomende rijen door toe te passen programmeerbare functies.</span><span class="sxs-lookup"><span data-stu-id="b321a-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="b321a-388">UDP, kunt u toocombine kolommen, wijzigt u de waarden en nieuwe kolommen toevoegen, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b321a-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="b321a-389">In principe helpt het tooprocess een rijenset tooproduce vereiste elementen.</span><span class="sxs-lookup"><span data-stu-id="b321a-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="b321a-390">toodefine een UDP, moeten we toocreate een `IProcessor` interface Hello `SqlUserDefinedProcessor` kenmerk optioneel voor UDP is.</span><span class="sxs-lookup"><span data-stu-id="b321a-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="b321a-391">Deze interface moet een definitie van Hallo voor Hallo bevatten `IRow` interface rijenset overschrijven, zoals wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b321a-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="b321a-392">**SqlUserDefinedProcessor** geeft aan dat het Hallo-type moet worden geregistreerd als een gebruiker gedefinieerde processor.</span><span class="sxs-lookup"><span data-stu-id="b321a-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="b321a-393">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-393">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-394">Hallo SqlUserDefinedProcessor kenmerk **optionele** voor UDP-definitie.</span><span class="sxs-lookup"><span data-stu-id="b321a-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="b321a-395">Hallo belangrijkste programmeerbaarheid objecten zijn **invoer** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="b321a-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="b321a-396">Hallo invoerobject is gebruikte tooenumerate invoerkolommen en uitvoer en de uitvoergegevens tooset als gevolg van Hallo processoractiviteit.</span><span class="sxs-lookup"><span data-stu-id="b321a-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="b321a-397">Voor de opsomming invoerkolommen, gebruiken we Hallo `input.Get` methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="b321a-398">parameter voor Hallo `input.Get` methode is een kolom die wordt doorgegeven als onderdeel van Hallo `PRODUCE` component Hallo `PROCESS` instructie van base Hallo U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="b321a-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="b321a-399">We moeten toouse Hallo juiste gegevenstype hier.</span><span class="sxs-lookup"><span data-stu-id="b321a-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="b321a-400">Gebruik voor uitvoer Hallo `output.Set` methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="b321a-401">Het is belangrijk toonote die aangepaste producent alleen levert kolommen en waarden die zijn gedefinieerd door hello `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="b321a-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="b321a-402">Hallo werkelijke processor uitvoer wordt geactiveerd door het aanroepen van `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="b321a-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="b321a-403">Hier volgt een voorbeeld van een processor:</span><span class="sxs-lookup"><span data-stu-id="b321a-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="b321a-404">In dit scenario use case Hallo processor genereert een nieuwe kolom 'full_description' door een combinatie van Hallo bestaande kolommen--in dit geval 'gebruiker' in hoofdletters en 'des' genoemd.</span><span class="sxs-lookup"><span data-stu-id="b321a-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="b321a-405">Ook worden opnieuw gegenereerd door een GUID en Hallo oorspronkelijke en nieuwe GUID-waarden retourneert.</span><span class="sxs-lookup"><span data-stu-id="b321a-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="b321a-406">Als u in het vorige voorbeeld Hallo zien kunt, kunt u C#-methoden tijdens aanroepen `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="b321a-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="b321a-407">Hieronder volgt een voorbeeld van base U-SQL-script dat gebruikmaakt van een aangepaste processor:</span><span class="sxs-lookup"><span data-stu-id="b321a-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="b321a-408">Gebruik van de gebruiker gedefinieerde appliers</span><span class="sxs-lookup"><span data-stu-id="b321a-408">Use user-defined appliers</span></span>
<span data-ttu-id="b321a-409">Een gebruiker gedefinieerde applier van U-SQL kunt u tooinvoke een aangepaste C#-functie voor elke rij die wordt geretourneerd door de buitenste tabelexpressie Hallo van een query.</span><span class="sxs-lookup"><span data-stu-id="b321a-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="b321a-410">de juiste invoerwaarden Hello wordt geëvalueerd voor elke rij uit de linker invoer Hallo en Hallo rijen die worden gemaakt voor de uiteindelijke uitvoer Hallo worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="b321a-411">Hallo-lijst met kolommen die worden geproduceerd door de operator APPLY Hallo zijn Hallo combinatie van Hallo set kolommen in Hallo links en Hallo rechts invoer.</span><span class="sxs-lookup"><span data-stu-id="b321a-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="b321a-412">Als onderdeel van Hallo expressie USQL Selecteer wordt gebruiker gedefinieerde applier aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b321a-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="b321a-413">Hallo typische aanroep toohello gebruiker gedefinieerde applier lijkt erop Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b321a-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="b321a-414">Zie voor meer informatie over het gebruik van appliers in een SELECT-expressie [U-SQL Selecteer selecteren in de CROSS APPLY en OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="b321a-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="b321a-415">Hallo gebruiker gedefinieerde applier basisklassendefinitie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="b321a-416">een door de gebruiker gedefinieerde applier toodefine, moeten we toocreate hello `IApplier` interface met Hallo [`SqlUserDefinedApplier`] kenmerk, maar dit optioneel voor een gebruiker gedefinieerde applier definitie is.</span><span class="sxs-lookup"><span data-stu-id="b321a-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="b321a-417">Van toepassing is aangeroepen voor elke rij van de buitenste tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="b321a-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="b321a-418">Deze retourneert Hallo `IUpdatableRow` uitvoer van de rijenset.</span><span class="sxs-lookup"><span data-stu-id="b321a-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="b321a-419">Hallo Constructor klasse is gebruikte toopass parameters toohello gebruiker gedefinieerde applier.</span><span class="sxs-lookup"><span data-stu-id="b321a-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="b321a-420">**SqlUserDefinedApplier** geeft aan dat het Hallo-type moet worden geregistreerd als een gebruiker gedefinieerde applier.</span><span class="sxs-lookup"><span data-stu-id="b321a-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="b321a-421">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-421">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-422">**SqlUserDefinedApplier** is **optionele** voor een gebruiker gedefinieerde applier definitie.</span><span class="sxs-lookup"><span data-stu-id="b321a-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="b321a-423">Hallo belangrijkste programmeerbare objecten zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="b321a-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="b321a-424">Invoer rijensets worden doorgegeven als `IRow` invoer.</span><span class="sxs-lookup"><span data-stu-id="b321a-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="b321a-425">Hallo rijen uitvoer gegenereerd als `IUpdatableRow` uitvoer-interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="b321a-426">Afzonderlijke kolomnamen kunnen worden bepaald door de aanroepende Hallo `IRow` Schema-methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="b321a-427">tooget hello werkelijke gegevenswaarden van inkomende hello `IRow`, gebruiken we Hallo Get() methode van `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="b321a-428">Of we de schemanaam kolom hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b321a-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="b321a-429">Hallo uitvoerwaarden moeten worden ingesteld met `IUpdatableRow` uitvoer:</span><span class="sxs-lookup"><span data-stu-id="b321a-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="b321a-430">Het is belangrijk toounderstand aangepaste appliers alleen uitvoer kolommen en waarden die zijn gedefinieerd met `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="b321a-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="b321a-431">Hallo werkelijke output wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="b321a-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="b321a-432">Hallo gebruiker gedefinieerde applier parameters kunnen toohello-constructor worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b321a-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="b321a-433">Applier kunnen een variabele aantal kolommen dat toobe gedefinieerd tijdens Hallo applier aanroep in base U-SQL-Script moet worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b321a-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="b321a-434">Hier volgt Hallo gebruiker gedefinieerde applier voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b321a-434">Here is hello user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="b321a-435">Hieronder vindt u Hallo base U-SQL-script voor deze gebruiker gedefinieerde applier:</span><span class="sxs-lookup"><span data-stu-id="b321a-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="b321a-436">In dit scenario gebruik case vissersvloot applier fungeert als een door komma's gescheiden waarde parser voor Hallo auto gebruiker gedefinieerde eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="b321a-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="b321a-437">Hallo invoerbestand rijen eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b321a-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="b321a-438">Er is een typische door tabs gescheiden TSV bestand met een kolom met eigenschappen van die auto eigenschappen zoals het merk en model bevat.</span><span class="sxs-lookup"><span data-stu-id="b321a-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="b321a-439">Deze eigenschappen moet de geparseerde toohello tabelkolommen.</span><span class="sxs-lookup"><span data-stu-id="b321a-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="b321a-440">Hallo applier die opgegeven kunt u ook toogenerate een dynamische aantal eigenschappen in Hallo rijenset leiden, op basis van het Hallo-parameter die wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b321a-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="b321a-441">U kunt alle eigenschappen of een specifieke set eigenschappen alleen genereren.</span><span class="sxs-lookup"><span data-stu-id="b321a-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="b321a-442">Hallo gebruiker gedefinieerde applier kan worden aangeroepen als een nieuw exemplaar van applier object:</span><span class="sxs-lookup"><span data-stu-id="b321a-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="b321a-443">Of met Hallo aanroep van een wrapper-fabrieksmethode:</span><span class="sxs-lookup"><span data-stu-id="b321a-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="b321a-444">Gebruik van de gebruiker gedefinieerde combiners</span><span class="sxs-lookup"><span data-stu-id="b321a-444">Use user-defined combiners</span></span>
<span data-ttu-id="b321a-445">Gebruiker gedefinieerde combiner of UDC, kunt u toocombine rijen uit de linker- en rijensets, op basis van aangepaste logica.</span><span class="sxs-lookup"><span data-stu-id="b321a-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="b321a-446">Gebruiker gedefinieerde combiner wordt met COMBINEREN expressie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b321a-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="b321a-447">Een combiner wordt aangeroepen met de Hallo COMBINEREN expressie waarmee Hallo nodige informatie over beide invoer rijensets hello, groeperen kolommen, Hallo Hallo verwacht resultaat schema en aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="b321a-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="b321a-448">toocall een combiner in een base U-SQL-script, gebruiken we Hallo de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="b321a-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="b321a-449">Zie voor meer informatie [COMBINEREN expressie (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="b321a-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="b321a-450">een door de gebruiker gedefinieerde combiner toodefine, moeten we toocreate hello `ICombiner` interface met Hallo [`SqlUserDefinedCombiner`] kenmerk optioneel voor een definitie van een gebruiker gedefinieerde Combiner is.</span><span class="sxs-lookup"><span data-stu-id="b321a-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="b321a-451">Base `ICombiner` definitie van klasse:</span><span class="sxs-lookup"><span data-stu-id="b321a-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="b321a-452">Hallo aangepaste implementatie van een `ICombiner` interface moet bevatten Hallo definitie voor een `IEnumerable<IRow>` onderdrukking combineren.</span><span class="sxs-lookup"><span data-stu-id="b321a-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="b321a-453">Hallo **SqlUserDefinedCombiner** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een gebruiker gedefinieerde combiner.</span><span class="sxs-lookup"><span data-stu-id="b321a-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="b321a-454">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-454">This class cannot be inherited.</span></span>

<span data-ttu-id="b321a-455">**SqlUserDefinedCombiner** is gebruikte toodefine hello Combiner modus eigenschap.</span><span class="sxs-lookup"><span data-stu-id="b321a-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="b321a-456">Het is een optioneel kenmerk voor een definitie van de gebruiker gedefinieerde combiner.</span><span class="sxs-lookup"><span data-stu-id="b321a-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="b321a-457">CombinerMode modus</span><span class="sxs-lookup"><span data-stu-id="b321a-457">CombinerMode     Mode</span></span>

<span data-ttu-id="b321a-458">CombinerMode enum kan duren voordat Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="b321a-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="b321a-459">Volledig (0) alle Hallo invoer rijen uit elke rij van de uitvoer mogelijk afhankelijk linker- en Hallo met dezelfde sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="b321a-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="b321a-460">Links (1), elke rij van de uitvoer is afhankelijk van één rij invoer van Hallo links (en mogelijk alle rijen uit Hallo Hallo met dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="b321a-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="b321a-461">Rechts (2), elke rij van de uitvoer is afhankelijk van één rij invoer van de juiste hello (en mogelijk alle rijen uit Hallo links Hello dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="b321a-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="b321a-462">Interne (3), elke rij van de uitvoer is afhankelijk van een invoer van één rij uit de linker- en rechterzijde Hello dezelfde waarde.</span><span class="sxs-lookup"><span data-stu-id="b321a-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="b321a-463">Voorbeeld: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="b321a-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="b321a-464">Hallo belangrijkste programmeerbare objecten zijn:</span><span class="sxs-lookup"><span data-stu-id="b321a-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="b321a-465">Invoer rijensets worden doorgegeven als **links** en **rechts** `IRowset` type interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="b321a-466">Beide rijensets moet worden geïnventariseerd voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="b321a-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="b321a-467">U kunt elke interface slechts een keer opsommen zodat we tooenumerate hebben en deze in de cache indien nodig.</span><span class="sxs-lookup"><span data-stu-id="b321a-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="b321a-468">Voor cachedoeleinden, maken we een lijst\<T\> type geheugenstructuur als gevolg hiervan van een LINQ uitvoering van de query, specifiek lijst <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="b321a-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="b321a-469">Hallo anonieme gegevenstype kan worden gebruikt tijdens de opsomming ook.</span><span class="sxs-lookup"><span data-stu-id="b321a-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="b321a-470">Zie [inleiding tooLINQ query's (C#)](https://msdn.microsoft.com/library/bb397906.aspx) voor meer informatie over de LINQ-query's en [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) voor meer informatie over IEnumerable\<T\> interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="b321a-471">tooget hello werkelijke gegevenswaarden van inkomende hello `IRowset`, gebruiken we Hallo Get() methode van `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="b321a-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="b321a-472">Afzonderlijke kolomnamen kunnen worden bepaald door de aanroepende Hallo `IRow` Schema-methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="b321a-473">Of met behulp van de schemanaam kolom Hallo:</span><span class="sxs-lookup"><span data-stu-id="b321a-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="b321a-474">Hallo algemene opsomming met LINQ ziet er Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b321a-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="b321a-475">We gaan tooloop via alle rijen na het inventariseren van beide rijensets.</span><span class="sxs-lookup"><span data-stu-id="b321a-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="b321a-476">Voor elke rij in het linkerdeelvenster rijenset hello gaan we toofind alle rijen die voldoen aan de voorwaarde van onze combiner Hallo.</span><span class="sxs-lookup"><span data-stu-id="b321a-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="b321a-477">Hallo uitvoerwaarden moeten worden ingesteld met `IUpdatableRow` uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b321a-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="b321a-478">Hallo werkelijke output wordt geactiveerd door aan te roepen te`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="b321a-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="b321a-479">Hier volgt een voorbeeld van een combiner:</span><span class="sxs-lookup"><span data-stu-id="b321a-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="b321a-480">In dit scenario use case wordt een rapport analytics voor Hallo detailhandel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b321a-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="b321a-481">Hallo-doel is toofind alle producten die meer dan 20.000 $ en die kosten via Hallo website sneller dan via reguliere detailhandel Hallo binnen een bepaald tijdsbestek verkopen.</span><span class="sxs-lookup"><span data-stu-id="b321a-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="b321a-482">Hier volgt Hallo base U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="b321a-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="b321a-483">U kunt Hallo logica tussen een OUTER-JOIN en een combiner vergelijken:</span><span class="sxs-lookup"><span data-stu-id="b321a-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="b321a-484">Een door de gebruiker gedefinieerde combiner kan worden aangeroepen als een nieuw exemplaar van Hallo applier object:</span><span class="sxs-lookup"><span data-stu-id="b321a-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="b321a-485">Of met Hallo aanroep van een wrapper-fabrieksmethode:</span><span class="sxs-lookup"><span data-stu-id="b321a-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="b321a-486">Gebruik van de gebruiker gedefinieerde verkleiningstoestellen</span><span class="sxs-lookup"><span data-stu-id="b321a-486">Use user-defined reducers</span></span>

<span data-ttu-id="b321a-487">U-SQL kunt u toowrite aangepaste rijenset verkleiningstoestellen in C# met behulp van Hallo gebruiker gedefinieerde operator uitbreidbaarheid framework en een IReducer-interface implementeren.</span><span class="sxs-lookup"><span data-stu-id="b321a-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="b321a-488">Gebruiker gedefinieerde reducer of UDR, kan gebruikte tooeliminate onnodige rijen zijn tijdens het ophalen van gegevens (importeren).</span><span class="sxs-lookup"><span data-stu-id="b321a-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="b321a-489">Het kan ook worden gebruikt toomanipulate en evalueren rijen en kolommen.</span><span class="sxs-lookup"><span data-stu-id="b321a-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="b321a-490">Op basis van programmeerbaarheid logica, kunt deze ook bepalen welke rijen moeten toobe hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="b321a-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="b321a-491">een klasse UDR toodefine, moeten we toocreate een `IReducer` interface met een optionele `SqlUserDefinedReducer` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="b321a-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="b321a-492">Deze klasseninterface moet een definitie voor Hallo bevatten `IEnumerable` interface rijenset overschrijven.</span><span class="sxs-lookup"><span data-stu-id="b321a-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="b321a-493">Hallo **SqlUserDefinedReducer** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een gebruiker gedefinieerde reducer.</span><span class="sxs-lookup"><span data-stu-id="b321a-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="b321a-494">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="b321a-494">This class cannot be inherited.</span></span>
<span data-ttu-id="b321a-495">**SqlUserDefinedReducer** is een optioneel kenmerk voor een definitie van de gebruiker gedefinieerde reducer.</span><span class="sxs-lookup"><span data-stu-id="b321a-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="b321a-496">Deze toodefine IsRecursive eigenschap gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b321a-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="b321a-497">BOOL IsRecursive</span><span class="sxs-lookup"><span data-stu-id="b321a-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="b321a-498">**de waarde True** = geeft aan of deze Reducer idempotent</span><span class="sxs-lookup"><span data-stu-id="b321a-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="b321a-499">Hallo belangrijkste programmeerbaarheid objecten zijn **invoer** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="b321a-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="b321a-500">Hallo invoerobject is gebruikte tooenumerate invoer rijen.</span><span class="sxs-lookup"><span data-stu-id="b321a-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="b321a-501">Uitvoer is gebruikte tooset uitvoer rijen als gevolg van de activiteit te verminderen.</span><span class="sxs-lookup"><span data-stu-id="b321a-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="b321a-502">Voor invoer rijen opsomming, gebruiken we Hallo `Row.Get` methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="b321a-503">de parameter voor Hallo Hallo `Row.Get` methode is een kolom die wordt doorgegeven als onderdeel van Hallo `PRODUCE` klasse Hallo `REDUCE` instructie van base Hallo U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="b321a-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="b321a-504">We moeten toouse Hallo juiste gegevenstype hier ook.</span><span class="sxs-lookup"><span data-stu-id="b321a-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="b321a-505">Gebruik voor uitvoer Hallo `output.Set` methode.</span><span class="sxs-lookup"><span data-stu-id="b321a-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="b321a-506">Het is belangrijk toounderstand die aangepaste reducer alleen uitvoer de waarden die zijn gedefinieerd met Hallo `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="b321a-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="b321a-507">Hallo werkelijke reducer uitvoer wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="b321a-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="b321a-508">Hier volgt een voorbeeld van een reducer:</span><span class="sxs-lookup"><span data-stu-id="b321a-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="b321a-509">In dit scenario use case Hallo reducer is rijen met een lege gebruikersnaam wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b321a-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="b321a-510">Voor elke rij in de rijenset elke vereiste kolom leest, vervolgens Hallo-lengte van de gebruikersnaam Hallo evalueert.</span><span class="sxs-lookup"><span data-stu-id="b321a-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="b321a-511">Het levert werkelijke rij Hallo alleen als de lengte van de gebruiker de naam van waarde is hoger dan 0.</span><span class="sxs-lookup"><span data-stu-id="b321a-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="b321a-512">Hieronder vindt u base U-SQL-script dat gebruikmaakt van een aangepaste reducer:</span><span class="sxs-lookup"><span data-stu-id="b321a-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
