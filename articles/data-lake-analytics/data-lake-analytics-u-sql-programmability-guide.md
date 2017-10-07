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
# <a name="u-sql-programmability-guide"></a>Handleiding voor het programmeren van U-SQL

U-SQL is een querytaal die ontworpen voor big data-type van werkbelastingen. Een van de unieke kenmerken Hallo van U-SQL is Hallo combinatie van Hallo SQL-achtige declaratieve taal met Hallo uitbreiden en programmeren die wordt geleverd door C#. In deze handleiding richten we op Hallo uitbreiden en programmeren van Hallo U-SQL-taal die wordt ingeschakeld met C#.

## <a name="requirements"></a>Vereisten

Download en installeer [Azure Data Lake Tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Aan de slag met U-SQL  

Bekijk Hallo volgende U-SQL-script:

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

Hiermee definieert u een rijenset aangeroepen @a en maakt een rijenset aangeroepen @results van @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>C#-typen en expressies in de U-SQL-script

Een U-SQL-expressie is een expressie C# in combinatie met logische U-SQL-bewerkingen zoals `AND`, `OR`, en `NOT`. U-SQL-expressies kunnen worden gebruikt met SELECT-, uitpakken, waarin, ONDERVINDT, GROEPEREN en DECLAREREN.

Bijvoorbeeld parseert Hallo na script een tekenreeks een DateTime-waarde in Hallo SELECT-component.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Hallo parseert volgende script een tekenreeks in een instructie DECLARE een DateTime-waarde.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>C#-expressies gebruiken voor de conversie van het gegevenstype
Hallo volgende voorbeeld laat zien hoe u een conversie van datum-/ kunt doen met behulp van C#-expressies. In dit scenario is datetime tekenreeksgegevens geconverteerde toostandard datetime met de notatie van de tijd 00:00:00 middernacht.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>C#-expressies gebruiken voor de datum van vandaag
toopull datum van vandaag, kunnen we gebruiken Hallo C#-expressie te volgen:

```
DateTime.Now.ToString("M/d/yyyy")
```

Hier volgt een voorbeeld van hoe toouse deze expressie in een script:

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



## <a name="using-net-assemblies"></a>Met behulp van .NET-assembly 's
U-SQL-uitbreidbaarheidsmodel is sterk afhankelijk van Hallo mogelijkheid tooadd aangepaste code. Op dit moment kunt biedt U-SQL u eenvoudige manieren tooadd uw eigen Microsoft. De code op basis van NET (met name, C#). U kunt echter ook aangepaste code die geschreven in .NET-talen, zoals of traditiegetrouw F # toevoegen. 

### <a name="register-a-net-assembly"></a>Registreren van een .NET-assembly

Hallo CREATE ASSEMBLY instructie tooplace een .NET-assembly in een U-SQL-Database gebruiken. Nadat een assembly een database is, kunnen U-SQL-scripts die assembly's gebruiken met behulp van Hallo referentie-ASSEMBLY-instructie. 

Hallo van de volgende code wordt getoond hoe tooregister een assembly:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Hallo van de volgende code wordt getoond hoe tooreference een assembly:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Raadpleeg Hallo [assembly registration instructies](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) die worden in dit onderwerp in meer detail behandeld.


### <a name="use-assembly-versioning"></a>Assembly-versiebeheer gebruiken
U-SQL gebruikt op dit moment Hallo .NET Framework versie 4.5. Dus zorg ervoor dat uw eigen assembly's compatibel met deze versie van Hallo-runtime zijn.

Zoals eerder gezegd code van de U-SQL wordt uitgevoerd in een 64-bits (x 64)-indeling. Dus zorg ervoor dat uw code gecompileerde toorun op x64. Anders krijgt u een onjuiste indelingsfout Hallo eerder weergegeven.

Elke assembly DLL-bestand geüpload en resource-bestand, zoals een andere runtime, een systeemeigen assembly of een configuratiebestand mag maximaal 400 MB. totale grootte van de Hallo van geïmplementeerde resources, hetzij via RESOURCE implementeren of een verwijzingen tooassemblies en de bijbehorende extra bestanden niet meer dan 3 GB.

Ten slotte Opmerking elke U-SQL-database mogen slechts één versie van de opgegeven assembly's. Bijvoorbeeld, als u zowel versie 7 als versie 8 Hallo NewtonSoft Json.Net-bibliotheek moet, moet u tooregister ze in twee verschillende databases. Bovendien kan elk script alleen tooone versie van een bepaalde assembly DLL verwijzen. In dit opzicht volgt U-SQL Hallo C#-assembly beheer- en versiebeheer semantiek.


## <a name="use-user-defined-functions-udf"></a>Gebruik van de gebruiker gedefinieerde functies: UDF
U-SQL-gebruiker gedefinieerde functies of UDF, programmeert routines die parameters accepteren, het uitvoeren van een actie (zoals een complexe berekening) en het Hallo resultaat van deze actie als wanneer u een waarde te retourneren. Hallo retourneren waarde van UDF kan alleen één scalair zijn. U-SQL-UDF kan worden aangeroepen in base U-SQL-script zoals elke andere C# scalaire functie.

Het is raadzaam dat u de gebruiker gedefinieerde U-SQL-functies als initialiseren **openbare** en **statische**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Eerste bekijken we Hallo eenvoudig voorbeeld van het maken van een UDF.

In dit scenario use case moet toodetermine Hallo fiscale periode, met inbegrip van Hallo Boekkwartaal en boekmaand van Hallo eerste aanmelden voor een specifieke gebruiker Hallo. Hallo is eerste boekmaand van Hallo jaar in ons scenario juni.

toocalculate fiscale periode, stellen we Hallo C#-functie te volgen:

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

Gewoon boekmaand en kwartaal berekend en retourneert een string-waarde. We gebruiken 'Q1:P1' voor juni, Hallo eerste maand van Hallo eerste kwartaal. Voor juli moeten we gebruiken 'Q1:P2', enzovoort.

Dit is een reguliere C#-functie we continu toouse zijn in de U-SQL-project.

Hier ziet u hoe Hallo code-behind sectie eruitziet in dit scenario:

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

Nu gaan we toocall deze functie van Hallo base U-SQL-script. toodo, hebben we tooprovide na een volledig gekwalificeerde naam voor de functie hello, inclusief Hallo-naamruimte die in dit geval NameSpace.Class.Function(parameter) is.

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Hieronder vindt u Hallo werkelijke U-SQL base script:

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

Dit is het uitvoerbestand Hallo Hallo uitvoeren van scripts:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Dit voorbeeld wordt een eenvoudig gebruik van inline UDF in U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Status tussen UDF aanroepen houden
U-SQL C# programmeerbare objecten kunnen worden meer geavanceerde, met behulp van interactiviteit via Hallo code-behind globale variabelen. Bekijk Hallo use case bedrijfsscenario te volgen.

In grote organisaties kunnen gebruikers schakelen tussen varianten van interne toepassingen. Voorbeelden Microsoft Dynamics CRM en Power BI. Klanten kunt tooapply een analyse telemetrie van hoe gebruikers tussen verschillende toepassingen schakelen, welke gebruik Hallo trends weet, enzovoort. Hello dient voor bedrijven Hallo toooptimize toepassingsgebruik. Ze ook verstandig toocombine verschillende toepassingen of specifieke routines voor eenmalige aanmelding.

tooachieve deze doelstelling krijgen we hebben toodetermine sessie-id's en vertragingstijd tussen Hallo laatste sessie die is opgetreden.

We moet toofind een vorige aanmelden en wijs deze aanmelden tooall-sessies die worden gegenereerd toohello dezelfde toepassing. Hallo eerste uitdaging is dat base U-SQL-script niet is toegestaan ons tooapply berekeningen via al berekende kolommen met de functie LAG. Hallo tweede uitdaging is dat we tookeep Hallo bepaalde sessie voor alle sessies binnen Hallo hebben dezelfde periode.

toosolve dit probleem, gebruiken we een globale variabele in een code-behind-sectie: `static public string globalSession;`.

Deze globale variabele is toegepaste toohello volledige rijenset tijdens de uitvoering van het script.

Hier volgt Hallo code-behind sectie van ons U-SQL-programma:

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

In dit voorbeeld toont de globale variabele Hallo `static public string globalSession;` gebruikt in Hallo `getStampUserSession` functie en het ophalen van opnieuw geïnitialiseerd elke keer Hallo sessie parameter wordt gewijzigd.

Hallo base U-SQL-script is als volgt:

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

De functie `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` hier tijdens de Hallo tweede geheugen rijenset berekening wordt aangeroepen. Dit wordt doorgegeven Hallo `UserSessionTimestamp` kolom en retourneert de waarde pas Hallo `UserSessionTimestamp` is gewijzigd.

Hallo-uitvoerbestand is als volgt:

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

In dit voorbeeld demonstreert een gecompliceerdere use case-scenario waarin we een globale variabele gebruiken in een code-behind sectie die is toegepast toohello hele geheugen rijenset.

## <a name="use-user-defined-types-udt"></a>Gebruik van de gebruiker gedefinieerde typen: UDT
Gebruiker gedefinieerde typen of UDT, is een andere programmeerbaarheidsfunctie van U-SQL. U-SQL-UDT fungeert als een reguliere C# gebruiker gedefinieerd type. C# is een sterk getypeerde taal waarmee ingebouwde en aangepaste gebruiker gedefinieerde typen hello gebruiken.

U-SQL kan niet impliciet serialiseren of deserialiseren willekeurige UDT's wanneer Hallo UDT wordt doorgegeven tussen hoekpunten in rijensets. Dit betekent dat Hallo gebruiker tooprovide een expliciete formatter met Hallo IFormatter-interface. Dit biedt U-SQL Hallo serialiseren en deserialiseren methoden voor het Hallo UDT.

> [!NOTE]
> Serialiseren U-SQL ingebouwde extractie- en outputters momenteel kan niet of deserialiseren UDT gegevens tooor zelfs Hallo IFormatter set bestanden. Wanneer u schrijft UDT gegevensbestand tooa Hello uitvoer-instructie of gelezen heeft met een zelfstandig uitpakken, hebt u toopass als een tekenreeks of een byte-matrix. Vervolgens aanroepen Hallo serialisatie en expliciet code (dat wil zeggen, de Hallo UDT ToString() methode) heeft het deserialiseren. Gebruiker gedefinieerde extractie- en outputters op Hallo andere kunnen hand, lezen en schrijven UDT's.

Als we toouse UDT in zelfstandig uitpakken of OUTPUTTER (buiten het vorige selecteren), proberen zoals hier wordt weergegeven:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

We ontvangen Hallo volgende fout:

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

toowork met UDT in outputter we hebben tooserialize het toostring met methode ToString() hello of een aangepaste outputter maken.

UDT's worden momenteel niet gebruikt in de GROUP BY. Als UDT wordt gebruikt in de GROUP BY, wordt de volgende fout Hallo gegenereerd:

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

een UDT toodefine, hebben we naar:

* Hallo naamruimten volgende toevoegen:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Voeg `Microsoft.Analytics.Interfaces`, die is vereist voor Hallo UDT-interfaces. Bovendien `System.IO` mogelijk nodig toodefine hello IFormatter interface.

* Een type gebruikt gedefinieerd met het kenmerk SqlUserDefinedType definiëren.

**SqlUserDefinedType** gebruikte toomark de definitie van een type in een assembly als een gebruiker gedefinieerde type (UDT) is in de U-SQL. Hallo-eigenschappen op Hallo kenmerk weerspiegelen Hallo fysieke kenmerken van Hallo UDT. Deze klasse kan niet worden overgenomen.

SqlUserDefinedType is een vereist kenmerk voor UDT-definitie.

Hallo-constructor van Hallo klasse:  

* SqlUserDefinedTypeAttribute (type-indeling)

* Typ formatter: parameter toodefine een formatter UDT--vereist in het bijzonder Hallo type Hallo `IFormatter` interface hier moet worden doorgegeven.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* Typische UDT vereist ook definitie van Hallo IFormatter interface, zoals wordt weergegeven in Hallo voorbeeld te volgen:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Hallo `IFormatter` interface serialiseert en ongedaan serialiseert een objectgrafiek met Hallo hoofdtype van \<typeparamref name = "T" >.

\<typeparam name = "T" > Hallo hoofdtype voor Hallo object grafiek tooserialize en te deserialiseren.

* **Deserialiseren**: ongedaan serialiseert Hallo gegevens op Hallo opgegeven stroom en reconstitutes Hallo graph-objecten.

* **Serialiseren**: een object of de grafiek van objecten, serialiseert Hello opgegeven hoofdmap toohello opgegeven stroom.

`MyType`exemplaar: exemplaar van het Hallo-type.  
`IColumnWriter`schrijver / `IColumnReader` lezer: Hallo onderliggende stroom van de kolom.  
`ISerializationContext`context: Enum die definieert een aantal vlaggen waarmee de Hallo bron of bestemming context voor Hallo stroom tijdens de serialisatie wordt.

* **Tussenliggende**: Hiermee geeft u op die Hallo bron of bestemming context is geen permanente opslag.

* **Persistentie**: Hiermee geeft u op die Hallo bron of bestemming context is een persistente archief.

Als een reguliere C#-type, een U-SQL-UDT-definitie kunt opnemen overschrijvingen voor operators zoals +/ == /! =. Het kan ook betekenen dat statische methoden. Bijvoorbeeld, als we gaan toouse deze UDT als een parameter tooa statistische functie MIN U-SQL, we hebben toodefine < operator overschrijven.

Eerder in deze handleiding wordt gedemonstreerd een voorbeeld van de fiscale periode-id van de specifieke datum Hallo Hallo indeling Qn:Pn (Q1:P10). Hallo volgende voorbeeld ziet u hoe toodefine een aangepast type voor fiscale periode waarden.

Hieronder volgt een voorbeeld van een code-behind sectie met aangepaste UDT en IFormatter-interface:

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

Hallo gedefinieerd type bevat twee getallen: kwartaal en maand. Operators == /! = / > / < en statische methode ToString() Hier worden gedefinieerd.

Zoals eerder gezegd, UDT kan worden gebruikt in expressies voor SELECT, maar kan niet worden gebruikt in OUTPUTTER/zelfstandig uitpakken zonder aangepaste serialisatie. Het bevat toobe geserialiseerd als een tekenreeks met ToString() of gebruikt met een aangepaste OUTPUTTER/zelfstandig uitpakken.

Nu gaan we gebruik van UDT bespreken. In een sectie code-behind we onze GetFiscalPeriod functie toohello volgende gewijzigd:

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

Zoals u ziet, wordt het Hallo-waarde van het type van onze FiscalPeriod.

Hier bieden we een voorbeeld van hoe de toouse is verder in base U-SQL-script. In dit voorbeeld laat zien dat verschillende vormen van UDT-aanroep van U-SQL-script.

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

Hier volgt een voorbeeld van een volledige code-behind-sectie:

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

## <a name="use-user-defined-aggregates-udagg"></a>Gebruik van de gebruiker gedefinieerde aggregaties: UDAGG
Gebruiker gedefinieerde aggregaties zijn niet out-of-the-box met U-SQL is geen aggregatie-gerelateerde functies die zijn verzonden. Hallo voorbeeld kan worden een cumulatieve tooperform aangepaste math berekeningen, samenvoegingen van tekenreeksen bewerkingen met tekenreeksen, enzovoort.

definitie van de gebruiker gedefinieerde cumulatieve basisklasse Hallo is als volgt:

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

**SqlUserDefinedAggregate** geeft aan dat het Hallo-type moet worden geregistreerd als een gebruiker gedefinieerde aggregatie. Deze klasse kan niet worden overgenomen.

SqlUserDefinedType kenmerk **optionele** voor UDAGG definitie.


Hallo basisklasse kunt u abstracte parameters toopass drie: twee als invoerparameters en één als Hallo resultaat. Hallo-gegevenstypen zijn variabel en tijdens klassenovername moeten worden gedefinieerd.

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

* **Init** roept eenmaal voor elke groep tijdens berekening. Het biedt een initialisatieroutine voor elke groep aggregatie.  
* **Verzamelt** één keer uitgevoerd voor elke waarde. Biedt de belangrijkste functionaliteit Hallo voor Hallo aggregatie-algoritme. Het kan gebruikte tooaggregate waarden met verschillende gegevenstypen die zijn gedefinieerd tijdens klassenovername zijn. Deze kan twee parameters van de variabele gegevenstypen accepteren.
* **Beëindigen** eenmaal per groep aan Hallo einde van het verwerken van toooutput Hallo resultaat voor elke groep aggregatie wordt uitgevoerd.

toodeclare juiste invoer en uitvoer-gegevenstypen, gebruikt de klassendefinitie Hallo als volgt:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: De eerste parameter tooaccumulate
* T2: De eerste parameter tooaccumulate
* TResult: Retourtype van beëindigen

Bijvoorbeeld:

```
public class GuidAggregate : IAggregate<string, int, int>
```

of

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Gebruik UDAGG in U-SQL
toouse UDAGG, eerst Definieer dit in code-behind of ernaar verwijzen vanuit Hallo-bestaande programmeerbaarheid DLL zoals hierboven besproken.

Gebruik vervolgens Hallo de volgende syntaxis:

```
AGG<UDAGG_functionname>(param1,param2)
```

Hier volgt een voorbeeld van UDAGG:

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

En U-SQL-script gebaseerd:

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

In dit scenario use case samenvoegen we klasse GUID's voor specifieke gebruikers Hallo.

## <a name="use-user-defined-objects-udo"></a>Gebruik van de gebruiker gedefinieerde objecten: UDO
U-SQL kunt u toodefine aangepaste programmeerbaarheid objecten, die de gebruiker gedefinieerde objecten of UDO worden genoemd.

Hallo Hier volgt een lijst met UDO in U-SQL:

* Gebruiker gedefinieerde extractie
    * Uitpakken per rij
    * Tooimplement gegevens uitpakken van bestanden met aangepaste gestructureerde gebruikt

* Gebruiker gedefinieerde outputters
    * Uitvoer per rij
    * Gebruikt de aangepaste gegevenstypen toooutput of aangepaste bestandsindelingen

* Gebruiker gedefinieerde processors
    * Één rij en produceert één rij
    * Gebruikte tooreduce Hallo aantal kolommen of produceren van nieuwe kolommen met waarden die zijn afgeleid van een bestaande set kolommen

* Gebruiker gedefinieerde appliers
    * Één rij en produceert 0 toon rijen
    * Gebruikt met buitenste/CROSS toepassen

* Gebruiker gedefinieerde combiners
    * Combineert rijensets--gebruiker gedefinieerde JOINs

* Gebruiker gedefinieerde verkleiningstoestellen
    * N rijen en produceert één rij
    * Tooreduce hello aantal rijen dat wordt gebruikt

UDO wordt normaal gesproken expliciet aangeroepen in de U-SQL-script als onderdeel van Hallo U-SQL-instructies te volgen:

* UITPAKKEN
* UITVOER
* PROCES
* COMBINEREN
* VERMINDEREN

> [!NOTE]  
> De UDO zijn beperkt tooconsume 0,5 Gb geheugen.  Deze beperking geheugen toolocal uitvoeringen niet van toepassing.

## <a name="use-user-defined-extractors"></a>Gebruik van de gebruiker gedefinieerde extractie
U-SQL kunt u tooimport externe gegevens door het gebruik van een instructie uitpakken. Een instructie EXTRACT kunt ingebouwde UDO extractie gebruiken:  

* *Extractors.Text()*: extractie van tekstbestanden met scheidingstekens van andere coderingen biedt.

* *Extractors.Csv()*: uitpakken van het bestand met door komma's gescheiden waarden (CSV)-bestanden van andere coderingen biedt.

* *Extractors.Tsv()*: extractie van tabblad gescheiden waarden (TSV)-bestanden van andere coderingen biedt.

Het kan zijn nuttig toodevelop een aangepaste zelfstandig uitpakken. Dit kan nuttig zijn bij het importeren van gegevens als we willen toodo van Hallo taken te volgen:

* Invoer gegevens wijzigen door het splitsen van kolommen en afzonderlijke waarden te wijzigen. Hallo processorfunctionaliteit is het beter voor het combineren van kolommen.
* Niet-gestructureerde gegevens zoals webpagina's en e-mailberichten of niet semi-gestructureerde gegevens, zoals XML/JSON parseren.
* Parseren van gegevens in niet-ondersteunde codering.

een gebruiker gedefinieerde zelfstandig uitpakken, toodefine of USIEF, moeten we toocreate een `IExtractor` interface. Alle parameters toohello zelfstandig uitpakken, zoals gedefinieerd in de constructor van de klasse Hallo Hallo toobe kolom/rij scheidingstekens en codering, moeten worden ingevoerd. Hallo `IExtractor` interface moet ook een definitie voor Hallo bevatten `IEnumerable<IRow>` overschrijven als volgt:

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

Hallo **SqlUserDefinedExtractor** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een door de gebruiker gedefinieerde zelfstandig uitpakken. Deze klasse kan niet worden overgenomen.

SqlUserDefinedExtractor is een optionele kenmerk voor de definitie van USIEF. Het toodefine AtomicFileProcessing eigenschap gebruikt voor Hallo USIEF object.

* BOOL AtomicFileProcessing   

* **de waarde True** = geeft aan dat deze zelfstandig uitpakken atomic invoerbestanden (JSON, XML,...) is vereist
* **False** = geeft aan dat deze zelfstandig uitpakken geschikt is voor gesplitste / gedistribueerde bestanden (CSV, SEQ,...)

Hallo USIEF programmeerbaarheid hoofdobjecten zijn **invoer** en **uitvoer**. Hallo invoerobject is gebruikte tooenumerate invoergegevens als `IUnstructuredReader`. Hallo uitvoer-object is de uitvoergegevens gebruikte tooset als gevolg van Hallo zelfstandig uitpakken activiteit.

Hallo invoergegevens toegankelijk is via `System.IO.Stream` en `System.IO.StreamReader`.

Voor invoerkolommen-opsomming splitsen we eerst Hallo invoerstroom met behulp van een rijscheidingsteken.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Vervolgens verder rij invoer in kolom delen gesplitst.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

tooset uitvoergegevens, gebruiken we Hallo `output.Set` methode.

Het is belangrijk toounderstand die aangepaste zelfstandig uitpakken Hallo levert alleen kolommen en waarden die zijn gedefinieerd met de Hallo uitvoer. Aanroep van methode instellen.

```
output.Set<string>(count, part);
```

Hallo werkelijke zelfstandig uitpakken uitvoer wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.

Dit is Hallo zelfstandig uitpakken voorbeeld:

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

In dit scenario use case Hallo zelfstandig uitpakken genereert Hallo GUID voor kolom 'guid' en zet Hallo-waarden van 'gebruiker' kolom tooupper case. Aangepaste extractie kunnen gecompliceerdere resultaten opleveren door invoergegevens geparseerd en bewerkt.

Hieronder vindt u base U-SQL-script dat gebruikmaakt van een aangepaste zelfstandig uitpakken:

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

## <a name="use-user-defined-outputters"></a>Gebruik van de gebruiker gedefinieerde outputters
Gebruiker gedefinieerde outputter is een andere U-SQL-UDO waarmee u tooextend ingebouwde U-SQL-functionaliteit. Vergelijkbare toohello zelfstandig uitpakken, er zijn verschillende ingebouwde outputters.

* *Outputters.Text()*: schrijft gegevens toodelimited tekstbestanden van andere coderingen.
* *Outputters.Csv()*: schrijft gegevens toocomma gescheiden waarden (CSV)-bestanden van andere coderingen.
* *Outputters.Tsv()*: schrijft gegevens tootab gescheiden waarden (TSV)-bestanden van andere coderingen.

Aangepaste outputter kunt u toowrite gegevens in een aangepaste gedefinieerde indeling. Dit kan handig zijn voor Hallo taken te volgen:

* Schrijven van toosemi gestructureerde of ongestructureerde gegevens.
* Coderingen schrijven van gegevens niet worden ondersteund.
* Uitvoergegevens te wijzigen of toevoegen van aangepaste kenmerken.

toodefine door gebruiker gedefinieerde outputter, moeten we toocreate hello `IOutputter` interface.

Hieronder vindt u Hallo base `IOutputter` implementatie van klasse:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Alle invoer parameters toohello outputter, zoals kolom/rij scheidingstekens, codering, enzovoort, moeten toobe gedefinieerd in de constructor Hallo van Hallo-klasse. Hallo `IOutputter` interface moet ook een definitie voor bevatten `void Output` overschrijven. Hallo-kenmerk `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` kan eventueel worden ingesteld voor verwerking-atomic-bestand. Zie de volgende details Hallo voor meer informatie.

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

* `Output`voor elke rij invoer wordt genoemd. Deze retourneert Hallo `IUnstructuredWriter output` rijenset.
* Hallo Constructor klasse wordt gebruikt toopass parameters toohello gebruiker gedefinieerde outputter.
* `Close`wordt gebruikt toooptionally toorelease dure status overschrijven of bepalen wanneer de laatste rij Hallo is geschreven.

**SqlUserDefinedOutputter** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een gebruiker gedefinieerde outputter. Deze klasse kan niet worden overgenomen.

SqlUserDefinedOutputter is een optionele kenmerk voor een definitie van de gebruiker gedefinieerde outputter. Deze toodefine hello AtomicFileProcessing eigenschap gebruikt.

* BOOL AtomicFileProcessing   

* **de waarde True** = geeft aan dat deze outputter atomic uitvoerbestanden (JSON, XML,...) is vereist
* **False** = geeft aan dat deze outputter geschikt is voor gesplitste / gedistribueerde bestanden (CSV, SEQ,...)

Hallo belangrijkste programmeerbaarheid objecten zijn **rij** en **uitvoer**. Hallo **rij** -object is de uitvoergegevens gebruikte tooenumerate als `IRow` interface. **Uitvoer** gebruikte tooset toohello doel uitvoergegevensbestand is.

Hallo uitvoergegevens toegankelijk is via Hallo `IRow` interface. Uitvoergegevens is een rij tegelijk doorgegeven.

Hallo afzonderlijke waarden worden geïnventariseerd door het aanroepen van Get-methode van de interface IRow Hallo Hallo:

```
row.Get<string>("column_name")
```

Afzonderlijke kolomnamen kunnen worden bepaald door het aanroepen van `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Deze aanpak kunt u een flexibele outputter voor elke metagegevensschema toobuild.

Hallo uitvoergegevens is geschreven in toofile `System.IO.StreamWriter`. Hallo-stroom is parameterset te`output.BaseStrea` als onderdeel van `IUnstructuredWriter output`.

Houd er rekening mee dat het is belangrijk tooflush Hallo buffer toohello gegevensbestand na elke iteratie rij. Bovendien Hallo `StreamWriter` object moet worden gebruikt met Hallo beschikbare kenmerk ingeschakeld (standaard) en Hallo **met** sleutelwoord:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

Anders expliciet worden aangeroepen methode Flush() na elke iteratie. We zien in het volgende voorbeeld Hallo.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Kopteksten en voetteksten ingesteld voor de gebruiker gedefinieerde outputter
een koptekst tooset gebruiken één iteratie uitvoering stroom.

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

Hallo-code in Hallo eerst `if (isHeaderRow)` blok wordt slechts één keer uitgevoerd.

Gebruik voor voettekst Hallo Hallo verwijzing toohello exemplaar van `System.IO.Stream` object (`output.BaseStream`). Schrijf Hallo voettekst in Hallo Close() methode Hallo `IOutputter` interface.  (Zie Hallo voorbeeld te volgen voor meer informatie.)

Hieronder volgt een voorbeeld van een gebruiker gedefinieerde outputter:

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

En base U-SQL-script:

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

Dit is een HTML-outputter een HTML-bestand gemaakt met gegevens in een tabel.

### <a name="call-outputter-from-u-sql-base-script"></a>Outputter aanroepen vanuit base U-SQL-script
een aangepaste outputter van Hallo base U-SQL-script toocall, Hallo nieuw exemplaar van Hallo outputter object heeft toobe gemaakt.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

maken van een exemplaar van Hallo tooavoid object base script maken we een wrapper functie, zoals wordt weergegeven in het vorige voorbeeld:

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

De oorspronkelijke aanroep Hallo ziet in dit geval er Hallo volgende:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Gebruiker gedefinieerde processors gebruiken
Gebruiker gedefinieerde processor- of UDP, is een type van U-SQL-UDO waarmee u tooprocess Hallo binnenkomende rijen door toe te passen programmeerbare functies. UDP, kunt u toocombine kolommen, wijzigt u de waarden en nieuwe kolommen toevoegen, indien nodig. In principe helpt het tooprocess een rijenset tooproduce vereiste elementen.

toodefine een UDP, moeten we toocreate een `IProcessor` interface Hello `SqlUserDefinedProcessor` kenmerk optioneel voor UDP is.

Deze interface moet een definitie van Hallo voor Hallo bevatten `IRow` interface rijenset overschrijven, zoals wordt weergegeven in Hallo voorbeeld te volgen:

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

**SqlUserDefinedProcessor** geeft aan dat het Hallo-type moet worden geregistreerd als een gebruiker gedefinieerde processor. Deze klasse kan niet worden overgenomen.

Hallo SqlUserDefinedProcessor kenmerk **optionele** voor UDP-definitie.

Hallo belangrijkste programmeerbaarheid objecten zijn **invoer** en **uitvoer**. Hallo invoerobject is gebruikte tooenumerate invoerkolommen en uitvoer en de uitvoergegevens tooset als gevolg van Hallo processoractiviteit.

Voor de opsomming invoerkolommen, gebruiken we Hallo `input.Get` methode.

```
string column_name = input.Get<string>("column_name");
```

parameter voor Hallo `input.Get` methode is een kolom die wordt doorgegeven als onderdeel van Hallo `PRODUCE` component Hallo `PROCESS` instructie van base Hallo U-SQL-script. We moeten toouse Hallo juiste gegevenstype hier.

Gebruik voor uitvoer Hallo `output.Set` methode.

Het is belangrijk toonote die aangepaste producent alleen levert kolommen en waarden die zijn gedefinieerd door hello `output.Set` methodeaanroep.

```
output.Set<string>("mycolumn", mycolumn);
```

Hallo werkelijke processor uitvoer wordt geactiveerd door het aanroepen van `return output.AsReadOnly();`.

Hier volgt een voorbeeld van een processor:

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

In dit scenario use case Hallo processor genereert een nieuwe kolom 'full_description' door een combinatie van Hallo bestaande kolommen--in dit geval 'gebruiker' in hoofdletters en 'des' genoemd. Ook worden opnieuw gegenereerd door een GUID en Hallo oorspronkelijke en nieuwe GUID-waarden retourneert.

Als u in het vorige voorbeeld Hallo zien kunt, kunt u C#-methoden tijdens aanroepen `output.Set` methodeaanroep.

Hieronder volgt een voorbeeld van base U-SQL-script dat gebruikmaakt van een aangepaste processor:

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

## <a name="use-user-defined-appliers"></a>Gebruik van de gebruiker gedefinieerde appliers
Een gebruiker gedefinieerde applier van U-SQL kunt u tooinvoke een aangepaste C#-functie voor elke rij die wordt geretourneerd door de buitenste tabelexpressie Hallo van een query. de juiste invoerwaarden Hello wordt geëvalueerd voor elke rij uit de linker invoer Hallo en Hallo rijen die worden gemaakt voor de uiteindelijke uitvoer Hallo worden gecombineerd. Hallo-lijst met kolommen die worden geproduceerd door de operator APPLY Hallo zijn Hallo combinatie van Hallo set kolommen in Hallo links en Hallo rechts invoer.

Als onderdeel van Hallo expressie USQL Selecteer wordt gebruiker gedefinieerde applier aangeroepen.

Hallo typische aanroep toohello gebruiker gedefinieerde applier lijkt erop Hallo volgende:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Zie voor meer informatie over het gebruik van appliers in een SELECT-expressie [U-SQL Selecteer selecteren in de CROSS APPLY en OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).

Hallo gebruiker gedefinieerde applier basisklassendefinitie is als volgt:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

een door de gebruiker gedefinieerde applier toodefine, moeten we toocreate hello `IApplier` interface met Hallo [`SqlUserDefinedApplier`] kenmerk, maar dit optioneel voor een gebruiker gedefinieerde applier definitie is.

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

* Van toepassing is aangeroepen voor elke rij van de buitenste tabel Hallo. Deze retourneert Hallo `IUpdatableRow` uitvoer van de rijenset.
* Hallo Constructor klasse is gebruikte toopass parameters toohello gebruiker gedefinieerde applier.

**SqlUserDefinedApplier** geeft aan dat het Hallo-type moet worden geregistreerd als een gebruiker gedefinieerde applier. Deze klasse kan niet worden overgenomen.

**SqlUserDefinedApplier** is **optionele** voor een gebruiker gedefinieerde applier definitie.


Hallo belangrijkste programmeerbare objecten zijn als volgt:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Invoer rijensets worden doorgegeven als `IRow` invoer. Hallo rijen uitvoer gegenereerd als `IUpdatableRow` uitvoer-interface.

Afzonderlijke kolomnamen kunnen worden bepaald door de aanroepende Hallo `IRow` Schema-methode.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

tooget hello werkelijke gegevenswaarden van inkomende hello `IRow`, gebruiken we Hallo Get() methode van `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Of we de schemanaam kolom hello gebruiken:

```
row.Get<int>(row.Schema[0].Name)
```

Hallo uitvoerwaarden moeten worden ingesteld met `IUpdatableRow` uitvoer:

```
output.Set<int>("mycolumn", mycolumn)
```

Het is belangrijk toounderstand aangepaste appliers alleen uitvoer kolommen en waarden die zijn gedefinieerd met `output.Set` methodeaanroep.

Hallo werkelijke output wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.

Hallo gebruiker gedefinieerde applier parameters kunnen toohello-constructor worden doorgegeven. Applier kunnen een variabele aantal kolommen dat toobe gedefinieerd tijdens Hallo applier aanroep in base U-SQL-Script moet worden geretourneerd.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Hier volgt Hallo gebruiker gedefinieerde applier voorbeeld:

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

Hieronder vindt u Hallo base U-SQL-script voor deze gebruiker gedefinieerde applier:

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

In dit scenario gebruik case vissersvloot applier fungeert als een door komma's gescheiden waarde parser voor Hallo auto gebruiker gedefinieerde eigenschappen. Hallo invoerbestand rijen eruitzien als Hallo volgende:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Er is een typische door tabs gescheiden TSV bestand met een kolom met eigenschappen van die auto eigenschappen zoals het merk en model bevat. Deze eigenschappen moet de geparseerde toohello tabelkolommen. Hallo applier die opgegeven kunt u ook toogenerate een dynamische aantal eigenschappen in Hallo rijenset leiden, op basis van het Hallo-parameter die wordt doorgegeven. U kunt alle eigenschappen of een specifieke set eigenschappen alleen genereren.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

Hallo gebruiker gedefinieerde applier kan worden aangeroepen als een nieuw exemplaar van applier object:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Of met Hallo aanroep van een wrapper-fabrieksmethode:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Gebruik van de gebruiker gedefinieerde combiners
Gebruiker gedefinieerde combiner of UDC, kunt u toocombine rijen uit de linker- en rijensets, op basis van aangepaste logica. Gebruiker gedefinieerde combiner wordt met COMBINEREN expressie gebruikt.

Een combiner wordt aangeroepen met de Hallo COMBINEREN expressie waarmee Hallo nodige informatie over beide invoer rijensets hello, groeperen kolommen, Hallo Hallo verwacht resultaat schema en aanvullende informatie.

toocall een combiner in een base U-SQL-script, gebruiken we Hallo de volgende syntaxis:

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

Zie voor meer informatie [COMBINEREN expressie (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).

een door de gebruiker gedefinieerde combiner toodefine, moeten we toocreate hello `ICombiner` interface met Hallo [`SqlUserDefinedCombiner`] kenmerk optioneel voor een definitie van een gebruiker gedefinieerde Combiner is.

Base `ICombiner` definitie van klasse:

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

Hallo aangepaste implementatie van een `ICombiner` interface moet bevatten Hallo definitie voor een `IEnumerable<IRow>` onderdrukking combineren.

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

Hallo **SqlUserDefinedCombiner** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een gebruiker gedefinieerde combiner. Deze klasse kan niet worden overgenomen.

**SqlUserDefinedCombiner** is gebruikte toodefine hello Combiner modus eigenschap. Het is een optioneel kenmerk voor een definitie van de gebruiker gedefinieerde combiner.

CombinerMode modus

CombinerMode enum kan duren voordat Hallo volgende waarden:

* Volledig (0) alle Hallo invoer rijen uit elke rij van de uitvoer mogelijk afhankelijk linker- en Hallo met dezelfde sleutelwaarde.

* Links (1), elke rij van de uitvoer is afhankelijk van één rij invoer van Hallo links (en mogelijk alle rijen uit Hallo Hallo met dezelfde sleutelwaarde).

* Rechts (2), elke rij van de uitvoer is afhankelijk van één rij invoer van de juiste hello (en mogelijk alle rijen uit Hallo links Hello dezelfde sleutelwaarde).

* Interne (3), elke rij van de uitvoer is afhankelijk van een invoer van één rij uit de linker- en rechterzijde Hello dezelfde waarde.

Voorbeeld: [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


Hallo belangrijkste programmeerbare objecten zijn:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Invoer rijensets worden doorgegeven als **links** en **rechts** `IRowset` type interface. Beide rijensets moet worden geïnventariseerd voor verwerking. U kunt elke interface slechts een keer opsommen zodat we tooenumerate hebben en deze in de cache indien nodig.

Voor cachedoeleinden, maken we een lijst\<T\> type geheugenstructuur als gevolg hiervan van een LINQ uitvoering van de query, specifiek lijst <`IRow`>. Hallo anonieme gegevenstype kan worden gebruikt tijdens de opsomming ook.

Zie [inleiding tooLINQ query's (C#)](https://msdn.microsoft.com/library/bb397906.aspx) voor meer informatie over de LINQ-query's en [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) voor meer informatie over IEnumerable\<T\> interface.

tooget hello werkelijke gegevenswaarden van inkomende hello `IRowset`, gebruiken we Hallo Get() methode van `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Afzonderlijke kolomnamen kunnen worden bepaald door de aanroepende Hallo `IRow` Schema-methode.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Of met behulp van de schemanaam kolom Hallo:

```
c# row.Get<int>(row.Schema[0].Name)
```

Hallo algemene opsomming met LINQ ziet er Hallo volgende:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

We gaan tooloop via alle rijen na het inventariseren van beide rijensets. Voor elke rij in het linkerdeelvenster rijenset hello gaan we toofind alle rijen die voldoen aan de voorwaarde van onze combiner Hallo.

Hallo uitvoerwaarden moeten worden ingesteld met `IUpdatableRow` uitvoer.

```
output.Set<int>("mycolumn", mycolumn)
```

Hallo werkelijke output wordt geactiveerd door aan te roepen te`yield return output.AsReadOnly();`.

Hier volgt een voorbeeld van een combiner:

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

In dit scenario use case wordt een rapport analytics voor Hallo detailhandel gemaakt. Hallo-doel is toofind alle producten die meer dan 20.000 $ en die kosten via Hallo website sneller dan via reguliere detailhandel Hallo binnen een bepaald tijdsbestek verkopen.

Hier volgt Hallo base U-SQL-script. U kunt Hallo logica tussen een OUTER-JOIN en een combiner vergelijken:

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

Een door de gebruiker gedefinieerde combiner kan worden aangeroepen als een nieuw exemplaar van Hallo applier object:

```
USING new MyNameSpace.MyCombiner();
```


Of met Hallo aanroep van een wrapper-fabrieksmethode:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Gebruik van de gebruiker gedefinieerde verkleiningstoestellen

U-SQL kunt u toowrite aangepaste rijenset verkleiningstoestellen in C# met behulp van Hallo gebruiker gedefinieerde operator uitbreidbaarheid framework en een IReducer-interface implementeren.

Gebruiker gedefinieerde reducer of UDR, kan gebruikte tooeliminate onnodige rijen zijn tijdens het ophalen van gegevens (importeren). Het kan ook worden gebruikt toomanipulate en evalueren rijen en kolommen. Op basis van programmeerbaarheid logica, kunt deze ook bepalen welke rijen moeten toobe hebt uitgepakt.

een klasse UDR toodefine, moeten we toocreate een `IReducer` interface met een optionele `SqlUserDefinedReducer` kenmerk.

Deze klasseninterface moet een definitie voor Hallo bevatten `IEnumerable` interface rijenset overschrijven.

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

Hallo **SqlUserDefinedReducer** kenmerk geeft aan dat Hallo type moet worden geregistreerd als een gebruiker gedefinieerde reducer. Deze klasse kan niet worden overgenomen.
**SqlUserDefinedReducer** is een optioneel kenmerk voor een definitie van de gebruiker gedefinieerde reducer. Deze toodefine IsRecursive eigenschap gebruikt.

* BOOL IsRecursive    
* **de waarde True** = geeft aan of deze Reducer idempotent

Hallo belangrijkste programmeerbaarheid objecten zijn **invoer** en **uitvoer**. Hallo invoerobject is gebruikte tooenumerate invoer rijen. Uitvoer is gebruikte tooset uitvoer rijen als gevolg van de activiteit te verminderen.

Voor invoer rijen opsomming, gebruiken we Hallo `Row.Get` methode.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

de parameter voor Hallo Hallo `Row.Get` methode is een kolom die wordt doorgegeven als onderdeel van Hallo `PRODUCE` klasse Hallo `REDUCE` instructie van base Hallo U-SQL-script. We moeten toouse Hallo juiste gegevenstype hier ook.

Gebruik voor uitvoer Hallo `output.Set` methode.

Het is belangrijk toounderstand die aangepaste reducer alleen uitvoer de waarden die zijn gedefinieerd met Hallo `output.Set` methodeaanroep.

```
output.Set<string>("mycolumn", guid);
```

Hallo werkelijke reducer uitvoer wordt geactiveerd door het aanroepen van `yield return output.AsReadOnly();`.

Hier volgt een voorbeeld van een reducer:

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

In dit scenario use case Hallo reducer is rijen met een lege gebruikersnaam wordt overgeslagen. Voor elke rij in de rijenset elke vereiste kolom leest, vervolgens Hallo-lengte van de gebruikersnaam Hallo evalueert. Het levert werkelijke rij Hallo alleen als de lengte van de gebruiker de naam van waarde is hoger dan 0.

Hieronder vindt u base U-SQL-script dat gebruikmaakt van een aangepaste reducer:

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
