---
title: aaaLearn over de werking van Azure SQL Data Warehouse | Microsoft Docs
description: 'In SQL Data Warehouse kunt u de rekencapaciteit naar wens vergroten, verkleinen of onderbreken door het aantal DWU''s (Data Warehouse Units) aan te passen met een schuifregelaar. In dit artikel wordt uitgelegd Hallo datawarehouse-metrieken en hun relatie tooDWUs. '
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: cadffa9c-589d-4db7-888a-1f202a753bc5
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 8be5ff6b14ab907e2b0a7eb55e0e2f4139aca8b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-workload"></a>Datawarehouse-workload
Een datawarehouse-workload verwijst tooall van Hallo-bewerkingen die de workload van een datawarehouse. Hallo datawarehouse-workload omvat Hallo hele proces van het laden van gegevens in Hallo warehouse, uitvoeren van analyses en rapportage over Hallo-datawarehouse, het beheren van gegevens in het datawarehouse Hallo en exporteren van gegevens uit het datawarehouse Hallo. Hallo zijn omvang en complexiteit van deze onderdelen vaak evenredig met Hallo ontwikkelingsniveau van Hallo datawarehouse.

## <a name="new-toodata-warehousing"></a>Nieuwe toodata datawarehousing?
Een datawarehouse is een verzameling van gegevens die worden geladen uit een of meer gegevens gegevensbronnen en gebruikte tooperform is business intelligence-taken zoals rapportages en analyses.

Datawarehouses worden gekenmerkt door query's die een groter aantal rijen of gegevensbereiken wordt gescand en relatief veel resultaten voor de toepassing hello van analyse en rapportage mogelijk geretourneerd. Bij datawarehouses worden meestal ook relatief veel gegevens geladen in plaats van ingevoegd, bijgewerkt of verwijderd.

* Een datawarehouse werkt het beste als Hallo gegevens worden opgeslagen op een manier die query's die tooscan groot aantal rijen of grote gegevensreeksen moeten worden geoptimaliseerd. Deze manier van scannen werkt het beste als Hallo-gegevens worden opgeslagen en worden doorzocht per kolom in plaats van per rij.

> [!NOTE]
> Hallo in-memory columnstore-index, kolomopslagindex, biedt tot de betere compressie too10x en 100 keer betere prestaties dan traditionele binaire structuren voor query's voor rapportage en analyse. We beschouwen kolomopslagindexen als Hallo standaard voor het opslaan en scannen van grote hoeveelheden gegevens in een datawarehouse.
> 
> 

* Aan een datawarehouse worden andere eisen gesteld dan aan een systeem dat is geoptimaliseerd voor onlinetransactieverwerking (OLTP, Online Transaction Processing). Hallo OLTP-systeem heeft veel invoegen, bijwerken en verwijderen van bewerkingen. Deze bewerkingen wordt gezocht toospecific rijen in Hallo tabel. Tabelzoekopdrachten werken het beste als Hallo gegevens worden opgeslagen op een manier per rij. Hallo-gegevens kunnen worden gesorteerd en snel doorzocht volgens een Verdeel en heersstrategie die ook wel een binaire-structuur- of btree-zoekopdracht.

## <a name="data-loading"></a>Gegevens laden
Gegevens laden is een belangrijk onderdeel van de datawarehouse-workload Hallo. Bedrijven hebben meestal een bezet OLTP-systeem bijhouden van wijzigingen in de loop Hallo dag wanneer klanten zakelijke transacties genereren. Regelmatig Hallo transacties vaak 's nachts tijdens een onderhoudsvenster, kennis worden verplaatst of gekopieerd toohello datawarehouse. Nadat gegevens Hallo Hallo-datawarehouse is, kunnen analisten analyses uitvoeren en zakelijke beslissingen op Hallo gegevens.

* Hallo-proces voor het laden is traditioneel ETL aangeroepen voor uitpakken, transformeren en laden. Gegevens moeten gewoonlijk toobe getransformeerd zodat deze consistent met andere gegevens in het datawarehouse Hallo. Voorheen gebruikten meestal bedrijven specifieke ETL-servers tooperform Hallo transformaties. U kunt nu met dergelijke snel massively parallelle processing eerst gegevens laden in SQL Data Warehouse en vervolgens Hallo-transformaties uitvoeren. Dit proces heet extraheren, laden en transformeren (ELT) en wordt een nieuwe norm voor datawarehouse-workload Hallo.

