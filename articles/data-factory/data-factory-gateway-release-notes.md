---
title: Opmerkingen bij de aaaRelease van Data Management Gateway | Microsoft Docs
description: Releaseopmerkingen voor Data Management Gateway-loop
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a>Releaseopmerkingen voor Data Management Gateway
Een van de uitdagingen Hallo voor moderne gegevensintegratie is toomove gegevens tooand van lokale toocloud. Data Factory maakt deze integratie met Data Management Gateway, een agent wordt dat u lokale tooenable hybride gegevensverplaatsing kunt installeren.

Zie de volgende artikelen voor meer informatie over Data Management Gateway Hallo en hoe toouse het:

*  [Gegevensbeheergateway](data-factory-data-management-gateway.md)
*  [Gegevens verplaatsen tussen on-premises en in de cloud met Azure Data Factory](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a>HUIDIGE VERSIE (2.10.6347.7)

### <a name="enhancements-"></a>Verbeteringen-
- U kunt toevoegen DNS-vermeldingen toowhitelist servicebus in plaats van door alle Azure-IP-adressen van uw firewall (indien nodig). U kunt de respectieve DNS-vermelding vinden op Azure-portal (Data Factory -> 'Maken en implementeren' -> 'Gateways'-'serviceUrls' (in JSON) >
- HDFS-connector ondersteunt nu zelfondertekend certificaat met openbare doordat u SSL-validatie overslaat.
- Vaste: Probleem met de gateway tijdens het bijwerken (vervaldatum tooclock tijdverschil)



## <a name="earlier-versions"></a>Eerdere versies

## <a name="2963132"></a>2.9.6313.2
### <a name="enhancements-"></a>Verbeteringen-
-   U kunt toevoegen DNS-vermeldingen toowhitelist Service Bus in plaats van door alle Azure-IP-adressen van uw firewall (indien nodig). Hier voor meer informatie.
-   U kunt nu gegevens uit een enkele blok-blob van too4.75 TB, namelijk Hallo maximaal ondersteunde grootte van blok-blob kopiëren. (eerdere limiet was 195 GB).
-   Vaste: Onvoldoende geheugen-probleem tijdens ritsen enkele kleine bestanden tijdens de kopieeractiviteit.
-   Vaste: Index valt buiten het bereik probleem tijdens het kopiëren van het Document DB tooan on-premises SQL Server met de functie idempotency.
-   Vaste: SQL-script voor opschoning werkt niet met lokale SQL Server van de Wizard kopiëren.
-   Vaste: Kolomnaam met ruimte aan Hallo einde werkt niet in de kopieerbewerking.

## <a name="28662833"></a>2.8.66283.3
### <a name="enhancements-"></a>Verbeteringen-
- Vaste: Probleem met de referenties op de computer opnieuw is opgestart gateway ontbreekt.
- Vaste: Probleem met de registratie tijdens gateway herstellen met behulp van een back-upbestand.


## <a name="2762401"></a>2.7.6240.1
### <a name="enhancements-"></a>Verbeteringen-
- Vaste: Onjuiste leesbewerking van de decimale null-waarde van Oracle als bron.

## <a name="2661922"></a>2.6.6192.2
### <a name="whats-new"></a>Nieuwe functies
- Klanten kunnen feedback op gateway registreren ervaring.
- Ondersteuning voor een nieuwe compressie-indeling: ZIP (Deflate)

### <a name="enhancements-"></a>Verbeteringen-
- Prestatieverbeteringen voor Oracle opvangen, HDFS-bron.
- Fout-oplossing voor gateway automatisch bijwerken, gateway parallelle verwerking van capaciteit.


## <a name="2561641"></a>2.5.6164.1
### <a name="enhancements"></a>Verbeteringen
- Betere en krachtigere Gateway registratie ervaring-nu kunt u de voortgangsstatus tijdens Hallo Gateway registratieproces, waardoor Hallo registratie ervaren responsievere bijhouden.
- Verbetering van de Gateway herstellen proces - u kunt nog steeds gateway herstellen, zelfs als er geen back-upbestand van Hallo gateway met deze update. Dit moet u tooreset gekoppelde Service referenties in Portal.
- Fout te herstellen.

## <a name="2461511"></a>2.4.6151.1

### <a name="whats-new"></a>Nieuwe functies

- U kunt nu de referenties voor gegevensbron lokaal opslaan. Hallo-referenties zijn versleuteld. referenties voor gegevensbron Hallo kunnen worden hersteld en teruggezet met behulp van back-upbestand Hallo die kan worden geëxporteerd uit een bestaande Gateway, alle lokale Hallo.

### <a name="enhancements-"></a>Verbeteringen-

- Betere en krachtigere Gateway registratie ervaring.
- Ondersteuning voor automatische detectie van QuoteChar configuratie voor tekst zonder opmaak in de wizard kopiëren en Hallo verbeteren de algemene indeling nauwkeurigheid van de detectie.

## <a name="2361002"></a>2.3.6100.2

- Ondersteuning voor firstRowAsHeader en SkipLineCount automatische detectie in de wizard kopiëren voor tekstbestanden in on-premises bestandssysteem en HDFS.
- Hallo stabiliteit van de netwerkverbinding tussen de gateway en Service Bus verbeteren
- Een aantal problemen opgelost


## <a name="2260721"></a>2.2.6072.1

*  Ondersteunt het instellen van HTTP-proxy voor het gebruik van de gateway Hallo Hallo Gateway Configuration Manager. Als geconfigureerd, zijn Azure Blob, Azure Table Azure Data Lake en Document DB toegankelijk via HTTP-proxy.
*  Ondersteunt header verwerking voor TextFormat bij het kopiëren van gegevens uit / tooAzure Blob, Azure Data Lake Store on-premises bestandssysteem en lokale HDFS.
*  Ondersteunt het kopiëren van gegevens van toevoeg-blobs en pagina-Blob samen met de Hallo al ondersteund blok-Blob.
*  Introduceert een nieuwe gatewaystatus **Online (beperkt)**, wat aangeeft dat de belangrijkste functionaliteit van die Hallo van Hallo gateway werkt, behalve Hallo interactieve bewerking ondersteuning voor de Wizard kopiëren.
*  Hallo robuustheid van gateway registreren met behulp van de registratiesleutel verbetert.

## <a name="216040"></a>2.1.6040.

*  DB2-stuurprogramma is nu opgenomen in Hallo gateway-installatiepakket. U hoeft geen tooinstall deze afzonderlijk.
*  DB2-stuurprogramma ondersteunt nu z-/ OS en DB2 voor ik (AS / 400) samen met de Hallo platformen die al worden ondersteund (Linux-, Unix- en Windows).
*  Ondersteunt het gebruik van Azure DB die Cosmos als een bron of bestemming voor on-premises gegevensopslagexemplaren
*  Ondersteunt het kopiëren van gegevens uit/toocold/hot blob-opslag samen met de Hallo al ondersteund algemeen opslagaccount.
*  Hiermee kunt u tooconnect tooon-premises SQL Server via de gateway met machtigingen voor externe aanmelding.  

## <a name="2060131"></a>2.0.6013.1

*  Hallo taalcultuur/toobe die tijdens de handmatige installatie door een gateway gebruikt, kunt u selecteren.

*  Wanneer de gateway werkt niet zoals verwacht, kunt u toosend gateway-logboeken van de afgelopen zeven dagen tooMicrosoft toofacilitate probleemoplossing van Hallo probleem. Als de gateway is niet verbonden toohello-cloudservice, kunt u kiezen toosave en archiveren van gateway-Logboeken.  

*  Verbeteringen in de gebruikersinterface voor gateway configuration manager:

    *  Status van gateway meer zichtbaar maken op het tabblad Hallo-start.

    *  Ingedeeld en vereenvoudigd besturingselementen.

    *  U kunt gegevens kopiëren van een opslagruimte met Hallo [voorbeeldfunctie code gratis exemplaar](data-factory-copy-data-wizard-tutorial.md). Zie [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) voor meer informatie over deze functie in het algemeen.
*  U kunt Data Management Gateway tooingress gegevens direct vanuit een on-premises SQL Server database in Azure Machine Learning.

*  Verbeterde prestaties

    * De prestaties weergeven/Preview-schemaversie op basis van SQL Server in code gratis exemplaar voorbeeldfunctie verbeteren.

## <a name="11259531"></a>1.12.5953.1

*  Oplossingen voor problemen

## <a name="11159181"></a>1.11.5918.1

*  Maximale grootte van het logboek voor systeemgebeurtenissen Hallo-gateway is verhoogd van 1 MB too40 MB.

*  Een dialoogvenster Beveiligingswaarschuwing wordt weergegeven als een herstart nodig is tijdens de gateway automatisch bijwerken. U kunt toorestart rechts vervolgens of hoger.

*  Als automatische updates is mislukt, probeert installatieprogramma van de gateway opnieuw automatische updates drie keer op maximum.

*  Verbeterde prestaties

    * De prestaties voor het laden van grote tabellen van de lokale server in een scenario zonder code kopiëren verbeteren.

*  Oplossingen voor problemen

## <a name="11058921"></a>1.10.5892.1

*  Verbeterde prestaties

*  Oplossingen voor problemen

## <a name="1958652"></a>1.9.5865.2

*  Nul mogelijkheid touch automatische update
*  Pictogram in systeemvak voor nieuwe met statusindicatoren gateway
*  De mogelijkheid te 'bijwerken nu' Hallo-client
*  Tijd van de mogelijkheid tooset update plannen
*  PowerShell-script voor het uitschakelen van automatische updates in-of uitschakelen
*  Ondersteuning voor JSON-indeling  
*  Verbeterde prestaties
*  Oplossingen voor problemen

## <a name="1858221"></a>1.8.5822.1

*  Probleemoplossing-ervaring te verbeteren
*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1757951"></a>1.7.5795.1

*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1757641"></a>1.7.5764.1

*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1657351"></a>1.6.5735.1

*  Ondersteuning voor on-premises HDFS bron/Sink
*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1656961"></a>1.6.5696.1

*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1656761"></a>1.6.5676.1

*  Diagnostische hulpprogramma's voor ondersteuning in Configuration Manager
*  De tabelkolommen ondersteuning voor gegevensbronnen voor Azure Data Factory in tabelvorm
*  Ondersteuning voor SQL DW voor Azure Data Factory
*  Reclusive in BlobSource en FileSource ondersteuning voor Azure Data Factory
*  Ondersteuning voor CopyBehavior – MergeFiles PreserveHierarchy en FlattenHierarchy in BlobSink en FileSink met binaire kopie voor Azure Data Factory
*  Ondersteuning voor Kopieeractiviteit rapportage voor Azure Data Factory
*  Ondersteuning voor bron connectiviteit gegevensvalidatie voor Azure Data Factory
*  Oplossingen voor problemen

### <a name="1656721"></a>1.6.5672.1

*  Naam van de tabel ondersteuning voor ODBC-gegevensbron voor Azure Data Factory
*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1656581"></a>1.6.5658.1

*  Ondersteuningsbestand van de Sink voor Azure Data Factory
*  Ondersteuning voor het behouden van hiërarchie in binaire kopie voor Azure Data Factory
*  Kopiëren activiteit Idempotency ondersteuning voor Azure Data Factory
*  Oplossingen voor problemen

### <a name="1656401"></a>1.6.5640.1

*  Ondersteuning voor 3 meer gegevensbronnen voor Azure Data Factory (ODBC, OData, HDFS)
*  Aanhalingsteken in CSV-parser ondersteuning voor Azure Data Factory
*  Compressieondersteuning (BZip2)
*  Oplossingen voor problemen

### <a name="1556121"></a>1.5.5612.1

*  Ondersteuning voor relationele databases van vijf voor Azure Data Factory (MySQL, PostgreSQL DB2, Teradata en Sybase)
*  Compressieondersteuning (Gzip en Deflate)
*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1455491"></a>1.4.5549.1

*  Oracle data source-ondersteuning voor Azure Data Factory toevoegen
*  Verbeterde prestaties
*  Oplossingen voor problemen

### <a name="1454921"></a>1.4.5492.1

*  Unified binair die ondersteuning biedt voor zowel Microsoft Azure Data Factory als Power BI voor Office 365-services
*  Verfijnen Hallo Configuratiegebruikersinterface en registratie-proces
*  Azure Data Factory – Azure inkomende en uitgaande ondersteuning voor SQL Server-gegevensbron

### <a name="1253031"></a>1.2.5303.1

*  Los time-out probleem toosupport meer tijdrovend gegevensbronverbindingen.

### <a name="1155268"></a>1.1.5526.8

*  .NET Framework 4.5.1 is vereist als een vereiste tijdens de installatie.

### <a name="1051442"></a>1.0.5144.2

*  Er zijn geen wijzigingen die invloed hebben op Azure Data Factory-scenario's.
