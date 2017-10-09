---
title: aaaAzure SQL Database JSON-functies | Microsoft Docs
description: Azure SQL Database kunt u tooparse, query- en de gegevens opmaken in de notatie JSON (JavaScript Object)-notatie.
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="9e617-103">Aan de slag met JSON-functies in Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="9e617-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="9e617-104">Azure SQL Database kunt u parseren en een query over gegevens die worden weergegeven in JavaScript Object Notation [(JSON)](http://www.json.org/) formatteren en relationele gegevens worden geëxporteerd als JSON-tekst.</span><span class="sxs-lookup"><span data-stu-id="9e617-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="9e617-105">JSON is een populair gegevensindeling gebruikt voor het uitwisselen van gegevens in moderne webtoepassingen en mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="9e617-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="9e617-106">JSON wordt ook gebruikt voor het opslaan van semi-gestructureerde gegevens in logboekbestanden of in de NoSQL-databases zoals [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="9e617-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="9e617-107">Veel REST-webservices worden opgemaakt als JSON-tekst of gegevens accepteert opgemaakt als JSON.</span><span class="sxs-lookup"><span data-stu-id="9e617-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="9e617-108">De meeste Azure services, zoals [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), en [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) REST-eindpunten die retourneren of JSON gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9e617-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="9e617-109">Azure SQL Database kunt u eenvoudig werken met JSON-gegevens en het integreren van uw database met moderne services.</span><span class="sxs-lookup"><span data-stu-id="9e617-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="9e617-110">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9e617-110">Overview</span></span>
<span data-ttu-id="9e617-111">Azure SQL Database biedt Hallo functies voor het werken met JSON-gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e617-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![JSON-functies](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="9e617-113">Als u JSON-tekst hebt, kunt u gegevens ophalen uit JSON of Controleer of JSON correct is geformatteerd met behulp van de ingebouwde functies Hallo [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), en [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="9e617-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="9e617-114">Hallo [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) functie kunt u de waarde in JSON-tekst wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="9e617-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="9e617-115">Voor meer query's en analyse geavanceerde, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) functie een matrix met JSON-objecten kan omzetten in een set rijen.</span><span class="sxs-lookup"><span data-stu-id="9e617-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="9e617-116">Een SQL-query kan worden uitgevoerd op Hallo heeft een resultatenset geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9e617-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="9e617-117">Ten slotte wordt er is een [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) component waarmee u gegevens in de relationele tabellen wordt opgeslagen als JSON-tekst opmaken.</span><span class="sxs-lookup"><span data-stu-id="9e617-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="9e617-118">Opmaak van relationele gegevens in JSON-indeling</span><span class="sxs-lookup"><span data-stu-id="9e617-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="9e617-119">Als u een webservice dat vergt gegevens uit de database Hallo layer en biedt een reactie in JSON-indeling of clientzijde JavaScript frameworks en bibliotheken die gegevens accepteert die zijn opgemaakt als JSON hebt, kunt u de inhoud van uw database opmaken als JSON rechtstreeks in een SQL-query.</span><span class="sxs-lookup"><span data-stu-id="9e617-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="9e617-120">U niet langer toowrite toepassingscode die indelingen van resultaten van Azure SQL Database als JSON, of hebben sommige JSON-serialisatie bibliotheek tooconvert tabellaire queryresultaten opnemen en vervolgens serialiseren objecten tooJSON indeling.</span><span class="sxs-lookup"><span data-stu-id="9e617-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="9e617-121">U kunt in plaats daarvan Hallo voor JSON-component tooformat SQL-queryresultaten gebruiken als JSON-code in Azure SQL Database en deze gebruiken rechtstreeks in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9e617-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="9e617-122">Rijen uit Hallo Sales.Customer tabel zijn Hallo voorbeeld te volgen, opgemaakt als JSON met behulp van hello FOR JSON-component:</span><span class="sxs-lookup"><span data-stu-id="9e617-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="9e617-123">Hallo-resultaten van Hallo query Hello FOR JSON PATH component opgemaakt als JSON-tekst.</span><span class="sxs-lookup"><span data-stu-id="9e617-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="9e617-124">Kolomnamen worden gebruikt als de sleutels, Hallo celwaarden als JSON-waarden worden gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="9e617-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="9e617-125">Hallo resultatenset is opgemaakt als een JSON-matrix waarbij elke rij is opgemaakt als een afzonderlijk JSON-object.</span><span class="sxs-lookup"><span data-stu-id="9e617-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="9e617-126">PAD geeft aan dat u met puntnotatie in Kolomaliassen Hallo de indeling van de uitvoer van uw JSON-resultaat kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="9e617-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="9e617-127">Hallo query na Hallo-naam van Hallo 'CustomerName' sleutel Hallo uitvoer JSON-indeling wordt gewijzigd en telefoon-en faxnummer op Hallo 'Neem contact op met' onderliggende object worden geplaatst:</span><span class="sxs-lookup"><span data-stu-id="9e617-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="9e617-128">Hallo-uitvoer van deze query ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="9e617-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="9e617-129">In dit voorbeeld wordt een JSON-object in plaats van een matrix geretourneerd door te geven Hallo [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) optie.</span><span class="sxs-lookup"><span data-stu-id="9e617-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="9e617-130">U kunt deze optie gebruiken als u weet dat u een enkel object als gevolg van de query retourneert.</span><span class="sxs-lookup"><span data-stu-id="9e617-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="9e617-131">belangrijkste waarde Hallo Hallo FOR JSON-component is dat Hiermee kunt u complexe hiërarchische gegevens worden geretourneerd uit de database die is geformatteerd als geneste JSON-objecten of -matrices.</span><span class="sxs-lookup"><span data-stu-id="9e617-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="9e617-132">Hallo voorbeeld ziet u hoe tooinclude Orders die deel uitmaken van de klant toohello als een geneste matrix van Orders te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e617-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="9e617-133">In plaats van het verzenden van gegevens van de klant tooget afzonderlijke query's en klik vervolgens op toofetch een lijst met verwante Orders, kunt u alle benodigde Hallo-gegevens met een enkele query opvragen, zoals wordt weergegeven in de volgende voorbeelduitvoer Hallo:</span><span class="sxs-lookup"><span data-stu-id="9e617-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="9e617-134">Werken met JSON-gegevens</span><span class="sxs-lookup"><span data-stu-id="9e617-134">Working with JSON data</span></span>
<span data-ttu-id="9e617-135">Als u geen strikt gestructureerde gegevens als u complexe onderliggende objecten, matrices of hiërarchische gegevens hebt, of als uw gegevensstructuren gedurende een bepaalde periode evolueren, Hallo JSON-indeling u toorepresent helpen kan elke complexe gegevensstructuur.</span><span class="sxs-lookup"><span data-stu-id="9e617-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="9e617-136">JSON wordt een tekstuele indeling die kan worden gebruikt als andere tekenreekstype in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="9e617-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="9e617-137">U kunt verzenden of JSON-gegevens opslaan als een standaard NVARCHAR:</span><span class="sxs-lookup"><span data-stu-id="9e617-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="9e617-138">Hallo JSON-gegevens in dit voorbeeld gebruikt wordt met behulp van het type NVARCHAR(MAX) hello vertegenwoordigd.</span><span class="sxs-lookup"><span data-stu-id="9e617-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="9e617-139">JSON kan worden ingevoegd in deze tabel of als een argument van Hallo opgeslagen procedure met behulp van standaard Transact-SQL-syntaxis, zoals weergegeven in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="9e617-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="9e617-140">Elke client-side taal of de bibliotheek die geschikt is voor tekenreeksgegevens in Azure SQL Database werkt ook met JSON-gegevens.</span><span class="sxs-lookup"><span data-stu-id="9e617-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="9e617-141">JSON kan worden opgeslagen in een tabel die ondersteuning biedt voor Hallo NVARCHAR type, zoals een tabel geoptimaliseerd voor geheugen of een systeemversietabel.</span><span class="sxs-lookup"><span data-stu-id="9e617-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="9e617-142">JSON wordt geen eventuele beperkingen in Hallo clientcode of in Hallo databaselaag.</span><span class="sxs-lookup"><span data-stu-id="9e617-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="9e617-143">JSON-gegevens opvragen</span><span class="sxs-lookup"><span data-stu-id="9e617-143">Querying JSON data</span></span>
<span data-ttu-id="9e617-144">Als u gegevens die zijn opgemaakt als JSON opgeslagen in Azure SQL-tabellen, kunnen JSON-functies u deze gegevens in een SQL-query.</span><span class="sxs-lookup"><span data-stu-id="9e617-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="9e617-145">JSON-functies die beschikbaar in Azure SQL database kunt zijn u gegevens die zijn opgemaakt als JSON als elke andere SQL-gegevenstype behandelen.</span><span class="sxs-lookup"><span data-stu-id="9e617-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="9e617-146">U kunt eenvoudig waarden ophalen uit JSON-tekst hello en JSON-gegevens in een query gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9e617-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="9e617-147">Hallo JSON_VALUE functie haalt een waarde van de JSON-tekst opgeslagen in de kolom Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="9e617-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="9e617-148">Deze functie gebruikt een JavaScript-achtige pad tooreference een waarde in JSON-tekst tooextract.</span><span class="sxs-lookup"><span data-stu-id="9e617-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="9e617-149">Hallo uitgepakt waarde kan worden gebruikt in een deel van de SQL-query.</span><span class="sxs-lookup"><span data-stu-id="9e617-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="9e617-150">Hallo JSON_QUERY-functie is vergelijkbaar tooJSON_VALUE.</span><span class="sxs-lookup"><span data-stu-id="9e617-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="9e617-151">In tegenstelling tot JSON_VALUE pakt deze functie complexe onderliggende object zoals matrices of objecten die in JSON-tekst worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="9e617-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="9e617-152">Hallo JSON_MODIFY functie kunt u Hallo-pad van het Hallo-waarde opgeven in Hallo JSON-tekst die moet worden bijgewerkt, evenals een nieuwe waarde die Hallo oude wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="9e617-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="9e617-153">Op deze manier kunt u eenvoudig bijwerken JSON-tekst zonder reparsing Hallo volledige structuur.</span><span class="sxs-lookup"><span data-stu-id="9e617-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="9e617-154">Aangezien JSON is opgeslagen in een standaardtekst, zijn er geen garanties dat Hallo waarden die zijn opgeslagen in tekstkolommen juist zijn opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e617-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="9e617-155">U kunt controleren tekst opgeslagen in JSON-kolom is correct opgemaakt met behulp van standaard check-beperkingen voor Azure SQL Database en Hallo ISJSON functie:</span><span class="sxs-lookup"><span data-stu-id="9e617-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="9e617-156">Als de ingevoerde tekst hello is juist opgemaakt JSON, Hallo ISJSON functie retourneert Hallo waarde 1.</span><span class="sxs-lookup"><span data-stu-id="9e617-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="9e617-157">Bij elke invoegen of bijwerken van de JSON-kolom, controleert deze beperking of nieuwe tekstwaarde is niet een verkeerd ingedeelde JSON.</span><span class="sxs-lookup"><span data-stu-id="9e617-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="9e617-158">Omzetten van JSON in tabelvorm</span><span class="sxs-lookup"><span data-stu-id="9e617-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="9e617-159">Azure SQL Database kunt u verzamelingen JSON in tabelvorm indeling en load of query JSON-gegevens te transformeren.</span><span class="sxs-lookup"><span data-stu-id="9e617-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="9e617-160">OPENJSON is een tabelwaarde functie die parseert JSON-tekst, zoekt de client een matrix met JSON-objecten, Hallo-elementen van de matrix Hallo doorlopen en retourneert één rij in Hallo uitvoerresultaat voor elk element van het Hallo-matrix.</span><span class="sxs-lookup"><span data-stu-id="9e617-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON in tabelvorm](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="9e617-162">Hallo bovenstaande voorbeeld kunt we opgeven waar toolocate Hallo JSON-matrix die moet worden geopend (in Hallo $. Orders pad), welke kolommen moeten worden geretourneerd als resultaat en waar toofind Hallo JSON-waarden die worden geretourneerd als in de cellen.</span><span class="sxs-lookup"><span data-stu-id="9e617-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="9e617-163">We kunnen een JSON-matrix in Hallo transformeren @orders variabele in een set rijen, deze resultaatset analyseren of invoegen van rijen in een standaard tabel:</span><span class="sxs-lookup"><span data-stu-id="9e617-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="9e617-164">Hallo verzameling orders opgemaakt als een JSON-matrix en die als een parameter toohello opgeslagen procedure kan worden geparseerd en ingevoegd in de tabel Orders hello wordt verstrekt.</span><span class="sxs-lookup"><span data-stu-id="9e617-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e617-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e617-165">Next steps</span></span>
<span data-ttu-id="9e617-166">toolearn hoe toointegrate JSON in uw toepassing, bekijk deze resources:</span><span class="sxs-lookup"><span data-stu-id="9e617-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="9e617-167">Blog van TechNet</span><span class="sxs-lookup"><span data-stu-id="9e617-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="9e617-168">MSDN-documentatie</span><span class="sxs-lookup"><span data-stu-id="9e617-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="9e617-169">Channel 9 video</span><span class="sxs-lookup"><span data-stu-id="9e617-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="9e617-170">toolearn over diverse scenario's voor het integreren van JSON in uw toepassing hello demo's in deze Zie [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) of vinden van een scenario dat overeenkomt met uw gebruiksvoorbeeld in [JSON blogberichten](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="9e617-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

