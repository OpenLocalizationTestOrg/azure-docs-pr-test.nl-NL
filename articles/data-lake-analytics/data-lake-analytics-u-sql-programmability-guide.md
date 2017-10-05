---
title: U-SQL programmeerbaarheid handleiding voor Azure Data Lake | Microsoft Docs
description: Meer informatie over de set van services in Azure Data Lake waarmee u een platform voor big data cloud-gebaseerde maken.
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
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="3d0f0-103">Handleiding voor het programmeren van U-SQL</span><span class="sxs-lookup"><span data-stu-id="3d0f0-103">U-SQL programmability guide</span></span>

<span data-ttu-id="3d0f0-104">U-SQL is een querytaal die ontworpen voor big data-type van werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="3d0f0-105">Een van de unieke kenmerken van U-SQL is de combinatie van de SQL-achtige declaratieve taal met de uitbreiden en programmeren die wordt geleverd door C#.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="3d0f0-106">In deze handleiding richten we op de uitbreiden en het programmeren van de U-SQL-taal die wordt ingeschakeld met C#.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="3d0f0-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3d0f0-107">Requirements</span></span>

<span data-ttu-id="3d0f0-108">Download en installeer [Azure Data Lake Tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="3d0f0-109">Aan de slag met U-SQL</span><span class="sxs-lookup"><span data-stu-id="3d0f0-109">Get started with U-SQL</span></span>  

<span data-ttu-id="3d0f0-110">Bekijk het volgende U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-110">Let’s look at the following U-SQL script:</span></span>

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

<span data-ttu-id="3d0f0-111">Hiermee definieert u een rijenset aangeroepen @a en maakt een rijenset aangeroepen @results van @a.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="3d0f0-112">C#-typen en expressies in de U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="3d0f0-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="3d0f0-113">Een U-SQL-expressie is een expressie C# in combinatie met logische U-SQL-bewerkingen zoals `AND`, `OR`, en `NOT`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="3d0f0-114">U-SQL-expressies kunnen worden gebruikt met SELECT-, uitpakken, waarin, ONDERVINDT, GROEPEREN en DECLAREREN.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="3d0f0-115">Het volgende script parseert bijvoorbeeld een tekenreeks in de component SELECT een DateTime-waarde.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="3d0f0-116">Het volgende script parseert een tekenreeks die een datum-/ tijdwaarde in de instructie DECLARE.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="3d0f0-117">C#-expressies gebruiken voor de conversie van het gegevenstype</span><span class="sxs-lookup"><span data-stu-id="3d0f0-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="3d0f0-118">Het volgende voorbeeld laat zien hoe u een conversie van datum-/ kunt doen met behulp van C#-expressies.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="3d0f0-119">In dit specifieke scenario wordt tekenreeksgegevens datum/tijd geconverteerd naar standard datetime-waarde met de notatie van de tijd 00:00:00 middernacht.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="3d0f0-120">C#-expressies gebruiken voor de datum van vandaag</span><span class="sxs-lookup"><span data-stu-id="3d0f0-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="3d0f0-121">De datum van vandaag ophalen, kunnen we de volgende C#-expressie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="3d0f0-122">Hier volgt een voorbeeld van het gebruik van deze expressie in een script:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-122">Here's an example of how to use this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="3d0f0-123">Met behulp van .NET-assembly 's</span><span class="sxs-lookup"><span data-stu-id="3d0f0-123">Using .NET assemblies</span></span>
<span data-ttu-id="3d0f0-124">U-SQL-uitbreidbaarheidsmodel is sterk afhankelijk van de mogelijkheid tot het toevoegen van aangepaste code.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="3d0f0-125">Op dit moment kunt biedt U-SQL u eenvoudige manieren waarop u uw eigen Microsoft toevoegen. De code op basis van NET (met name, C#).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="3d0f0-126">U kunt echter ook aangepaste code die geschreven in .NET-talen, zoals of traditiegetrouw F # toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="3d0f0-127">Registreren van een .NET-assembly</span><span class="sxs-lookup"><span data-stu-id="3d0f0-127">Register a .NET assembly</span></span>

<span data-ttu-id="3d0f0-128">De instructie CREATE ASSEMBLY gebruiken om een .NET-assembly in een U-SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="3d0f0-129">Zodra een assembly is opgenomen in een database, kunnen U-SQL-scripts die assembly's gebruiken met behulp van de referentie-ASSEMBLY-instructie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="3d0f0-130">De volgende code toont het registreren van een assembly:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="3d0f0-131">De volgende code laat zien hoe om te verwijzen naar een assembly:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="3d0f0-132">Raadpleeg de [assembly registration instructies](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) die worden in dit onderwerp in meer detail behandeld.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="3d0f0-133">Assembly-versiebeheer gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d0f0-133">Use assembly versioning</span></span>
<span data-ttu-id="3d0f0-134">Op dit moment kunt U-SQL maakt gebruik van de .NET Framework versie 4.5.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="3d0f0-135">Dus zorg ervoor dat uw eigen assembly's compatibel met deze versie van de runtime zijn.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="3d0f0-136">Zoals eerder gezegd code van de U-SQL wordt uitgevoerd in een 64-bits (x 64)-indeling.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="3d0f0-137">Zorg er dus dat uw code wordt gecompileerd voor uitvoeren onder x64.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="3d0f0-138">Anders krijgt u de eerder vermelde onjuiste indeling-fout.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="3d0f0-139">Elke assembly DLL-bestand geüpload en resource-bestand, zoals een andere runtime, een systeemeigen assembly of een configuratiebestand mag maximaal 400 MB.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="3d0f0-140">De totale grootte van de geïmplementeerde resources, hetzij via RESOURCE implementeren of verwijzingen naar assembly's en de aanvullende bestanden kan niet groter zijn dan 3 GB.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="3d0f0-141">Ten slotte Opmerking elke U-SQL-database mogen slechts één versie van de opgegeven assembly's.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="3d0f0-142">Als u zowel versie 7 en 8-versie van de bibliotheek NewtonSoft Json.Net moet, moet u bijvoorbeeld deze registreren in twee verschillende databases.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="3d0f0-143">Elk script kan bovendien alleen verwijzen naar één versie van een bepaalde assembly DLL-bestand.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="3d0f0-144">In dit opzicht volgt U-SQL de C#-assembly beheer- en versiebeheer semantiek.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="3d0f0-145">Gebruik van de gebruiker gedefinieerde functies: UDF</span><span class="sxs-lookup"><span data-stu-id="3d0f0-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="3d0f0-146">U-SQL-gebruiker gedefinieerde functies of UDF, programmeert routines die parameters accepteren, het uitvoeren van een actie (zoals een complexe berekening) en het resultaat van deze actie als wanneer u een waarde retourneren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="3d0f0-147">De retourwaarde van UDF kan alleen worden voor één scalair.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="3d0f0-148">U-SQL-UDF kan worden aangeroepen in base U-SQL-script zoals elke andere C# scalaire functie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="3d0f0-149">Het is raadzaam dat u de gebruiker gedefinieerde U-SQL-functies als initialiseren **openbare** en **statische**.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="3d0f0-150">Eerste bekijken we het eenvoudig voorbeeld van het maken van een UDF.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="3d0f0-151">In dit scenario use case moet om te bepalen van de fiscale periode, met inbegrip van het kwartaal en boekmaand van de eerste aanmelding voor de specifieke gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="3d0f0-152">De eerste boekmaand van het jaar in ons scenario is juni.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="3d0f0-153">Voor het berekenen van fiscale periode, stellen we de volgende C#-functie:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-153">To calculate fiscal period, we introduce the following C# function:</span></span>

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

<span data-ttu-id="3d0f0-154">Gewoon boekmaand en kwartaal berekend en retourneert een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="3d0f0-155">Voor juni, de eerste maand van de eerste Boekkwartaal we gebruiken 'Q1:P1'.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="3d0f0-156">Voor juli moeten we gebruiken 'Q1:P2', enzovoort.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="3d0f0-157">Dit is een reguliere C# functie die we gaan gebruiken in onze project U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="3d0f0-158">Dit is de weergave van de code-behind-sectie in dit scenario:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-158">Here is how the code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="3d0f0-159">Nu gaan we deze functie uit de base U-SQL-script aanroept.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="3d0f0-160">We hebben om dit te doen, Geef een volledig gekwalificeerde naam voor de functie, inclusief de naamruimte die in dit geval NameSpace.Class.Function(parameter) is.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="3d0f0-161">Hieronder vindt u de werkelijke base U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-161">Following is the actual U-SQL base script:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="3d0f0-162">Hieronder vindt u het bestand voor uitvoer van de uitvoering van het script:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="3d0f0-163">Dit voorbeeld wordt een eenvoudig gebruik van inline UDF in U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="3d0f0-164">Status tussen UDF aanroepen houden</span><span class="sxs-lookup"><span data-stu-id="3d0f0-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="3d0f0-165">U-SQL C# programmeerbare objecten kunnen worden meer geavanceerde, met behulp van interactiviteit via het code-behind globale variabelen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="3d0f0-166">Bekijk het volgende use case bedrijfsscenario.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="3d0f0-167">In grote organisaties kunnen gebruikers schakelen tussen varianten van interne toepassingen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="3d0f0-168">Voorbeelden Microsoft Dynamics CRM en Power BI.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="3d0f0-169">Klanten mogelijk wilt toepassen van een analyse telemetrie van hoe gebruikers tussen verschillende toepassingen schakelen, wat de trends in gebruik zijn, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="3d0f0-170">Het doel voor het bedrijf is het gebruik van de toepassing te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="3d0f0-171">Ze ook wilt combineren verschillende toepassingen of specifieke routines voor eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="3d0f0-172">We hebben om dit doel te bereiken, om te bepalen van de sessie-id's en vertragingstijd tussen de laatste sessie die is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="3d0f0-173">Er moet een vorige aanmelden zoeken en vervolgens deze aanmeldingspagina aan alle sessies die worden gegenereerd voor dezelfde toepassing toewijzen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="3d0f0-174">De eerste uitdaging is dat base U-SQL-script niet kan we berekeningen toepassen op kolommen met de functie LAG al berekend.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="3d0f0-175">De tweede uitdaging is dat we hebben zodat de specifieke sessie voor alle sessies binnen dezelfde periode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="3d0f0-176">U lost dit probleem, gebruiken we een globale variabele in een code-behind-sectie: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="3d0f0-177">Globale variabele wordt toegepast op de hele rijenset tijdens de uitvoering van het script.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="3d0f0-178">Hier volgt de code-behind-sectie van ons U-SQL-programma:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-178">Here is the code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="3d0f0-179">Dit voorbeeld ziet u de globale variabele `static public string globalSession;` gebruikt in de `getStampUserSession` functie en het ophalen van opnieuw initialiseren telkens wanneer de sessie-parameter is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="3d0f0-180">Het basistype U-SQL-script is als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-180">The U-SQL base script is as follows:</span></span>

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
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="3d0f0-181">De functie `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` hier tijdens de tweede geheugen rijenset berekening wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="3d0f0-182">Dit wordt doorgegeven de `UserSessionTimestamp` kolom en retourneert de waarde pas `UserSessionTimestamp` is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="3d0f0-183">Het uitvoerbestand is als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-183">The output file is as follows:</span></span>

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

<span data-ttu-id="3d0f0-184">In dit voorbeeld demonstreert een gecompliceerdere use case-scenario waarin we een globale variabele gebruiken in een code-behind sectie dat wordt toegepast op de hele geheugen-rijenset.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="3d0f0-185">Gebruik van de gebruiker gedefinieerde typen: UDT</span><span class="sxs-lookup"><span data-stu-id="3d0f0-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="3d0f0-186">Gebruiker gedefinieerde typen of UDT, is een andere programmeerbaarheidsfunctie van U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="3d0f0-187">U-SQL-UDT fungeert als een reguliere C# gebruiker gedefinieerd type.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="3d0f0-188">C# is een sterk getypeerde taal waarmee het gebruik van de ingebouwde en aangepaste gebruiker gedefinieerde typen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="3d0f0-189">U-SQL kan niet impliciet serialiseren of deserialiseren willekeurige UDT's wanneer de UDT wordt doorgegeven tussen hoekpunten in rijensets.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="3d0f0-190">Dit betekent dat de gebruiker te bieden een expliciete formatter met behulp van de interface IFormatter.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="3d0f0-191">Dit biedt U-SQL met het serialiseren en deserialiseren methoden voor het UDT.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="3d0f0-192">Serialiseren U-SQL ingebouwde extractie- en outputters momenteel kan niet of deserialiseren UDT gegevens naar of van bestanden met de set IFormatter zelfs.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="3d0f0-193">Wanneer u UDT-gegevens schrijven naar een bestand met de uitvoer-instructie of lezen met een zelfstandig uitpakken, hebt u dus doorgegeven als een tekenreeks of bytematrix.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="3d0f0-194">Vervolgens aanroepen van de serialisatie en deserialisatie code (dat wil zeggen, de UDT ToString() methode) expliciet.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="3d0f0-195">Gebruiker gedefinieerde extractie- en outputters, aan de andere kant kunnen lezen en schrijven UDT's.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="3d0f0-196">Als we UDT in zelfstandig uitpakken of OUTPUTTER (buiten het vorige selecteren) gebruiken als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="3d0f0-197">We hebben de volgende fout ontvangen:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="3d0f0-198">Om te werken met UDT in outputter, hebben we voor het serialiseren van het tekenreeks met de methode ToString() of maak een aangepaste outputter.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="3d0f0-199">UDT's worden momenteel niet gebruikt in de GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="3d0f0-200">Als UDT wordt gebruikt in de GROUP BY, wordt de volgende fout geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="3d0f0-201">Als u wilt definiëren een UDT, hebben we naar:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="3d0f0-202">Voeg de volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="3d0f0-203">Voeg `Microsoft.Analytics.Interfaces`, die is vereist voor de UDT-interfaces.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="3d0f0-204">Bovendien `System.IO` kunnen nodig zijn voor het definiëren van de interface IFormatter.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="3d0f0-205">Een type gebruikt gedefinieerd met het kenmerk SqlUserDefinedType definiëren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="3d0f0-206">**SqlUserDefinedType** wordt gebruikt voor de definitie van een type in een assembly als een door de gebruiker gedefinieerd type (UDT) in de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="3d0f0-207">De eigenschappen van het kenmerk weerspiegelen de fysieke kenmerken van de UDT.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="3d0f0-208">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-208">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-209">SqlUserDefinedType is een vereist kenmerk voor UDT-definitie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="3d0f0-210">De constructor van de klasse:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-210">The constructor of the class:</span></span>  

* <span data-ttu-id="3d0f0-211">SqlUserDefinedTypeAttribute (type-indeling)</span><span class="sxs-lookup"><span data-stu-id="3d0f0-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="3d0f0-212">Typ de formatter: vereiste parameter voor het definiëren van een formatter UDT--in het bijzonder het type van de `IFormatter` interface hier moet worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="3d0f0-213">Typische UDT vereist ook definitie van de interface IFormatter, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="3d0f0-214">De `IFormatter` interface serialiseert en ongedaan serialiseert een objectgrafiek met het type van de hoofdmap van \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="3d0f0-215">\<typeparam name = "T" > het type voor de objectgrafiek voor het serialiseren en deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="3d0f0-216">**Deserialiseren**: de gegevens op de opgegeven stroom ongedaan serialiseert en reconstitutes van de grafiek van objecten.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="3d0f0-217">**Serialiseren**: serialiseert een object of de grafiek van objecten met de opgegeven hoofdmap naar de opgegeven stroom.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="3d0f0-218">`MyType`exemplaar: exemplaar van het type.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="3d0f0-219">`IColumnWriter`schrijver / `IColumnReader` lezer: de onderliggende stroom van de kolom.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="3d0f0-220">`ISerializationContext`context: Enum die definieert een aantal vlaggen waarmee de context van de bron of bestemming voor de stroom tijdens serialisatie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="3d0f0-221">**Tussenliggende**: Hiermee geeft u de bron- of doelserver context is niet een persistente archief.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="3d0f0-222">**Persistentie**: geeft aan dat de bron- of doelserver context een persistente archief is.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="3d0f0-223">Als een reguliere C#-type, een U-SQL-UDT-definitie kunt opnemen overschrijvingen voor operators zoals +/ == /! =.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="3d0f0-224">Het kan ook betekenen dat statische methoden.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-224">It can also include static methods.</span></span> <span data-ttu-id="3d0f0-225">Bijvoorbeeld, als we gaan deze UDT gebruiken als een parameter voor een statistische functie MIN U-SQL, we hebben voor het definiëren van < operator overschrijven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="3d0f0-226">Eerder in deze handleiding wordt gedemonstreerd een voorbeeld van de fiscale identificatie vanaf de opgegeven datum in de notatie Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="3d0f0-227">Het volgende voorbeeld laat zien hoe een aangepast type voor fiscale periode waarden te definiëren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="3d0f0-228">Hieronder volgt een voorbeeld van een code-behind sectie met aangepaste UDT en IFormatter-interface:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="3d0f0-229">Het gedefinieerde type bevat twee getallen: kwartaal en maand.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="3d0f0-230">Operators == /! = / > / < en statische methode ToString() Hier worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="3d0f0-231">Zoals eerder gezegd, UDT kan worden gebruikt in expressies voor SELECT, maar kan niet worden gebruikt in OUTPUTTER/zelfstandig uitpakken zonder aangepaste serialisatie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="3d0f0-232">Deze moet worden geserialiseerd als tekenreeks met ToString() of gebruikt met een aangepaste OUTPUTTER/zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="3d0f0-233">Nu gaan we gebruik van UDT bespreken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="3d0f0-234">In een sectie code-behind we onze GetFiscalPeriod functie gewijzigd in het volgende:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

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

<span data-ttu-id="3d0f0-235">Zoals u ziet, wordt de waarde van onze FiscalPeriod type geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="3d0f0-236">Hier bieden we een voorbeeld van hoe u verder in base U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="3d0f0-237">In dit voorbeeld laat zien dat verschillende vormen van UDT-aanroep van U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="3d0f0-238">Hier volgt een voorbeeld van een volledige code-behind-sectie:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="3d0f0-239">Gebruik van de gebruiker gedefinieerde aggregaties: UDAGG</span><span class="sxs-lookup"><span data-stu-id="3d0f0-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="3d0f0-240">Gebruiker gedefinieerde aggregaties zijn niet out-of-the-box met U-SQL is geen aggregatie-gerelateerde functies die zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="3d0f0-241">In het voorbeeld is een statistische functie uitvoeren van aangepaste math berekeningen, samenvoegingen van tekenreeksen, bewerkingen met tekenreeksen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="3d0f0-242">De definitie van de gebruiker gedefinieerde cumulatieve basisklasse is als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-242">The user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="3d0f0-243">**SqlUserDefinedAggregate** geeft aan dat het type moet worden geregistreerd als een gebruiker gedefinieerde aggregatie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="3d0f0-244">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-244">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-245">SqlUserDefinedType kenmerk **optionele** voor UDAGG definitie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="3d0f0-246">De basisklasse kunt u drie abstracte parameters doorgeven: twee als invoerparameters en één als resultaat.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="3d0f0-247">De gegevenstypen zijn variabel en tijdens klassenovername moeten worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-247">The data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="3d0f0-248">**Init** roept eenmaal voor elke groep tijdens berekening.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="3d0f0-249">Het biedt een initialisatieroutine voor elke groep aggregatie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="3d0f0-250">**Verzamelt** één keer uitgevoerd voor elke waarde.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="3d0f0-251">De belangrijkste functionaliteit biedt voor de aggregatie-algoritme.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="3d0f0-252">Het kan worden gebruikt voor statistische waarden met verschillende gegevenstypen die zijn gedefinieerd tijdens klassenovername.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="3d0f0-253">Deze kan twee parameters van de variabele gegevenstypen accepteren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="3d0f0-254">**Beëindigen** eenmaal per aggregatie groep aan het einde van de verwerking van de resultaten voor elke groep wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="3d0f0-255">Om te declareren juist invoer en uitvoer gegevenstypen, gebruikt u de klassendefinitie als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="3d0f0-256">T1: De eerste parameter verzamelen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="3d0f0-257">T2: De eerste parameter verzamelen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="3d0f0-258">TResult: Retourtype van beëindigen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="3d0f0-259">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="3d0f0-260">of</span><span class="sxs-lookup"><span data-stu-id="3d0f0-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="3d0f0-261">Gebruik UDAGG in U-SQL</span><span class="sxs-lookup"><span data-stu-id="3d0f0-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="3d0f0-262">Voor het gebruik van UDAGG eerst Definieer dit in code-behind of verwijzing van de bestaande programmeerbaarheid dll-bestand, zoals eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="3d0f0-263">Gebruik vervolgens de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="3d0f0-264">Hier volgt een voorbeeld van UDAGG:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="3d0f0-265">En U-SQL-script gebaseerd:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="3d0f0-266">In dit scenario use case samenvoegen we klasse GUID's voor specifieke gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="3d0f0-267">Gebruik van de gebruiker gedefinieerde objecten: UDO</span><span class="sxs-lookup"><span data-stu-id="3d0f0-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="3d0f0-268">U-SQL kunt u voor het definiëren van aangepaste programmeerbaarheid-objecten, die de gebruiker gedefinieerde objecten of UDO worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="3d0f0-269">Hier volgt een lijst met UDO in U-SQL:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="3d0f0-270">Gebruiker gedefinieerde extractie</span><span class="sxs-lookup"><span data-stu-id="3d0f0-270">User-defined extractors</span></span>
    * <span data-ttu-id="3d0f0-271">Uitpakken per rij</span><span class="sxs-lookup"><span data-stu-id="3d0f0-271">Extract row by row</span></span>
    * <span data-ttu-id="3d0f0-272">Gebruikt voor het ophalen van gegevens van aangepaste structured-bestanden implementeren</span><span class="sxs-lookup"><span data-stu-id="3d0f0-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="3d0f0-273">Gebruiker gedefinieerde outputters</span><span class="sxs-lookup"><span data-stu-id="3d0f0-273">User-defined outputters</span></span>
    * <span data-ttu-id="3d0f0-274">Uitvoer per rij</span><span class="sxs-lookup"><span data-stu-id="3d0f0-274">Output row by row</span></span>
    * <span data-ttu-id="3d0f0-275">Gebruikt voor het aangepaste gegevenstypen van uitvoer of aangepaste bestand indelingen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="3d0f0-276">Gebruiker gedefinieerde processors</span><span class="sxs-lookup"><span data-stu-id="3d0f0-276">User-defined processors</span></span>
    * <span data-ttu-id="3d0f0-277">Één rij en produceert één rij</span><span class="sxs-lookup"><span data-stu-id="3d0f0-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="3d0f0-278">Verminder het aantal kolommen of produceren van nieuwe kolommen met waarden die zijn afgeleid van een bestaande set kolommen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="3d0f0-279">Gebruiker gedefinieerde appliers</span><span class="sxs-lookup"><span data-stu-id="3d0f0-279">User-defined appliers</span></span>
    * <span data-ttu-id="3d0f0-280">Één rij en produceert van 0 tot en met n rijen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="3d0f0-281">Gebruikt met buitenste/CROSS toepassen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="3d0f0-282">Gebruiker gedefinieerde combiners</span><span class="sxs-lookup"><span data-stu-id="3d0f0-282">User-defined combiners</span></span>
    * <span data-ttu-id="3d0f0-283">Combineert rijensets--gebruiker gedefinieerde JOINs</span><span class="sxs-lookup"><span data-stu-id="3d0f0-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="3d0f0-284">Gebruiker gedefinieerde verkleiningstoestellen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-284">User-defined reducers</span></span>
    * <span data-ttu-id="3d0f0-285">N rijen en produceert één rij</span><span class="sxs-lookup"><span data-stu-id="3d0f0-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="3d0f0-286">Verminder het aantal rijen waarmee</span><span class="sxs-lookup"><span data-stu-id="3d0f0-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="3d0f0-287">UDO wordt normaal gesproken expliciet aangeroepen in de U-SQL-script als onderdeel van de volgende U-SQL-instructies:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="3d0f0-288">UITPAKKEN</span><span class="sxs-lookup"><span data-stu-id="3d0f0-288">EXTRACT</span></span>
* <span data-ttu-id="3d0f0-289">UITVOER</span><span class="sxs-lookup"><span data-stu-id="3d0f0-289">OUTPUT</span></span>
* <span data-ttu-id="3d0f0-290">PROCES</span><span class="sxs-lookup"><span data-stu-id="3d0f0-290">PROCESS</span></span>
* <span data-ttu-id="3d0f0-291">COMBINEREN</span><span class="sxs-lookup"><span data-stu-id="3d0f0-291">COMBINE</span></span>
* <span data-ttu-id="3d0f0-292">VERMINDEREN</span><span class="sxs-lookup"><span data-stu-id="3d0f0-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="3d0f0-293">De UDO zijn beperkt 0,5 Gb geheugen in beslag neemt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="3d0f0-294">Deze beperking geheugen geldt niet voor lokale uitvoeringen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="3d0f0-295">Gebruik van de gebruiker gedefinieerde extractie</span><span class="sxs-lookup"><span data-stu-id="3d0f0-295">Use user-defined extractors</span></span>
<span data-ttu-id="3d0f0-296">U-SQL kunt u externe gegevens te importeren met behulp van een instructie uitpakken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="3d0f0-297">Een instructie EXTRACT kunt ingebouwde UDO extractie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="3d0f0-298">*Extractors.Text()*: extractie van tekstbestanden met scheidingstekens van andere coderingen biedt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="3d0f0-299">*Extractors.Csv()*: uitpakken van het bestand met door komma's gescheiden waarden (CSV)-bestanden van andere coderingen biedt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="3d0f0-300">*Extractors.Tsv()*: extractie van tabblad gescheiden waarden (TSV)-bestanden van andere coderingen biedt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="3d0f0-301">Kan het handig zijn voor het ontwikkelen van een aangepaste zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="3d0f0-302">Dit kan nuttig zijn bij het importeren van gegevens als we wilt uitvoeren op een van de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="3d0f0-303">Invoer gegevens wijzigen door het splitsen van kolommen en afzonderlijke waarden te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="3d0f0-304">De PROCESSOR-functionaliteit is beter voor het combineren van kolommen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="3d0f0-305">Niet-gestructureerde gegevens zoals webpagina's en e-mailberichten of niet semi-gestructureerde gegevens, zoals XML/JSON parseren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="3d0f0-306">Parseren van gegevens in niet-ondersteunde codering.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="3d0f0-307">Als u wilt een gebruiker gedefinieerde zelfstandig uitpakken of USIEF definiëren, moeten we maken een `IExtractor` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="3d0f0-308">Alle parameters voor het zelfstandig uitpakken, zoals scheidingstekens voor kolom/rij invoer- en -codering moet worden gedefinieerd in de constructor van de klasse.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="3d0f0-309">De `IExtractor` interface moet ook een definitie voor bevatten de `IEnumerable<IRow>` overschrijven als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="3d0f0-310">De **SqlUserDefinedExtractor** kenmerk geeft aan dat het type moet worden geregistreerd als een door de gebruiker gedefinieerde zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="3d0f0-311">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-311">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-312">SqlUserDefinedExtractor is een optionele kenmerk voor de definitie van USIEF.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="3d0f0-313">Het wordt gebruikt om de eigenschap AtomicFileProcessing voor het object USIEF te definiëren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="3d0f0-314">BOOL AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="3d0f0-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="3d0f0-315">**de waarde True** = geeft aan dat deze zelfstandig uitpakken atomic invoerbestanden (JSON, XML,...) is vereist</span><span class="sxs-lookup"><span data-stu-id="3d0f0-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="3d0f0-316">**False** = geeft aan dat deze zelfstandig uitpakken geschikt is voor gesplitste / gedistribueerde bestanden (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="3d0f0-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="3d0f0-317">De belangrijkste USIEF programmeerbaarheid objecten zijn **invoer** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="3d0f0-318">Het invoerobject wordt gebruikt om te inventariseren invoergegevens als `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="3d0f0-319">De uitvoer-object wordt gebruikt om in te stellen uitvoergegevens als gevolg van de activiteit zelfstandig uitpakken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="3d0f0-320">De ingevoerde gegevens toegankelijk is via `System.IO.Stream` en `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="3d0f0-321">Voor invoerkolommen-opsomming splitsen we eerst de invoerstroom met behulp van een rijscheidingsteken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="3d0f0-322">Vervolgens verder rij invoer in kolom delen gesplitst.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="3d0f0-323">Om in te stellen uitvoergegevens, gebruiken we de `output.Set` methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="3d0f0-324">Het is belangrijk te weten dat de aangepaste zelfstandig uitpakken alleen levert kolommen en waarden die zijn gedefinieerd met de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="3d0f0-325">Aanroep van methode instellen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="3d0f0-326">De uitvoer van de werkelijke zelfstandig uitpakken wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="3d0f0-327">Dit is het zelfstandig uitpakken-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-327">Following is the extractor example:</span></span>

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
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
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
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
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

<span data-ttu-id="3d0f0-328">In dit scenario use case het zelfstandig uitpakken worden opnieuw gegenereerd door de GUID voor kolom 'guid' en 'gebruiker' kolomwaarden omgezet in hoofdletters.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="3d0f0-329">Aangepaste extractie kunnen gecompliceerdere resultaten opleveren door invoergegevens geparseerd en bewerkt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="3d0f0-330">Hieronder vindt u base U-SQL-script dat gebruikmaakt van een aangepaste zelfstandig uitpakken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="3d0f0-331">Gebruik van de gebruiker gedefinieerde outputters</span><span class="sxs-lookup"><span data-stu-id="3d0f0-331">Use user-defined outputters</span></span>
<span data-ttu-id="3d0f0-332">Gebruiker gedefinieerde outputter is een andere U-SQL-UDO waarmee u de ingebouwde U-SQL-functionaliteit uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="3d0f0-333">Net als de zelfstandig uitpakken, er zijn verschillende ingebouwde outputters.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="3d0f0-334">*Outputters.Text()*: schrijft gegevens naar tekstbestanden met scheidingstekens van andere coderingen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="3d0f0-335">*Outputters.Csv()*: schrijft gegevens naar een door komma's gescheiden waarden (CSV)-bestanden van andere coderingen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="3d0f0-336">*Outputters.Tsv()*: schrijft gegevens naar het tabblad's gescheiden waarden (TSV)-bestanden van andere coderingen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="3d0f0-337">Aangepaste outputter kunt u gegevens in een aangepaste indeling voor de gedefinieerde schrijven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="3d0f0-338">Dit kan handig zijn voor de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="3d0f0-339">Schrijven van gegevens naar semi-gestructureerde of ongestructureerde bestanden.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="3d0f0-340">Coderingen schrijven van gegevens niet worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="3d0f0-341">Uitvoergegevens te wijzigen of toevoegen van aangepaste kenmerken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="3d0f0-342">Als u wilt definiëren de gebruiker gedefinieerde outputter, moeten we maken de `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="3d0f0-343">Hieronder volgt de base `IOutputter` implementatie van klasse:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="3d0f0-344">Alle ingevoerde parameters de outputter, zoals kolom/rij scheidingstekens, codering, enzovoort, moeten worden gedefinieerd in de constructor van de klasse.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="3d0f0-345">De `IOutputter` interface moet ook een definitie voor bevatten `void Output` overschrijven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="3d0f0-346">Het kenmerk `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` kan eventueel worden ingesteld voor verwerking-atomic-bestand.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="3d0f0-347">Zie de volgende details voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-347">For more information, see the following details.</span></span>

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

* <span data-ttu-id="3d0f0-348">`Output`voor elke rij invoer wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-348">`Output` is called for each input row.</span></span> <span data-ttu-id="3d0f0-349">Deze retourneert de `IUnstructuredWriter output` rijenset.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="3d0f0-350">De Constructor-klasse wordt gebruikt voor parameters doorgeven aan de gebruiker gedefinieerde outputter.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="3d0f0-351">`Close`wordt gebruikt om eventueel negeren als u wilt vrijgeven dure status of bepalen wanneer de laatste rij is geschreven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="3d0f0-352">**SqlUserDefinedOutputter** kenmerk geeft aan dat het type moet worden geregistreerd als een gebruiker gedefinieerde outputter.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="3d0f0-353">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-353">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-354">SqlUserDefinedOutputter is een optionele kenmerk voor een definitie van de gebruiker gedefinieerde outputter.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="3d0f0-355">Wordt gebruikt om de eigenschap AtomicFileProcessing te definiëren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="3d0f0-356">BOOL AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="3d0f0-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="3d0f0-357">**de waarde True** = geeft aan dat deze outputter atomic uitvoerbestanden (JSON, XML,...) is vereist</span><span class="sxs-lookup"><span data-stu-id="3d0f0-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="3d0f0-358">**False** = geeft aan dat deze outputter geschikt is voor gesplitste / gedistribueerde bestanden (CSV, SEQ,...)</span><span class="sxs-lookup"><span data-stu-id="3d0f0-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="3d0f0-359">De belangrijkste programmeerbaarheid objecten zijn **rij** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="3d0f0-360">De **rij** object wordt gebruikt om te inventariseren uitvoergegevens als `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="3d0f0-361">**Uitvoer** uitvoergegevens instellen op de doelbestand wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="3d0f0-362">De uitvoergegevens kan worden geopend via de `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="3d0f0-363">Uitvoergegevens is een rij tegelijk doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="3d0f0-364">De afzonderlijke waarden worden geïnventariseerd door het aanroepen van de methode Get van de interface IRow:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="3d0f0-365">Afzonderlijke kolomnamen kunnen worden bepaald door het aanroepen van `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="3d0f0-366">Deze aanpak kunt u een flexibele outputter voor elke metagegevensschema bouwen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="3d0f0-367">De uitvoergegevens worden geschreven naar het bestand met behulp van `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="3d0f0-368">De parameter van de stroom is ingesteld op `output.BaseStrea` als onderdeel van `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="3d0f0-369">Houd er rekening mee dat het is belangrijk de gegevensbuffer naar het bestand leegmaken na elke iteratie rij.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="3d0f0-370">Bovendien de `StreamWriter` object moet worden gebruikt met de beschikbare kenmerk ingeschakeld (standaard) en de **met** sleutelwoord:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="3d0f0-371">Anders expliciet worden aangeroepen methode Flush() na elke iteratie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="3d0f0-372">We zien in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="3d0f0-373">Kopteksten en voetteksten ingesteld voor de gebruiker gedefinieerde outputter</span><span class="sxs-lookup"><span data-stu-id="3d0f0-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="3d0f0-374">U stelt een koptekst met één iteratie uitvoering stroom.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-374">To set a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="3d0f0-375">De code in de eerste `if (isHeaderRow)` blok wordt slechts één keer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="3d0f0-376">Gebruik de verwijzing naar het exemplaar van voor de voettekst `System.IO.Stream` object (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="3d0f0-377">Schrijven van de voettekst in de methode Close() van de `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="3d0f0-378">(Zie het volgende voorbeeld voor meer informatie.)</span><span class="sxs-lookup"><span data-stu-id="3d0f0-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="3d0f0-379">Hieronder volgt een voorbeeld van een gebruiker gedefinieerde outputter:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-379">Following is an example of a user-defined outputter:</span></span>

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

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
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
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
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
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="3d0f0-380">En base U-SQL-script:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-380">And U-SQL base script:</span></span>

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
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="3d0f0-381">Dit is een HTML-outputter een HTML-bestand gemaakt met gegevens in een tabel.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="3d0f0-382">Outputter aanroepen vanuit base U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="3d0f0-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="3d0f0-383">Als u een aangepaste outputter vanuit het basistype U-SQL-script, heeft het nieuwe exemplaar van het object outputter worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="3d0f0-384">Om te voorkomen maakt u een instantie van het object in base script, maken we een wrapper functie, zoals wordt weergegeven in het vorige voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="3d0f0-385">In dit geval wordt de oorspronkelijke aanroep ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="3d0f0-386">Gebruiker gedefinieerde processors gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d0f0-386">Use user-defined processors</span></span>
<span data-ttu-id="3d0f0-387">Gebruiker gedefinieerde processor- of UDP, is een type van U-SQL-UDO waarmee u voor het verwerken van de binnenkomende rijen door toe te passen programmeerbare functies.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="3d0f0-388">UDP kunt u kolommen combineren, waarden wijzigen en nieuwe kolommen toevoegen, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="3d0f0-389">In principe helpt het verwerken van een rijenset vereiste gegevenselementen produceren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="3d0f0-390">Als u wilt definiëren een UDP, moeten we maken een `IProcessor` contact kunnen maken met de `SqlUserDefinedProcessor` kenmerk optioneel voor UDP is.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="3d0f0-391">Deze interface mag de definitie voor de `IRow` interface rijenset overschrijven, zoals wordt weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

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

<span data-ttu-id="3d0f0-392">**SqlUserDefinedProcessor** geeft aan dat het type moet worden geregistreerd als een gebruiker gedefinieerde processor.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="3d0f0-393">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-393">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-394">Het kenmerk SqlUserDefinedProcessor **optionele** voor UDP-definitie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="3d0f0-395">De belangrijkste programmeerbaarheid objecten zijn **invoer** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="3d0f0-396">Het invoerobject wordt gebruikt om kolommen invoer en uitvoer te inventariseren en in te stellen uitvoergegevens als gevolg van de processoractiviteit.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="3d0f0-397">Invoerkolommen opsomming, gebruiken we de `input.Get` methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="3d0f0-398">De parameter voor `input.Get` methode is een kolom die wordt doorgegeven als onderdeel van de `PRODUCE` -component van de `PROCESS` instructie van het basistype U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="3d0f0-399">We moeten het juiste gegevenstype hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="3d0f0-400">Gebruik voor uitvoer, de `output.Set` methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="3d0f0-401">Het is belangrijk te weten dat aangepaste producent levert alleen kolommen en waarden die zijn gedefinieerd met de `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="3d0f0-402">De uitvoer van de werkelijke processor wordt geactiveerd door het aanroepen van `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="3d0f0-403">Hier volgt een voorbeeld van een processor:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-403">Following is a processor example:</span></span>

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

<span data-ttu-id="3d0f0-404">In dit scenario use case wordt een nieuwe kolom met de naam 'full_description' door een combinatie van de bestaande kolommen--in dit geval 'gebruiker' in hoofdletters en 'des' het genereren van de processor.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="3d0f0-405">Ook worden opnieuw gegenereerd door een GUID en de oorspronkelijke en nieuwe GUID-waarden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="3d0f0-406">Als u in het vorige voorbeeld zien kunt, kunt u C#-methoden tijdens aanroepen `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="3d0f0-407">Hieronder volgt een voorbeeld van base U-SQL-script dat gebruikmaakt van een aangepaste processor:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="3d0f0-408">Gebruik van de gebruiker gedefinieerde appliers</span><span class="sxs-lookup"><span data-stu-id="3d0f0-408">Use user-defined appliers</span></span>
<span data-ttu-id="3d0f0-409">Een gebruiker gedefinieerde applier van U-SQL kunt u een aangepaste C#-functie voor elke rij die wordt geretourneerd door de buitenste tabelexpressie van een query worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="3d0f0-410">De juiste invoerwaarden wordt geëvalueerd voor elke rij uit de linker-invoer en de rijen die worden gemaakt voor de uiteindelijke uitvoer worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="3d0f0-411">De lijst met kolommen die worden geproduceerd door de operator APPLY zijn de combinatie van de set kolommen in de linkerkant en de juiste invoerwaarden.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="3d0f0-412">Als onderdeel van de expressie USQL Selecteer wordt gebruiker gedefinieerde applier aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="3d0f0-413">De typische aanroep van de gebruiker gedefinieerde applier ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="3d0f0-414">Zie voor meer informatie over het gebruik van appliers in een SELECT-expressie [U-SQL Selecteer selecteren in de CROSS APPLY en OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="3d0f0-415">De gebruiker gedefinieerde applier base klassendefinitie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="3d0f0-416">Als u een gebruiker gedefinieerde applier definieert, moeten we maken de `IApplier` contact kunnen maken met de [`SqlUserDefinedApplier`] kenmerk, maar dit optioneel voor een gebruiker gedefinieerde applier definitie is.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="3d0f0-417">Van toepassing is aangeroepen voor elke rij van de buitenste tabel.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="3d0f0-418">Deze retourneert de `IUpdatableRow` uitvoer van de rijenset.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="3d0f0-419">De Constructor-klasse wordt gebruikt voor parameters doorgeven aan de gebruiker gedefinieerde applier.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="3d0f0-420">**SqlUserDefinedApplier** geeft aan dat het type moet worden geregistreerd als een gebruiker gedefinieerde applier.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="3d0f0-421">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-421">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-422">**SqlUserDefinedApplier** is **optionele** voor een gebruiker gedefinieerde applier definitie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="3d0f0-423">De belangrijkste programmeerbare objecten zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="3d0f0-424">Invoer rijensets worden doorgegeven als `IRow` invoer.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="3d0f0-425">De uitvoer rijen worden gegenereerd als `IUpdatableRow` uitvoer-interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="3d0f0-426">Afzonderlijke kolomnamen kunnen worden bepaald door het aanroepen van de `IRow` Schema-methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="3d0f0-427">De werkelijke waarden ophalen uit de binnenkomende `IRow`, gebruiken we de methode Get() van `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="3d0f0-428">Of we de naam van de schema-kolom gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="3d0f0-429">De uitvoerwaarden moeten worden ingesteld met `IUpdatableRow` uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="3d0f0-430">Het is belangrijk te begrijpen dat aangepaste appliers uitvoer alleen kolommen en waarden die zijn gedefinieerd met `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="3d0f0-431">De werkelijke uitvoer wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="3d0f0-432">De gebruiker gedefinieerde applier parameters kunnen worden doorgegeven aan de constructor.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="3d0f0-433">Applier kunnen een variabele aantal kolommen dat moet worden gedefinieerd tijdens het aanroepen van applier in base U-SQL-Script geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="3d0f0-434">Hier volgt de gebruiker gedefinieerde applier voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-434">Here is the user-defined applier example:</span></span>

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

<span data-ttu-id="3d0f0-435">Dit is het basistype U-SQL-script voor deze door de gebruiker gedefinieerde applier:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-435">Following is the base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="3d0f0-436">In dit scenario gebruik case fungeert gebruiker gedefinieerde applier als een door komma's gescheiden waarde parser voor de vloot auto-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="3d0f0-437">De rijen invoerbestand er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="3d0f0-438">Er is een typische door tabs gescheiden TSV bestand met een kolom met eigenschappen van die auto eigenschappen zoals het merk en model bevat.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="3d0f0-439">Deze eigenschappen moeten worden geparseerd naar kolommen in de tabel.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="3d0f0-440">De applier die opgegeven kunt u het genereren van een dynamische aantal eigenschappen in de rijenset resultaat, op basis van de parameter die wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="3d0f0-441">U kunt alle eigenschappen of een specifieke set eigenschappen alleen genereren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="3d0f0-442">De gebruiker gedefinieerde applier kan worden aangeroepen als een nieuw exemplaar van applier object:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="3d0f0-443">Of met het aanroepen van een wrapper-fabrieksmethode:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="3d0f0-444">Gebruik van de gebruiker gedefinieerde combiners</span><span class="sxs-lookup"><span data-stu-id="3d0f0-444">Use user-defined combiners</span></span>
<span data-ttu-id="3d0f0-445">Gebruiker gedefinieerde combiner of UDC, kunt u rijen uit de linker- en rijensets, op basis van aangepaste regels worden gecombineerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="3d0f0-446">Gebruiker gedefinieerde combiner wordt met COMBINEREN expressie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="3d0f0-447">Een combiner wordt aangeroepen met de expressie COMBINEREN met de benodigde informatie over zowel de invoer rijensets, de groepering kolommen, het verwachte resultaat schema en aanvullende informatie.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="3d0f0-448">Om aan te roepen een combiner in een base U-SQL-script, maar we gebruiken de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

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

<span data-ttu-id="3d0f0-449">Zie voor meer informatie [COMBINEREN expressie (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="3d0f0-450">Als u een gebruiker gedefinieerde combiner definieert, moeten we maken de `ICombiner` contact kunnen maken met de [`SqlUserDefinedCombiner`] kenmerk optioneel voor een definitie van een gebruiker gedefinieerde Combiner is.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="3d0f0-451">Base `ICombiner` definitie van klasse:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="3d0f0-452">De aangepaste implementatie van een `ICombiner` interface mag de definitie voor een `IEnumerable<IRow>` onderdrukking combineren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="3d0f0-453">De **SqlUserDefinedCombiner** kenmerk geeft aan dat het type moet worden geregistreerd als een gebruiker gedefinieerde combiner.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="3d0f0-454">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-454">This class cannot be inherited.</span></span>

<span data-ttu-id="3d0f0-455">**SqlUserDefinedCombiner** wordt gebruikt voor het definiëren van de eigenschap Combiner mode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="3d0f0-456">Het is een optioneel kenmerk voor een definitie van de gebruiker gedefinieerde combiner.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="3d0f0-457">CombinerMode modus</span><span class="sxs-lookup"><span data-stu-id="3d0f0-457">CombinerMode     Mode</span></span>

<span data-ttu-id="3d0f0-458">CombinerMode enum kan duren voordat de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="3d0f0-459">Volledig (0) elke rij van de uitvoer mogelijk afhankelijk van alle invoer rijen van links en met dezelfde sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="3d0f0-460">Left (1) de rij voor elke uitvoer, is afhankelijk van één rij invoer van links (en mogelijk alle rijen uit de rechts met dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="3d0f0-461">Recht (2) de rij voor elke uitvoer, is afhankelijk van één rij invoer van het recht (en mogelijk alle rijen uit de linkerkant met dezelfde sleutelwaarde).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="3d0f0-462">Binnenste (3) de rij voor elke uitvoer, is afhankelijk van een enkele rij invoer van links en rechts met dezelfde waarde.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="3d0f0-463">Voorbeeld: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="3d0f0-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="3d0f0-464">De belangrijkste programmeerbare objecten zijn:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="3d0f0-465">Invoer rijensets worden doorgegeven als **links** en **rechts** `IRowset` type interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="3d0f0-466">Beide rijensets moet worden geïnventariseerd voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="3d0f0-467">U kunt elke interface slechts een keer opsommen zodat we niet inventariseren en deze in de cache indien nodig.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="3d0f0-468">Voor cachedoeleinden, maken we een lijst\<T\> type geheugenstructuur als gevolg hiervan van een LINQ uitvoering van de query, specifiek lijst <`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="3d0f0-469">Het anonieme type kan worden gebruikt tijdens de opsomming ook.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="3d0f0-470">Zie [Inleiding tot LINQ-query's (C#)](https://msdn.microsoft.com/library/bb397906.aspx) voor meer informatie over de LINQ-query's en [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) voor meer informatie over IEnumerable\<T\> interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="3d0f0-471">De werkelijke waarden ophalen uit de binnenkomende `IRowset`, gebruiken we de methode Get() van `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="3d0f0-472">Afzonderlijke kolomnamen kunnen worden bepaald door het aanroepen van de `IRow` Schema-methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="3d0f0-473">Of met behulp van de naam van de schema-kolom:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="3d0f0-474">De algemene opsomming met LINQ ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="3d0f0-475">We gaan doorlopen alle rijen na het inventariseren van beide rijensets.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="3d0f0-476">We gaan zoeken naar alle rijen die voldoen aan de voorwaarde van onze combiner voor elke rij in de linker-rijenset.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="3d0f0-477">De uitvoerwaarden moeten worden ingesteld met `IUpdatableRow` uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="3d0f0-478">De werkelijke uitvoer wordt geactiveerd door aanroepen naar `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="3d0f0-479">Hier volgt een voorbeeld van een combiner:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="3d0f0-480">In dit scenario use case wordt een rapport analytics gemaakt voor de detailhandel.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="3d0f0-481">Het doel is te vinden van alle producten die meer dan 20.000 $ kosten en die via de website sneller dan via de detailhandel reguliere binnen een bepaald tijdsbestek verkopen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="3d0f0-482">Hier is het basistype U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="3d0f0-483">U kunt de logica tussen een OUTER-JOIN en een combiner vergelijken:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="3d0f0-484">Een door de gebruiker gedefinieerde combiner kan worden aangeroepen als een nieuw exemplaar van het applier object:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="3d0f0-485">Of met het aanroepen van een wrapper-fabrieksmethode:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="3d0f0-486">Gebruik van de gebruiker gedefinieerde verkleiningstoestellen</span><span class="sxs-lookup"><span data-stu-id="3d0f0-486">Use user-defined reducers</span></span>

<span data-ttu-id="3d0f0-487">U-SQL kunt u aangepaste rijenset verkleiningstoestellen in C# schrijven met behulp van de gebruiker gedefinieerde operator uitbreidbaarheid framework en een IReducer-interface implementeren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="3d0f0-488">Gebruiker gedefinieerde reducer of UDR, kan worden gebruikt om te verwijderen van onnodige rijen tijdens het ophalen van gegevens (importeren).</span><span class="sxs-lookup"><span data-stu-id="3d0f0-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="3d0f0-489">Het kan ook worden gebruikt om te bewerken en evalueren van rijen en kolommen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="3d0f0-490">Op basis van programmeerbaarheid logica, kunt het ook bepalen welke rijen moeten worden geëxtraheerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="3d0f0-491">Als u wilt een UDR klasse definieert, moeten we maken een `IReducer` interface met een optionele `SqlUserDefinedReducer` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="3d0f0-492">Deze klasseninterface moet een definitie voor bevatten de `IEnumerable` interface rijenset overschrijven.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="3d0f0-493">De **SqlUserDefinedReducer** kenmerk geeft aan dat het type moet worden geregistreerd als een gebruiker gedefinieerde reducer.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="3d0f0-494">Deze klasse kan niet worden overgenomen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-494">This class cannot be inherited.</span></span>
<span data-ttu-id="3d0f0-495">**SqlUserDefinedReducer** is een optioneel kenmerk voor een definitie van de gebruiker gedefinieerde reducer.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="3d0f0-496">Wordt gebruikt om de eigenschap IsRecursive te definiëren.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="3d0f0-497">BOOL IsRecursive</span><span class="sxs-lookup"><span data-stu-id="3d0f0-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="3d0f0-498">**de waarde True** = geeft aan of deze Reducer idempotent</span><span class="sxs-lookup"><span data-stu-id="3d0f0-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="3d0f0-499">De belangrijkste programmeerbaarheid objecten zijn **invoer** en **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="3d0f0-500">Het invoerobject wordt gebruikt voor het inventariseren van invoer rijen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="3d0f0-501">Uitvoer wordt gebruikt om in te stellen uitvoer rijen als gevolg van de activiteit te verminderen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="3d0f0-502">Invoer rijen opsomming, gebruiken we de `Row.Get` methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="3d0f0-503">De parameter voor de `Row.Get` methode is een kolom die wordt doorgegeven als onderdeel van de `PRODUCE` klasse van de `REDUCE` instructie van het basistype U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="3d0f0-504">We moeten het juiste gegevenstype ook hier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="3d0f0-505">Gebruik voor uitvoer, de `output.Set` methode.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="3d0f0-506">Het is belangrijk te begrijpen die aangepaste reducer levert alleen waarden die zijn gedefinieerd met de `output.Set` methodeaanroep.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="3d0f0-507">De uitvoer van de werkelijke reducer wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="3d0f0-508">Hier volgt een voorbeeld van een reducer:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="3d0f0-509">In dit scenario use case, is de reducer rijen met een lege gebruikersnaam overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="3d0f0-510">Voor elke rij in de rijenset elke vereiste kolom leest, vervolgens de lengte van de gebruikersnaam wordt geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="3d0f0-511">Het levert de werkelijke rij alleen als de lengte van de gebruiker de naam van waarde is hoger dan 0.</span><span class="sxs-lookup"><span data-stu-id="3d0f0-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="3d0f0-512">Hieronder vindt u base U-SQL-script dat gebruikmaakt van een aangepaste reducer:</span><span class="sxs-lookup"><span data-stu-id="3d0f0-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```
