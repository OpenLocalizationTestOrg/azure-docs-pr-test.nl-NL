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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Aan de slag met JSON-functies in Azure SQL Database
Azure SQL Database kunt u parseren en een query over gegevens die worden weergegeven in JavaScript Object Notation [(JSON)](http://www.json.org/) formatteren en relationele gegevens worden geëxporteerd als JSON-tekst.

JSON is een populair gegevensindeling gebruikt voor het uitwisselen van gegevens in moderne webtoepassingen en mobiele toepassingen. JSON wordt ook gebruikt voor het opslaan van semi-gestructureerde gegevens in logboekbestanden of in de NoSQL-databases zoals [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/). Veel REST-webservices worden opgemaakt als JSON-tekst of gegevens accepteert opgemaakt als JSON. De meeste Azure services, zoals [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), en [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) REST-eindpunten die retourneren of JSON gebruiken.

Azure SQL Database kunt u eenvoudig werken met JSON-gegevens en het integreren van uw database met moderne services.

## <a name="overview"></a>Overzicht
Azure SQL Database biedt Hallo functies voor het werken met JSON-gegevens te volgen:

![JSON-functies](./media/sql-database-json-features/image_1.png)

Als u JSON-tekst hebt, kunt u gegevens ophalen uit JSON of Controleer of JSON correct is geformatteerd met behulp van de ingebouwde functies Hallo [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), en [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Hallo [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) functie kunt u de waarde in JSON-tekst wordt bijgewerkt. Voor meer query's en analyse geavanceerde, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) functie een matrix met JSON-objecten kan omzetten in een set rijen. Een SQL-query kan worden uitgevoerd op Hallo heeft een resultatenset geretourneerd. Ten slotte wordt er is een [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) component waarmee u gegevens in de relationele tabellen wordt opgeslagen als JSON-tekst opmaken.

## <a name="formatting-relational-data-in-json-format"></a>Opmaak van relationele gegevens in JSON-indeling
Als u een webservice dat vergt gegevens uit de database Hallo layer en biedt een reactie in JSON-indeling of clientzijde JavaScript frameworks en bibliotheken die gegevens accepteert die zijn opgemaakt als JSON hebt, kunt u de inhoud van uw database opmaken als JSON rechtstreeks in een SQL-query. U niet langer toowrite toepassingscode die indelingen van resultaten van Azure SQL Database als JSON, of hebben sommige JSON-serialisatie bibliotheek tooconvert tabellaire queryresultaten opnemen en vervolgens serialiseren objecten tooJSON indeling. U kunt in plaats daarvan Hallo voor JSON-component tooformat SQL-queryresultaten gebruiken als JSON-code in Azure SQL Database en deze gebruiken rechtstreeks in uw toepassing.

Rijen uit Hallo Sales.Customer tabel zijn Hallo voorbeeld te volgen, opgemaakt als JSON met behulp van hello FOR JSON-component:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

Hallo-resultaten van Hallo query Hello FOR JSON PATH component opgemaakt als JSON-tekst. Kolomnamen worden gebruikt als de sleutels, Hallo celwaarden als JSON-waarden worden gegenereerd:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

Hallo resultatenset is opgemaakt als een JSON-matrix waarbij elke rij is opgemaakt als een afzonderlijk JSON-object.

PAD geeft aan dat u met puntnotatie in Kolomaliassen Hallo de indeling van de uitvoer van uw JSON-resultaat kunt aanpassen. Hallo query na Hallo-naam van Hallo 'CustomerName' sleutel Hallo uitvoer JSON-indeling wordt gewijzigd en telefoon-en faxnummer op Hallo 'Neem contact op met' onderliggende object worden geplaatst:

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

Hallo-uitvoer van deze query ziet er als volgt:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

In dit voorbeeld wordt een JSON-object in plaats van een matrix geretourneerd door te geven Hallo [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) optie. U kunt deze optie gebruiken als u weet dat u een enkel object als gevolg van de query retourneert.

belangrijkste waarde Hallo Hallo FOR JSON-component is dat Hiermee kunt u complexe hiërarchische gegevens worden geretourneerd uit de database die is geformatteerd als geneste JSON-objecten of -matrices. Hallo voorbeeld ziet u hoe tooinclude Orders die deel uitmaken van de klant toohello als een geneste matrix van Orders te volgen:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

In plaats van het verzenden van gegevens van de klant tooget afzonderlijke query's en klik vervolgens op toofetch een lijst met verwante Orders, kunt u alle benodigde Hallo-gegevens met een enkele query opvragen, zoals wordt weergegeven in de volgende voorbeelduitvoer Hallo:

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

## <a name="working-with-json-data"></a>Werken met JSON-gegevens
Als u geen strikt gestructureerde gegevens als u complexe onderliggende objecten, matrices of hiërarchische gegevens hebt, of als uw gegevensstructuren gedurende een bepaalde periode evolueren, Hallo JSON-indeling u toorepresent helpen kan elke complexe gegevensstructuur.

JSON wordt een tekstuele indeling die kan worden gebruikt als andere tekenreekstype in Azure SQL Database. U kunt verzenden of JSON-gegevens opslaan als een standaard NVARCHAR:

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

Hallo JSON-gegevens in dit voorbeeld gebruikt wordt met behulp van het type NVARCHAR(MAX) hello vertegenwoordigd. JSON kan worden ingevoegd in deze tabel of als een argument van Hallo opgeslagen procedure met behulp van standaard Transact-SQL-syntaxis, zoals weergegeven in het volgende voorbeeld Hallo:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Elke client-side taal of de bibliotheek die geschikt is voor tekenreeksgegevens in Azure SQL Database werkt ook met JSON-gegevens. JSON kan worden opgeslagen in een tabel die ondersteuning biedt voor Hallo NVARCHAR type, zoals een tabel geoptimaliseerd voor geheugen of een systeemversietabel. JSON wordt geen eventuele beperkingen in Hallo clientcode of in Hallo databaselaag.

## <a name="querying-json-data"></a>JSON-gegevens opvragen
Als u gegevens die zijn opgemaakt als JSON opgeslagen in Azure SQL-tabellen, kunnen JSON-functies u deze gegevens in een SQL-query.

JSON-functies die beschikbaar in Azure SQL database kunt zijn u gegevens die zijn opgemaakt als JSON als elke andere SQL-gegevenstype behandelen. U kunt eenvoudig waarden ophalen uit JSON-tekst hello en JSON-gegevens in een query gebruiken:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Hallo JSON_VALUE functie haalt een waarde van de JSON-tekst opgeslagen in de kolom Hallo-gegevens. Deze functie gebruikt een JavaScript-achtige pad tooreference een waarde in JSON-tekst tooextract. Hallo uitgepakt waarde kan worden gebruikt in een deel van de SQL-query.

Hallo JSON_QUERY-functie is vergelijkbaar tooJSON_VALUE. In tegenstelling tot JSON_VALUE pakt deze functie complexe onderliggende object zoals matrices of objecten die in JSON-tekst worden geplaatst.

Hallo JSON_MODIFY functie kunt u Hallo-pad van het Hallo-waarde opgeven in Hallo JSON-tekst die moet worden bijgewerkt, evenals een nieuwe waarde die Hallo oude wordt overschreven. Op deze manier kunt u eenvoudig bijwerken JSON-tekst zonder reparsing Hallo volledige structuur.

Aangezien JSON is opgeslagen in een standaardtekst, zijn er geen garanties dat Hallo waarden die zijn opgeslagen in tekstkolommen juist zijn opgemaakt. U kunt controleren tekst opgeslagen in JSON-kolom is correct opgemaakt met behulp van standaard check-beperkingen voor Azure SQL Database en Hallo ISJSON functie:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Als de ingevoerde tekst hello is juist opgemaakt JSON, Hallo ISJSON functie retourneert Hallo waarde 1. Bij elke invoegen of bijwerken van de JSON-kolom, controleert deze beperking of nieuwe tekstwaarde is niet een verkeerd ingedeelde JSON.

## <a name="transforming-json-into-tabular-format"></a>Omzetten van JSON in tabelvorm
Azure SQL Database kunt u verzamelingen JSON in tabelvorm indeling en load of query JSON-gegevens te transformeren.

OPENJSON is een tabelwaarde functie die parseert JSON-tekst, zoekt de client een matrix met JSON-objecten, Hallo-elementen van de matrix Hallo doorlopen en retourneert één rij in Hallo uitvoerresultaat voor elk element van het Hallo-matrix.

![JSON in tabelvorm](./media/sql-database-json-features/image_2.png)

Hallo bovenstaande voorbeeld kunt we opgeven waar toolocate Hallo JSON-matrix die moet worden geopend (in Hallo $. Orders pad), welke kolommen moeten worden geretourneerd als resultaat en waar toofind Hallo JSON-waarden die worden geretourneerd als in de cellen.

We kunnen een JSON-matrix in Hallo transformeren @orders variabele in een set rijen, deze resultaatset analyseren of invoegen van rijen in een standaard tabel:

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
Hallo verzameling orders opgemaakt als een JSON-matrix en die als een parameter toohello opgeslagen procedure kan worden geparseerd en ingevoegd in de tabel Orders hello wordt verstrekt.

## <a name="next-steps"></a>Volgende stappen
toolearn hoe toointegrate JSON in uw toepassing, bekijk deze resources:

* [Blog van TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [MSDN-documentatie](https://msdn.microsoft.com/library/dn921897.aspx)
* [Channel 9 video](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn over diverse scenario's voor het integreren van JSON in uw toepassing hello demo's in deze Zie [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) of vinden van een scenario dat overeenkomt met uw gebruiksvoorbeeld in [JSON blogberichten](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

