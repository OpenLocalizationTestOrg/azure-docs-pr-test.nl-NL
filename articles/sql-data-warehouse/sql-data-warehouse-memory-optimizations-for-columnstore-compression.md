---
title: prestaties van aaaImprove columnstore-index in Azure SQL | Microsoft Docs
description: Verminder de geheugenvereisten of Hallo beschikbaar geheugen toomaximize Hallo aantal rijen comprimeren van een columnstore-index in elke rijgroep vergroot.
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Het optimaliseren van rijgroep kwaliteit voor columnstore

Rijgroep kwaliteit wordt bepaald door het aantal rijen in een rijgroep Hallo. Verminder de geheugenvereisten of Hallo beschikbaar geheugen toomaximize Hallo aantal rijen comprimeren van een columnstore-index in elke rijgroep vergroot.  Gebruik deze methoden tooimprove compressie tarieven en prestaties van query's voor columnstore-indexen.

## <a name="why-hello-rowgroup-size-matters"></a>Waarom Hallo rijgroep grootte van belang is
Omdat een columnstore-index een tabel scant door kolomsegmenten van afzonderlijke rowgroups scannen, verbetert het optimaliseren van het aantal rijen in elke rijgroep Hallo de queryprestaties. Wanneer rowgroups hebt een groot aantal rijen, verbetert wat betekent dat er minder tooread gegevens vanaf schijf is gegevenscompressie de.