> [!NOTE]
> Met SQL Server 2016 kunt u nu in realtime analyses uitvoeren op een OLTP-tabel. Dit niet Hallo noodzakelijk voor een datawarehouse toostore en analyseren van gegevens biedt, maar een manier tooperform analyse in realtime.
> 
> 

### <a name="reporting-and-analysis-queries"></a>Query's voor rapportage en analyse
Query's voor rapportage en analyse worden vaak onderverdeeld in kleine, middelgrote en grote query's op basis van een aantal criteria. Meestal gebeurt dit op basis van tijd. In de meeste datawarehouses bestaat de workload uit een combinatie van kort- en langlopende query's. In elk geval is het belangrijk toodetermine deze combinatie en toodetermine de frequentie (elk uur, dagelijks, einde van de maand, kwartaal, enzovoort). Het is belangrijk toounderstand die Hallo gemengde query werkbelasting, samen met de gelijktijdigheid van taken, potentiële klanten tooproper capaciteitsplanning voor een datawarehouse.

* Plannen van capaciteit kan erg ingewikkeld zijn voor een werkbelasting gemengde query's met name als er een lange lead tijd tooadd capaciteit toohello datawarehouse. SQL Data Warehouse verdwijnt Hallo urgentie van de capaciteitsplanning van, omdat u kunt vergroten of verkleinen van rekencapaciteit op elk gewenst moment en de opslag en rekencapaciteit afzonderlijk kunnen worden aangepast.

### <a name="data-management"></a>Gegevensbeheer
Het beheren van gegevens is belangrijk, vooral wanneer u weet dat onvoldoende schijfruimte in Hallo nabije toekomst kan worden uitgevoerd. Hallo gegevens datawarehouses gewoonlijk ingedeeld in logische bereiken, die worden opgeslagen als partities in een tabel. Alle producten op basis van SQL Server kunnen u partities in en uit Hallo tabel verplaatsen. Deze partitie kunt u oudere gegevens tooless dure opslag verplaatsen en Hallo meest recente gegevens beschikbaar houden voor online-opslag.

* Kolomopslagindexen bieden ondersteuning voor gepartitioneerde tabellen. Bij kolomopslagindexen worden gepartitioneerde tabellen gebruikt voor het beheren en archiveren van gegevens. Bij tabellen die per rij zijn opgeslagen, spelen partities een grotere rol in de prestaties van query's.  
* PolyBase speelt een belangrijke rol bij het beheren van gegevens. Met PolyBase hebt Hallo optie tooarchive oudere gegevens tooHadoop of Azure blob-opslag.  Dit biedt veel mogelijkheden omdat Hallo gegevens nog steeds online.  Het duurt langer tooretrieve gegevens uit Hadoop, maar Hallo langere ophaaltijd kan bieden, opwegen tegen de opslagkosten Hallo.

### <a name="exporting-data"></a>Gegevens exporteren
Eenzijdige toomake gegevens beschikbaar voor rapporten en analyses zijn toosend gegevens van Hallo datawarehouse tooservers toegewezen voor het uitvoeren van rapporten en analyses. Deze servers worden datamarts genoemd. U kunt bijvoorbeeld rapportgegevens vooraf verwerken en vervolgens het exporteren van gegevens datawarehouse toomany beheerservers Hallo wereld Hallo, toomake deze grote schaal beschikbaar voor klanten en analisten.

* Voor het genereren van rapporten, elke nacht kon u alleen-lezen rapportageservers met een momentopname van de dagelijkse hoeveelheden Hallo vullen. Hiermee geeft u hogere bandbreedte voor klanten bij Hallo rekencapaciteit is vereist voor het datawarehouse Hallo verlagen. Bijkomend beveiligingsvoordeel toestaan datamarts tooreduce Hallo aantal gebruikers die toegang toohello datawarehouse hebben.
* Voor analyses, kunt u een Analysekubus op Hallo-datawarehouse en analyses uitvoeren op Hallo-datawarehouse, of gegevens vooraf verwerken en dit toohello analysis-server voor verdere analyse te exporteren.

## <a name="next-steps"></a>Volgende stappen
Nu u weet wat SQL Data Warehouse, kunt u nagaan hoe tooquickly [maken van een SQL Data Warehouse] [ create a SQL Data Warehouse] en [voorbeeldgegevens laden][load sample data].

<!--Image references-->

<!--Article references-->
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md

<!--MSDN references-->

<!--Other web references-->
