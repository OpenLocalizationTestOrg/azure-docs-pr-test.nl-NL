---
title: aaaWhat is Azure SQL Data Warehouse? | Microsoft Docs
description: Gedistribueerde database op ondernemingsniveau die geschikt is voor het verwerken van petabytes aan relationele en niet-relationele gegevens. Dit Hallo branche eerste cloud datawarehouse met vergroten, verkleinen, en onderbreken in seconden.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: bjhubbard
editor: 
ms.assetid: 4006c201-ec71-4982-b8ba-24bba879d7bb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: overview
ms.date: 2/28/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 5fefe40879230f123c2e4a90b9c20a35779cf711
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-sql-data-warehouse"></a>Wat is Azure SQL Data Warehouse?
Azure SQL Data Warehouse is een schaalbare, relationele MMP-clouddatabase (Massively Parallel Processing) die geschikt is voor het verwerken van grote hoeveelheden gegevens. 

SQL Data Warehouse:

* Relationele SQL Server-database Hallo combineert met de mogelijkheden van Azure-cloud scale-out. 
* Maakt het mogelijk opslag los te koppelen van rekenactiviteiten.
* Maakt het uitbreiden, beperken, onderbreken of hervatten van rekenactiviteiten mogelijk. 
* Kan worden geïntegreerd via hello Azure-platform.
* Maakt gebruik van SQL Server Transact-SQL (T-SQL) en hulpprogramma's.
* Voldoet aan diverse juridische en zakelijke beveiligingsvereisten, zoals SOC en ISO.

Dit artikel wordt beschreven Hallo belangrijke functies van SQL Data Warehouse.

## <a name="massively-parallel-processing-architecture"></a>MPP-architectuur (Massively Parallel Processing)
SQL Data Warehouse is een gedistribueerd MPP-databasesysteem (Massively Parallel Processing). Achter de schermen Hallo worden verspreid SQL Data Warehouse uw gegevens over veel niets wordt gedeeld-opslag- en verwerkingseenheden. Hallo-gegevens worden opgeslagen in een Premium lokaal redundante opslaglaag bovenop die dynamisch gekoppelde rekenknooppunten query's uitvoeren. SQL Data Warehouse duurt die een benadering 'verdelen en heersprincipe' toorunning wordt geladen en complexe query's. Aanvragen worden ontvangen door een beheerknooppunt geoptimaliseerd voor distributie en vervolgens doorgegeven tooCompute knooppunten toodo hun werk parallel.

Als u opslag en rekenactiviteiten loskoppelt van elkaar, kan SQL Data Warehouse:

* De beschikbare opslag vergroten of verkleinen, onafhankelijk van de rekencapaciteit.
* De rekencapaciteit vergroten of verkleinen zonder gegevens te verplaatsen.
* De rekencapaciteit onderbreken terwijl gegevens intact blijven en u alleen betaalt voor opslag.
* De rekencapaciteit hervatten tijdens werktijden.

Hallo volgende diagram toont de architectuur Hallo in meer detail.

![Architectuur van SQL Data Warehouse][1]

**Door het beheerknooppunt:** Hallo beheerknooppunt beheert en query's worden geoptimaliseerd. Is het Hallo-front-end met interactie met alle toepassingen en verbindingen. In SQL Data Warehouse Hallo beheerknooppunt door SQL-Database, en verbinding maken met tooit lijkt en dezelfde werkt Hallo. Onder Hallo oppervlak coördineert Hallo beheerknooppunt alle Hallo gegevensverplaatsing en berekeningen vereist toorun parallelle query's op uw gedistribueerde gegevens. Wanneer u een T-SQL-query tooSQL Data Warehouse verzendt, wordt het in Hallo door het beheerknooppunt getransformeerd tot afzonderlijke query's die op elk rekenknooppunt parallel worden uitgevoerd.