Zie voor meer informatie over rowgroups [Columnstore-indexen handleiding](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Doelgrootte voor rowgroups
Hallo-doel is voor de beste queryprestaties toomaximize Hallo aantal rijen per rijgroep in een columnstore-index. Een rijgroep kan een maximum van 1.048.576 rijen hebben. De orde toonot Hallo kunt u het maximale aantal rijen per rijgroep hebben. Columnstore-indexen bereiken van goede prestaties wanneer rowgroups ten minste 100.000 rijen hebben.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Rowgroups kunt ophalen afgekapte tijdens compressie

Tijdens het bulksgewijs laden of columnstore-index opnieuw opbouwen, soms er niet voldoende geheugen beschikbaar toocompress die alle rijen die zijn aangewezen voor elke rijgroep Hallo. Wanneer er geheugendruk, trim columnstore-indexen Hallo rijgroep grootten compressie in Hallo columnstore kan wel. 

Wanneer er onvoldoende geheugen toocompress minimaal 10.000 rijen in elke rijgroep, wordt er een fout gegenereerd in SQL Data Warehouse.

Zie voor meer informatie over bulksgewijs laden [bulksgewijs laden in een geclusterde columnstore-index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Hoe toomonitor rijgroep kwaliteit

Er is een DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) die nuttige informatie zoals het aantal rijen in rowgroups en Hallo reden voor bijsnijden beschikbaar worden gesteld als er was u. U kunt de volgende weergave als een handige manier tooquery Hallo deze DMV tooget informatie maken op rijgroep bijsnijden.

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

Hallo trim_reason_desc vertelt of Hallo rijgroep is verkleind (trim_reason_desc = NO_TRIM impliceert er is geen inkorten en rijgroep van optimale kwaliteit is). Hallo vermeld trim oorzaken voortijdige worden ingekort door Hallo rijgroep:
- BULKLOAD: Deze trim reden wordt gebruikt wanneer Hallo binnenkomende batch rijen voor Hallo load minder dan 1 miljoen rijen heeft. Hallo-engine maakt gecomprimeerde Rijgroepen als er zijn meer dan 100.000 rijen worden ingevoegd (als tegengestelde tooinserting in Hallo delta archief) maar sets Hallo trim reden tooBULKLOAD. In dit scenario kunt u uw batch load venster tooaccumulate verhogen meer rijen. Herzie ook uw partitionering schema tooensure is niet te gedetailleerde zoals Rijgroepen niet meerdere grenzen van partities omvatten.
- MEMORY_LIMITATION: toocreate Rijgroepen met een bepaalde hoeveelheid werkende geheugen van 1 miljoen rijen is vereist door Hallo-engine. Wanneer het beschikbare geheugen van Hallo sessie laden is lager dan het Hallo vereist geheugen werkt, krijgen voortijdig Rijgroepen bijgesneden. Hallo volgende secties wordt uitgelegd hoe tooestimate geheugen vereist en meer geheugen toewijzen.
- DICTIONARY_SIZE: Voor deze trim reden geeft aan dat rijgroep bijsnijden omdat er ten minste één kolom met tekenreeksen met een hoge en/of hoge kardinaliteit tekenreeks is opgetreden. Hallo woordenlijst grootte is beperkt too16 MB in het geheugen en wanneer deze limiet is bereikt Hallo rijgroep worden gecomprimeerd. Als u in deze situatie uitvoert, kunt u overwegen isoleren Hallo problematisch kolom in een afzonderlijke tabel.

## <a name="how-tooestimate-memory-requirements"></a>Hoe tooestimate geheugenvereisten

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Hallo vereist Maximumgeheugen toocompress één rijgroep is ongeveer

- 72 MB +
- \#rijen \* \#kolommen \* 8 bytes +
- \#rijen \* \#korte tekenreekskolommen \* 32 bytes +
- \#lange tekenreekskolommen \* 16 MB voor compressiebibliotheek

waar korte tekenreekskolommen gebruiken voor de gegevenstypen string van < = 32 bytes en het gebruik van lange tekenreekskolommen tekenreeks gegevenstypen > 32 bytes.

Lange tekenreeksen zijn gecomprimeerd met een compressiemethode die is ontworpen voor het comprimeren van tekst. Deze compressiemethode gebruikt een *woordenlijst* toostore alleen tekstpatronen. Hallo maximale grootte van een woordenboek is 16 MB. Er is slechts één woordenlijst voor elke kolom lange tekenreeks in Hallo rijgroep.

Zie de video voor een gedetailleerdere beschrijving van de geheugenvereisten columnstore [Azure SQL Data Warehouse schalen: configuratie en richtlijnen](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Manieren tooreduce geheugenvereisten

Gebruik hello technieken tooreduce Hallo geheugenvereisten voor rowgroups comprimeren en columnstore-indexen te volgen.

### <a name="use-fewer-columns"></a>Gebruik minder kolommen
Indien mogelijk ontwerp Hallo tabel met minder kolommen. Wanneer een rijgroep in Hallo columnstore is gecomprimeerd, Hallo columnstore-index elk kolomsegment afzonderlijk gecomprimeerd. Daarom Hallo geheugenvereisten toocompress een rijgroep als Hallo aantal kolommen toeneemt verhogen.


### <a name="use-fewer-string-columns"></a>Gebruik minder tekenreekskolommen
Kolommen van de gegevenstypen string vereisen meer geheugen dan numerieke en datum-gegevenstypen. tooreduce geheugenvereisten, overweeg dan tekenreekskolommen verwijderen uit feitentabellen en ze in kleinere dimensietabellen te plaatsen.

Extra geheugen nodig voor de compressie van de tekenreeks:

- De gegevenstypen String up too32 tekens kunnen 32 aanvullende bytes per waarde vereisen.
- De gegevenstypen String met meer dan 32 tekens zijn gecomprimeerd met behulp van methoden van de woordenlijst.  Elke kolom in Hallo rijgroep kunt vereisen van tooan aanvullende 16 MB toobuild Hallo-woordenlijst.

### <a name="avoid-over-partitioning"></a>Te veel partitioneren voorkomen

Columnstore-indexen maken een of meer rowgroups per partitie. In SQL Data Warehouse groeit het aantal partities Hallo snel omdat Hallo gegevens wordt gedistribueerd en elke distributie is gepartitioneerd. Als Hallo tabel te veel partities heeft, er mogelijk niet voldoende rijen toofill hello rowgroups. Hallo gebrek aan rijen maakt geen geheugendruk tijdens compressie, maar dit leidt toorowgroups die Voer geen controles door Hallo beste columnstore queryprestaties.

Een andere reden tooavoid te veel partitioneren is er een geheugen overhead voor het laden van rijen in een columnstore-index in een gepartitioneerde tabel. Tijdens een werklast kunnen veel partities Hallo binnenkomende rijen, wat in het geheugen worden bewaard totdat elke partitie onvoldoende rijen toobe gecomprimeerd heeft ontvangen. Aanvullende geheugendruk met te veel partities worden gemaakt.

### <a name="simplify-hello-load-query"></a>Hallo load query vereenvoudigen

Hallo database deelt Hallo geheugentoekenning voor een query tussen alle Hallo operators in Hallo-query. Wanneer een load-query complexe sorteerbewerkingen en joins heeft, is Hallo geheugen beschikbaar is voor compressie verminderd.

Ontwerp Hallo load query toofocus alleen voor het laden van Hallo-query. Als u toorun transformaties op Hallo gegevens nodig, gescheiden van Hallo load query uitvoeren. Bijvoorbeeld, fase Hallo gegevens in een tabel heap Hallo transformaties uitvoeren en vervolgens laden Hallo faseringstabel in Hallo columnstore-index. U kunt ook eerst laden Hallo gegevens en gebruik vervolgens Hallo MPP tootransform Hallo systeemgegevens.

### <a name="adjust-maxdop"></a>MAXDOP aanpassen

Elk distributiepunt comprimeert rowgroups in Hallo columnstore parallel wanneer er meer dan één CPU-kern beschikbaar per distributiepunt. Hallo parallelle uitvoering vereist extra geheugenbronnen, wat toomemory druk en rijgroep bijsnijden leiden kunnen.

tooreduce geheugendruk, kunt u Hallo MAXDOP query hint tooforce Hallo load bewerking toorun in de modus seriële binnen elk distributiepunt.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Manieren tooallocate meer geheugen

DWU grootte en Hallo gebruiker bronklasse samen bepalen hoeveel geheugen beschikbaar is voor de aanvraag voor een gebruiker. tooincrease hello geheugen verlenen voor een load-query, kunt u Verhoog het aantal dwu's Hallo of Hallo bronklasse verhogen.

- tooincrease hello dwu's, Zie [hoe schalen prestaties?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- Zie toochange Hallo bronklasse voor een query [wijzigen van een voorbeeld van een gebruiker resource klasse](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Bijvoorbeeld op DWU 100 kunt een gebruiker in Hallo smallrc bronklasse 100 MB aan geheugen voor elk distributiepunt. Zie voor meer informatie Hallo [gelijktijdigheid in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).

Stel dat u vastgesteld dat er 700 MB aan geheugen tooget rijgroep van hoge kwaliteit grootten. Deze voorbeelden laten zien hoe u Hallo load query kunt uitvoeren met onvoldoende geheugen.

- DWU-1000 en mediumrc gebruikt, is uw geheugentoekenning 800 MB
- DWU 600 en largerc gebruikt, is uw geheugentoekenning 800 MB.


## <a name="next-steps"></a>Volgende stappen

toofind meer manieren tooimprove prestaties in SQL Data Warehouse, Zie Hallo [prestatieoverzicht](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
