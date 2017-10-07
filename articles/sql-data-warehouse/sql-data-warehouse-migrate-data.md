---
title: aaaMigrate uw gegevens tooSQL Data Warehouse | Microsoft Docs
description: Tips voor het migreren van uw gegevens tooAzure SQL Data Warehouse om oplossingen te ontwikkelen.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: d78f954a-f54c-4aa4-9040-919bc6414887
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/29/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: fe4c6b7e82094c59c45e06be6da225fee1b707ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data"></a>Uw gegevens migreren
Gegevens kunnen worden verplaatst van verschillende bronnen in uw SQL Data Warehouse met een aantal verschillende hulpprogramma's.  Kopiëren van de ADF, SSIS en bcp kan alle gebruikte tooachieve dit doel. Echter, als Hallo hoeveelheid gegevens toeneemt moet u bedenken Hallo migratieproces in stappen op te splitsen. Hierdoor kunnen u Hallo kans toooptimize elke stap voor prestaties en herstelmogelijkheden tooensure een smooth gegevensmigratie.

Dit artikel wordt eerst Hallo eenvoudige migratiescenario's van ADF kopiëren, SSIS en bcp. Vervolgens uiterlijk enigszins dieper in hoe Hallo migratie kan worden geoptimaliseerd.

## <a name="azure-data-factory-adf-copy"></a>Azure Data Factory (ADF) kopiëren
[Kopiëren van de ADF] [ ADF Copy] maakt deel uit van [Azure Data Factory][Azure Data Factory]. U kunt ADF kopiëren tooexport tooflat gegevensbestanden die zich op de lokale opslag tooremote platte bestanden bewaard in Azure blob-opslag of rechtstreeks in SQL Data Warehouse.

Als uw gegevens in platte bestanden begint, dan u eerst tootransfer moet het storage-blob tooAzure voordat u begint een laden in SQL Data Warehouse. Zodra het Hallo-gegevens worden overgedragen naar Azure blob-opslag kunt u toouse [ADF kopiëren] [ ADF Copy] opnieuw toopush Hallo gegevens in SQL Data Warehouse.

PolyBase biedt ook de optie voor het laden van gegevens Hallo hoge prestaties. Dat betekent dat twee hulpprogramma's voor gebruik in plaats van een. Als u de beste prestaties Hallo moet u PolyBase gebruiken. Als u een ervaring één hulpprogramma wilt (en Hallo gegevens niet enorme zijn) is ADF uw antwoord.


> 
> 

Via het volgende artikel voor een groot toohello HEAD [ADF voorbeelden][ADF samples].

## <a name="integration-services"></a>Integratieservices
Integration Services (SSIS) is een krachtige en flexibele extraheren Transform and Load (ETL) hulpprogramma die ondersteuning biedt voor complexe werkstromen, gegevenstransformatie en verschillende opties voor het laden van gegevens. SSIS toosimply overdracht gegevens tooAzure gebruiken of als onderdeel van een bredere migratie.

> [!NOTE]
> SSIS kunt tooUTF-8 zonder Hallo bytevolgordemarkering in Hallo-bestand exporteren. Dit moet u eerst hello gebruiken kolom onderdeel tooconvert Hallo-tekengegevens in afgeleide tooconfigure Hallo stroom toouse Hallo 65001 UTF-8 code gegevenspagina. Zodra het Hallo-kolommen zijn geconverteerd, schrijf Hallo gegevens toohello plat bestand bestemming adapter ervoor te zorgen dat 65001 ook is geselecteerd als Hallo codetabel voor Hallo-bestand.
> 
> 

SSIS verbindt tooSQL Data Warehouse, net zoals SQL Server-implementatie tooa verbinding wordt gemaakt. Uw verbindingen moet echter toobe met een ADO.NET-Verbindingsbeheer. U moet ook behandelen tooconfigure Hallo 'Gebruik bulksgewijs invoegen indien beschikbaar' instelling toomaximize doorvoer. Raadpleeg toohello [ADO.NET-doeladapter] [ ADO.NET destination adapter] artikel toolearn meer over deze eigenschap

