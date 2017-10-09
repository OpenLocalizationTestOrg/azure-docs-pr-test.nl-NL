---
title: 'Migreren: Datawarehouse migratiehulpprogramma | Microsoft Docs'
description: TooSQL Data Warehouse migreren.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a>Datawarehouse migratiehulpprogramma (Preview)
> [!div class="op_single_selector"]
> * [Migratiehulpprogramma voor downloaden][Download Migration Utility]
> 
> 

Hallo-hulpprogramma voor migratie datawarehouse is dat een hulpprogramma ontworpen toomigrate schema en de gegevens uit SQL Server en Azure SQL Database tooAzure SQL Data Warehouse. Tijdens de migratie schema Hallo hulpprogramma automatisch Hallo bijbehorende schema van bron toodestination toegewezen. Nadat het Hallo-schema is gemigreerd, biedt extra Hallo Hallo optie toomove gegevens met automatisch gegenereerde scripts.

Bovendien gestroomlijnde tooschema en -gegevensmigratie, dit hulpprogramma biedt u de optie toogenerate compatibiliteitsrapporten geven een overzicht van compatibiliteitsproblemen tussen Hallo doel- en -exemplaren waarvoor geen Hallo migratie.

## <a name="get-started"></a>Aan de slag
Als een vereiste voor installatie moet u Hallo BCP opdrachtregelprogramma toorun migratiescripts en Office tooview Hallo compatibiliteitsrapport. Na het starten van Hallo worden uitvoerbaar bestand dat u wordt gedownload van vraag tooaccept standaard gebruiksrechtovereenkomst voordat het Hallo tool wordt geïnstalleerd.

Bovendien toorun Hallo migratie Utiliy, u wordt moet Hallo een volgende machtigingen op Hallo database dat u op zoek bent toomigrate: CREATE DATABASE, ALTER ANY DATABASE of een WEERGAVEDEFINITIE.

### <a name="launching-hello-tool-and-connecting"></a>Hallo hulpprogramma starten en verbinding te maken
Hallo-hulpprogramma starten door te klikken op het bureaubladpictogram Hallo die wordt weergegeven na installeren. Bij het openen van Hallo hulpprogramma, wordt u gevraagd met een eerste verbindingspagina u de bron- en doel voor Hallo-hulpprogramma voor migratie kunt. Op dit moment ondersteunen we SQL Server en Azure SQL Database als bronnen en SQL Data Warehouse als doel. Nadat u dit hebt u gevraagd tooconnect tooyour bronserver vult servernaam en verifiëren en vervolgens te klikken op 'Connect'.

Hallo-hulpprogramma wordt een lijst met databases die aanwezig in het Hallo-server waarmee u bent zijn met verbonden weergegeven als de verificatie is gelukt. Hallo migratie kunt u beginnen door een database die u graag toomigrate en vervolgens te klikken op 'Migreren geselecteerd' te selecteren.

## <a name="migration-report"></a>Migratierapport
Een rapport met overzicht van alle object compatibiliteitsproblemen 'Databasecompatibiliteit controleren' selecteren in Hallo hulpprogramma wordt gegenereerd in Hallo-database die u hebt aangevraagd toomigrate. Een uitgebreidere lijst van een aantal SQL Server-functionaliteit is niet aanwezig in SQL Data Warehouse Hallo vindt u in onze [migratiedocumentatie][migration documentation]. Nadat het Hallo-rapport is gegenereerd kunt u zich kunt toosave en open Hallo-rapport in Excel.

Houd er rekening mee dat bij het genereren van Hallo migratie schema, de meeste problemen geïdentificeerd als 'Object' in order tooallow onmiddellijke migratie van die gegevens moeten worden aangepast. Controleer Hallo wijzigingen tooensure u niet wilt dat extra aanpassingen toomake alvorens Hallo schema toe te passen.

## <a name="migrate-schema"></a>Schema migreren
Nadat u verbinding maakt, selecteren 'Migreren Schema' wordt een schema migratiescript genereren voor Hallo geselecteerde tabellen. Deze structuur script poorten Hallo van Hallo-tabel incompatibele gegevens typen toomore compatibel formulieren wordt toegewezen, en maakt beveiligingsreferenties en het schema als dit wordt aangegeven door de gebruiker Hallo in Hallo migratie-instellingen. Deze code kan worden uitgevoerd tegen Hallo gericht SQL Data Warehouse-exemplaar, tooa-bestand hebt opgeslagen, tooyour Klembord gekopieerd of zelfs bewerkt in-line alvorens verdere actie te ondernemen.  

Als opgemerkt, wanneer schema revisie Hallo migratie die Hallo verandert hulpprogramma heeft doorgevoerd in de volgorde tooensure die dat u volledig deze begrijpt.  

## <a name="migrate-data"></a>Gegevens migreren
Door te klikken op Hallo 'Data migreren' optie kunt u BCP-scripts die uw eerste tooflat gegevensbestanden op uw server gaat genereren en vervolgens rechtstreeks in uw SQL Data Warehouse. Het is raadzaam om dit proces voor het verplaatsen van kleine hoeveelheden gegevens, en als nieuwe pogingen zijn niet ingebouwde en kan mislukken als er een verlies van Hallo netwerkverbinding. In volgorde toorun dit, moet u toohave Hallo opdrachtregelprogramma BCP geïnstalleerd en Hallo-schema voor Hallo gegevens, moet al zijn gemaakt.

Nadat u hebt ingevuld Hallo uitvoerparameters hierboven u gewoon moet tooclick migratie uitvoeren en een set van twee pakketten gegenereerd tooyour opgegeven locatie. Hallo-exportbestand in volgorde tooexport gegevens van de migratiebron voor uw uitvoeren naar platte bestanden en Voer Hallo-bestand importeren in volgorde tooimport uw gegevens in SQL Data Warehouse.

## <a name="next-steps"></a>Volgende stappen
Nu dat u sommige gegevens hebt gemigreerd, bekijk hoe te[ontwikkelen][develop].

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