**Rekenknooppunten:** hello rekenknooppunten vormen Hallo kracht achter SQL Data Warehouse. Het zijn SQL Databases die uw gegevens opslaan en uw query verwerken. Wanneer u gegevens toevoegt, wordt in SQL Data Warehouse Hallo rijen tooyour Compute nodes distribueert. Hallo Compute nodes zijn Hallo werknemers die Hallo parallelle query's op uw gegevens uitvoeren. Na de verwerking doorgeven ze Hallo resultaten back toohello beheerknooppunt. toofinish hello query, het beheerknooppunt Hallo aggregeert Hallo resultaten en retourneert Hallo eindresultaat.

**Opslag:** uw gegevens worden opgeslagen in Azure-blobopslag. Wanneer de rekenknooppunten communiceren met uw gegevens, deze schrijven en lezen rechtstreeks tooand van blob-opslag. Omdat Azure storage wordt uitgebreid transparant en aanzienlijk, SQL Data Warehouse kunt doen Hallo dezelfde. Omdat reken- en opslagcapaciteit niet van elkaar afhankelijk zijn, kan de opslagcapaciteit in SQL Data Warehouse automatisch los van de rekencapaciteit worden geschaald en omgekeerd. Azure Blob-opslag is ook volledig fouttolerant en zodat Hallo back-up en herstelproces.

**Data Movement Service:** Data Movement Service (DMS) verplaatst gegevens tussen Hallo knooppunten. DMS geeft Hallo Compute-knooppunten toegang toodata ze nodig hebben voor samenvoegingen en aggregaties. DMS is geen Azure-service. Dit is een Windows-service die wordt uitgevoerd naast SQL Database op alle knooppunten van het Hallo. DMS is een achtergrondproces waarmee u niet rechtstreeks aan de slag kunt. Echter, u kunt raadplegen query plannen toosee wanneer DMS-bewerkingen plaatsvinden, aangezien gegevensverplaatsing nodig toorun elke query parallel.

## <a name="optimized-for-data-warehouse-workloads"></a>Geoptimaliseerd voor datawarehouse-workloads
Hallo MPP-methode ondersteund door verschillende gegevensopslag specifieke optimalisaties, met inbegrip van:

* een gedistribueerde queryoptimalisatie en een set complexe statistieken voor alle gegevens. Voor meer informatie over het gebruik van informatie op de gegevensomvang en distributie is Hallo service kunnen toooptimize query's door Hallo kosten van specifieke gedistribueerde querybewerkingen vast te stellen.
* Geavanceerde algoritmen en technieken geïntegreerd in Hallo data movement proces tooefficiently verplaatsen gegevens tussen de computerbronnen als nodig tooperform Hallo query. Deze gegevensverplaatsingsbewerkingen zijn ingebouwd in en alle optimalisaties toohello Data Movement Service gebeurt automatisch.
* Er wordt standaard gebruikgemaakt van geclusterde **kolomopslag**indexen. SQL Data Warehouse opgehaald met behulp van opslag op basis van een kolom, gemiddeld 5 x betere compressie over traditionele rij-opslag en omhoog too10x of meer betere prestaties. Analysequery's waarbij tooscan moeten een groot aantal rijen beter werkt met columnstore-indexen.


## <a name="predictable-and-scalable-performance-with-data-warehouse-units"></a>Voorspelbare en schaalbare prestaties met Data Warehouse Units
SQL Data Warehouse is opgebouwd op basis van vergelijkbare technologieën als die van SQL Database, wat betekent dat gebruikers consistente en voorspelbare prestaties kunnen verwachten voor analytische query's. Gebruikers verwachten toosee prestaties scale lineair als ze toevoegen aan of verwijderen van rekenknooppunten. Toewijzing van resources tooyour SQL Data Warehouse wordt gemeten in Data Warehouse Units (dwu's). Dwu's zijn metingen van het onderliggende bronnen zoals CPU, geheugen, IOP's tooyour SQL Data Warehouse worden toegewezen. Hallo aantal dwu's te verhogen, verhoogt resources en de prestaties. DWU's zorgen met name voor het volgende:

* U zijn kunt tooscale uw datawarehouse zonder dat u over Hallo onderliggende hardware of software.
* U kunt voorspellen prestatieverbeteringen voor DWU-niveau voordat Hallo compute van uw datawarehouse wijzigen.
* Hallo kunnen onderliggende hardware en software van uw exemplaar wijzigen of verplaatsen zonder invloed op prestaties van uw workload.
* Microsoft kan de onderliggende architectuur van Hallo service zonder dat de prestaties van uw workload Hallo Hallo te verbeteren.
* Microsoft kan snel de prestaties verbeteren in SQL Data Warehouse, op een manier die schaalbaar is en evenredig effecten Hallo system.

Data Warehouse Units (DWU's) bieden een maatstaf voor drie metrische gegevens die nauw verband houden met de prestaties van datawarehouses bij een bepaalde workload. Hallo volgende key werkbelasting metrische gegevens schaal Lineair met Hallo dwu's.

**Scan/aggregatie:** een standaarddatawarehousequery waarmee een groot aantal rijen wordt gescand waarop vervolgens een complexe aggregatie wordt uitgevoerd. Dit is een I/O-bewerking waarbij de CPU intensief wordt belast.

**Belasting:** mogelijkheid tooingest gegevens Hallo Hallo brengen. Laadacties worden het beste uitgevoerd met PolyBase van Azure Storage Blobs of Azure Data Lake. Deze waarde is ontworpen toostress netwerk en CPU-aspecten van Hallo-service.

**Maak Table As Select (CTAS):** CTAS Hallo mogelijkheid toocopy wordt een tabel. Dit omvat het lezen van gegevens van opslag, verdelen over Hallo-knooppunten van het Hallo-apparaat en toostorage opnieuw te schrijven. Dit is een bewerking waarbij de CPU, de IO en het netwerk intensief worden belast.

## <a name="built-on-sql-server"></a>Gebouwd op SQL Server
SQL Data Warehouse is gebaseerd op Hallo SQL Server relationele database-engine en bevat veel Hallo-functies die u van een datawarehouse voor ondernemingen verwacht. Als u al T-SQL weet, is het eenvoudig tootransfer uw kennis tooSQL Data Warehouse. Hiermee wordt aangegeven of u nu een ervaren of maar net begint, Hallo voorbeelden in Hallo documentatie kunt u. U nadenken over het algemeen over Hallo manier we de elementen van de taal van SQL Data Warehouse Hallo als volgt hebt gebouwd:

* SQL Data Warehouse gebruikt T-SQL-syntaxis voor veel bewerkingen. Deze biedt ook ondersteuning voor diverse traditionele SQL-constructs, zoals opgeslagen procedures, door de gebruiker gedefinieerde functies, tabelpartities, indexen en sorteringen.
* SQL Data Warehouse bevat ook een aantal nieuwere functies van SQL Server, zoals geclusterde **kolomopslag**indexen, PolyBase-integratie en gegevensauditing (inclusief beoordeling van bedreigingen).
* Bepaalde T-SQL-taal-elementen die minder gangbaar zijn voor workloads van gegevensopslag, of nieuwere tooSQL Server, zijn mogelijk niet beschikbaar. Zie voor meer informatie, Hallo [migratiedocumentatie][Migration documentation].

U kunt een oplossing die past bij de gegevensbehoeften van uw kunt ontwikkelen met hello Transact-SQL- en functie overeenkomsten tussen de SQL Server, SQL Data Warehouse, SQL-Database en Analytics Platform System. U kunt ervoor kiezen waar tookeep uw gegevens, op basis van prestaties, beveiliging en schaal en overdracht van gegevens als nodig tussen verschillende systemen.

## <a name="data-protection"></a>Gegevensbeveiliging
Alle SQL Data Warehouse-gegevens worden opgeslagen in Azure Premium-opslag met lokaal redundante opslag. Meerdere synchrone kopieën van Hallo gegevens worden onderhouden in Hallo lokale gegevens center tooguarantee transparante gegevensbeveiliging tegen gelokaliseerde fouten. Bovendien maakt SQL Data Warehouse automatisch en regelmatig back-ups van uw actieve (niet-onderbroken) databases met Azure Storage-momentopnamen. toolearn informatie over het back-up en herstel werkt, Zie Hallo [overzicht van back-up en herstel][Backup and restore overview].

## <a name="integrated-with-microsoft-tools"></a>Geïntegreerd met Microsoft-hulpprogramma's
SQL Data Warehouse ook worden geïntegreerd veel van Hallo-hulpprogramma's die gebruikers al bekend met wellicht SQL-Server. Tot deze hulpmiddelen behoren onder meer:

**Traditionele SQL Server-hulpprogramma's:** SQL Data Warehouse is volledig geïntegreerd met SQL Server Analysis Services, Integration Services en Reporting Services.

**Cloudhulpprogramma's:** SQL Data Warehouse kan worden geïntegreerd in verschillende services in Azure, waaronder Data Factory, Stream Analytics, Machine Learning en Power BI. Voor een volledig overzicht raadpleegt u [Overzicht met geïntegreerde hulpmiddelen][Integrated tools overview].

**Hulpprogramma's van derden:** veel externe leveranciers hebben de integratie van hun hulpprogramma's met SQL Data Warehouse laten certificeren. Zie voor een volledige lijst [SQL Data Warehouse-oplossingspartners][SQL Data Warehouse solution partners].

## <a name="hybrid-data-sources-scenarios"></a>Hybride scenario's met gegevensbronnen
Polybase kunt u tooleverage uw gegevens uit verschillende bronnen met behulp van bekende T-SQL-opdrachten. Met Polybase kunt u de niet-relationele gegevens tooquery ondergebracht in Azure Blob-opslag, hoewel dit een gewone tabellen. Gebruik Polybase tooquery niet-relationele gegevens of niet-relationele gegevens tooimport in SQL Data Warehouse.

* PolyBase gebruikt externe tabellen tooaccess niet-relationele gegevens. Hallo tabeldefinities worden opgeslagen in SQL Data Warehouse en u er toegang toe met behulp van SQL en hulpprogramma's zoals u zou toegang tot normale relationele gegevens.
* Polybase is agnostisch qua integratie. Deze zichtbaar gemaakt Hallo dezelfde functies en functionaliteit tooall Hallo bronnen die wordt ondersteund. Hallo-gegevens gelezen door Polybase kunnen zich in verschillende indelingen, waaronder bestanden met scheidingstekens of ORC-bestanden.
* PolyBase kan worden gebruikt tooaccess blob-opslag die ook wordt gebruikt als opslag voor een HDInsight-cluster. Dit biedt u toegang tot toohello dezelfde gegevens met relationele en niet-relationele hulpprogramma's.

## <a name="sla"></a>SLA
SQL Data Warehouse biedt een SLA (Service Level Agreement, serviceovereenkomst) op productniveau als onderdeel van de Microsoft Online Services SLA. Ga voor meer informatie naar [SLA voor SQL Data Warehouse][SLA for SQL Data Warehouse]. Voor informatie over alle andere producten SLA vindt u Hallo [Service Level Agreements] Azure pagina of deze downloaden op Hallo [Volume Licensing] [ Volume Licensing] pagina. 

## <a name="next-steps"></a>Volgende stappen
Nu u weet wat SQL Data Warehouse, kunt u nagaan hoe tooquickly [maken van een SQL Data Warehouse] [ create a SQL Data Warehouse] en [voorbeeldgegevens laden][load sample data]. Als u nieuwe tooAzure bent, vindt u Hallo [Azure verklarende woordenlijst] [ Azure glossary] handig als u nieuwe terminologie optreden. U kunt ook enkele andere SQL Data Warehouse-resources bekijken.  

* [Succesverhalen van klanten]
* [Blogs]
* [Functieverzoeken]
* [Video's]
* [Teamblogs met adviezen voor klanten]
* [Ondersteuningsticket maken]
* [MSDN-forum]
* [Stack Overflow-forum]
* [Twitter]

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Ondersteuningsticket maken]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Succesverhalen van klanten]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Teamblogs met adviezen voor klanten]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Functieverzoeken]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN-forum]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Stack Overflow-forum]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Video's]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/en-us/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[Service Level Agreements]: https://azure.microsoft.com/en-us/support/legal/sla/