> [!NOTE]
> Verbinding maken met tooAzure SQL Data Warehouse met behulp van OLEDB wordt niet ondersteund.
> 
> 

Bovendien is er altijd Hallo kans dat een pakket mislukt, mogelijk vanwege problemen met toothrottling of netwerk. Ontwerp pakketten zodat ze kunnen worden hervat op Hallo storingspunt, zonder opnieuw uitvoeren, werkt die vóór de fout Hallo is voltooid.

Raadpleeg voor meer informatie Hallo [SSIS-documentatie][SSIS documentation].

## <a name="bcp"></a>bcp
BCP is een opdrachtregelprogramma dat is ontworpen voor een plat bestand gegevens importeren en exporteren. Sommige transformatie kan worden uitgevoerd tijdens het exporteren van gegevens. eenvoudige transformaties tooperform gebruik van een query-tooselect en Hallo gegevens transformeren. Eenmaal geëxporteerd, kunnen Hallo platte bestanden rechtstreeks in Hallo doel Hallo SQL Data Warehouse-database worden geladen.

> [!NOTE]
> Het is vaak een goed idee tooencapsulate Hallo transformaties gebruikt tijdens de gegevens in een weergave in het bronsysteem Hallo exporteren. Dit zorgt ervoor dat Hallo logica wordt bewaard en Hallo-proces herhaald wordt.
> 
> 

Voordelen van bcp zijn:

* Eenvoud. BCP-opdrachten zijn eenvoudige toobuild en uitvoeren
* Het laadproces is opnieuw gestart. Eenmaal geëxporteerde Hallo load mag een onbeperkt aantal keren uitgevoerd

Beperkingen van bcp zijn:

* BCP werkt met gebruikmaking platte bestanden alleen. Deze functie niet samenwerkt met zoals XML- of JSON-bestanden
* Data transformation mogelijkheden zijn beperkt toohello export alleen Faseren en eenvoudige aard
* BCP is niet robuust van aangepast toobe bij het laden van gegevens via internet Hallo. Netwerk instabiliteit kan ertoe leiden dat een fout bij het laden.
* BCP is afhankelijk van Hallo schema aanwezig zijn in Hallo doel database voorafgaande toohello laden

Zie voor meer informatie [bcp tooload gegevens worden gebruikt in SQL Data Warehouse][Use bcp tooload data into SQL Data Warehouse].

## <a name="optimizing-data-migration"></a>Gegevensmigratie optimaliseren
Een migratieproces SQLDW kan worden effectief onderverdeeld in drie afzonderlijke stappen:

1. Het exporteren van de brongegevens
2. Overdracht van gegevens tooAzure
3. In de doeldatabase SQLDW Hallo laden

Elke stap kan worden afzonderlijk geoptimaliseerde toocreate een robuuste, opnieuw gestart en robuuste migratieproces die optimaliseert de prestaties bij elke stap.

## <a name="optimizing-data-load"></a>Optimaliseren laden van gegevens
Kijken naar deze in omgekeerde volgorde voor even; Er is een Hallo snelste manier tooload gegevens met PolyBase. Optimaliseren voor een PolyBase laadproces wordt geplaatst vereisten op de vorige stappen dus is het beste toounderstand dit Hallo vooraf. Ze zijn:

1. Codering van gegevensbestanden
2. Indeling van de gegevensbestanden worden opgeslagen
3. Locatie van gegevensbestanden

### <a name="encoding"></a>Encoding
PolyBase vereist gegevens bestanden toobe UTF-8- of UTF-16FE. 



### <a name="format-of-data-files"></a>Indeling van de gegevensbestanden worden opgeslagen
PolyBase vereist een vaste rijeinde van \n of nieuwe regel aangeeft. Uw gegevensbestanden moeten toothis standaard voldoen. Er zijn geen beperkingen op tekenreeks- of afsluitingen.

Hebt u toodefine voor elke kolom in Hallo-bestand als onderdeel van de externe tabel in PolyBase. Zorg ervoor dat alle geëxporteerde kolommen vereist zijn en dat Hallo typen toohello vereist standaarden voldoen.

Raadpleeg terug toohello [migreren uw schema] artikel voor informatie over de ondersteunde gegevenstypen.

### <a name="location-of-data-files"></a>Locatie van gegevensbestanden
SQL Data Warehouse gebruikt uitsluitend PolyBase tooload gegevens uit Azure Blob Storage. Als gevolg daarvan kan moet Hallo gegevens eerst overgedragen naar de blobopslag.

## <a name="optimizing-data-transfer"></a>Gegevensoverdracht optimaliseren
Een van de traagste onderdelen van de gegevensmigratie Hallo is Hallo overdracht van Hallo gegevens tooAzure. Niet alleen kunt netwerkbandbreedte een probleem kunnen zijn, maar ook netwerk betrouwbaarheid kunt ernstig wordt verstoord uitgevoerd. Standaard is migreren gegevens tooAzure via internet zodat kans op fouten van overdracht plaatsvinden redelijkerwijs waarschijnlijk Hallo Hallo. Deze fouten vereisen echter gegevens toobe opnieuw verzonden geheel of gedeeltelijk.

Gelukkig hebt u verschillende opties tooimprove Hallo snelheid en herstelmogelijkheden van dit proces:

### <a name="expressrouteexpressroute"></a>[ExpressRoute][ExpressRoute]
U kunt met behulp van tooconsider [ExpressRoute] [ ExpressRoute] toospeed up Hallo overdracht. [ExpressRoute] [ ExpressRoute] biedt u met een particuliere verbinding tot stand gebrachte tooAzure zodat Hallo verbinding verloopt niet via Hallo openbare internet. Dit is geen een verplichte stap. Echter het verbeteren van doorvoer wanneer tooAzure gegevens worden gepusht uit een on-premises of CO-locatiefaciliteit.

voordelen van het gebruik van Hallo [ExpressRoute] [ ExpressRoute] zijn:

1. Hogere mate van betrouwbaarheid
2. Snellere netwerksnelheid
3. Lagere netwerklatentie
4. hogere netwerkbeveiliging

[ExpressRoute] [ ExpressRoute] is handig voor een aantal scenario's; niet alleen Hallo migratie.

Geïnteresseerd? Bezoek voor meer informatie en neem prijzen Hallo [ExpressRoute-documentatie][ExpressRoute documentation].

### <a name="azure-import-and-export-service"></a>Azure Import- en Export-Service
Hello is Azure importeren en exporteren Service een overdrachtsproces gegevens is ontworpen voor grote (GB ++) toomassive (TB ++) overdrachten van gegevens in Azure. Dit omvat het schrijven van uw gegevens toodisks en het verzenden tooan Azure-Datacenter. de inhoud van de schijf Hello wordt vervolgens in Azure Storage-Blobs namens jou worden geladen.

Een weergave op hoog niveau van Hallo importeren exportproces is als volgt:

1. Een Azure Blob Storage-container tooreceive Hallo gegevens configureren
2. De opslag van uw gegevens toolocal exporteren
3. Hallo gegevens too3.5 inch SATA III-II harde schijven met Hallo [Azure Import/Export Tool] kopiëren
4. Maken van een Import-taak met hello Azure Import- en exporteren Service bieden Hallo journaal-bestanden die wordt geproduceerd door Hallo [Azure Import/Export Tool]
5. Hallo schijven uw aangewezen Azure-Datacenter verzenden
6. Uw gegevens zijn overgedragen tooyour Azure Blob Storage-container
7. Hallo gegevens laden in SQLDW met PolyBase

### <a name="azcopyazcopy-utility"></a>[AZCopy][AZCopy] hulpprogramma
Hallo [AZCopy][AZCopy] hulpprogramma is een uitstekend hulpprogramma voor het ophalen van de gegevens die binnenkomen in Azure Storage-Blobs. Is bedoeld voor kleine (MB ++) toovery grote (GB ++) gegevensoverdracht. [AZCopy] ook goed robuuste doorvoer ontworpen tooprovide is opgetreden bij het overbrengen van gegevens tooAzure en daarom is een ideale keuze voor Hallo gegevensoverdracht stap. Eenmaal overgebrachte kunt u Hallo-gegevens met PolyBase in SQL Data Warehouse laden. U kunt ook AZCopy opnemen in uw SSIS-pakketten met behulp van een 'Proces uitvoeren'.

toouse AZCopy u eerst toodownload nodig hebt en deze installeren. Er is een [productieversie] [ production version] en een [preview-versie] [ preview version] beschikbaar.

tooupload een bestand van het bestandssysteem u een opdracht zoals Hallo een hieronder moet:

```
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:abc.txt
```

Een samenvatting van het proces op hoog niveau kan worden:

1. Een Azure-opslag-blob-container tooreceive Hallo gegevens configureren
2. De opslag van uw gegevens toolocal exporteren
3. Uw gegevens in Azure Blob Storage-container Hallo AZCopy
4. Hallo gegevens laden in SQL Data Warehouse met PolyBase

Volledige documentatie beschikbaar: [AZCopy][AZCopy].

## <a name="optimizing-data-export"></a>Optimaliseren gegevens exporteren
Bovendien kan toooptimize Hallo exporteren van het Hallo gegevens tooimprove Hallo processen meer ook zoeken door tooensuring dat Hallo export verspreid door PolyBase u toohello-vereisten voldoet.



### <a name="data-compression"></a>Gegevenscompressie
Gzip gecomprimeerde gegevens kan worden gelezen door PolyBase. Als u kunnen toocompress die en de gegevensbestanden toogzip vervolgens minimaliseert u Hallo en de hoeveelheid gegevens die via Hallo netwerk wordt gepusht.

### <a name="multiple-files"></a>Meerdere bestanden
Niet alleen tooimprove snelheid exporteren van grote tabellen in verschillende bestanden op te splitsen helpt, maar ook met overbrengen re-startability en Hallo algehele beheerbaarheid van Hallo gegevens eenmaal in hello Azure blob-opslag. Een van de Hallo veel nice functies van PolyBase is Hiermee worden alle Hallo-bestanden naar de map lezen en behandelen als één tabel. Daarom is het een goed idee tooisolate Hallo-bestanden voor elke tabel in de eigen map.

PolyBase biedt ook ondersteuning voor een functie die bekend als 'recursieve map traversal'. U kunt deze functie toofurther verbeteren Hallo organisatie van de geëxporteerde gegevens tooimprove uw gegevensbeheer.

toolearn meer informatie over het laden van gegevens met PolyBase, Zie [tooload-gegevens met PolyBase in SQL Data Warehouse][Use PolyBase tooload data into SQL Data Warehouse].

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de migratie [migreren van uw oplossing tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse].
Zie voor meer tips voor ontwikkeling, [overzicht voor ontwikkelaars][development overview].

<!--Image references-->

<!--Article references-->
[AZCopy]:../storage/common/storage-use-azcopy.md
[ADF Copy]: ../data-factory/data-factory-data-movement-activities.md 
[ADF samples]: ../data-factory/data-factory-samples.md
[ADF Copy examples]: ../data-factory/data-factory-copy-activity-tutorial-using-visual-studio.md
[development overview]: sql-data-warehouse-overview-develop.md
[Migrate your solution tooSQL Data Warehouse]: sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[Use bcp tooload data into SQL Data Warehouse]: sql-data-warehouse-load-with-bcp.md
[Use PolyBase tooload data into SQL Data Warehouse]: sql-data-warehouse-get-started-load-with-polybase.md


<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory]: http://azure.microsoft.com/services/data-factory/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[ExpressRoute documentation]: http://azure.microsoft.com/documentation/services/expressroute/

[production version]: http://aka.ms/downloadazcopy/
[preview version]: http://aka.ms/downloadazcopypr/
[ADO.NET destination adapter]: https://msdn.microsoft.com/library/bb934041.aspx
[SSIS documentation]: https://msdn.microsoft.com/library/ms141026.aspx
