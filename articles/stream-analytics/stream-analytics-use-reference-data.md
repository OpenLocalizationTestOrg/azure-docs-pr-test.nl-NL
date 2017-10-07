---
title: aaaUse gegevens en lookup verwijzingsdimensies in Stream Analytics | Microsoft Docs
description: Referentiegegevens gebruiken in een Stream Analytics-query
keywords: referentiegegevens opzoektabel
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 06103be5-553a-4da1-8a8d-3be9ca2aff54
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fb1d18fba920db5e097d0c95d333e8e8390d1589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-reference-data-or-lookup-tables-in-a-stream-analytics-input-stream"></a>Met behulp van verwijzingsdimensies of opzoeken van gegevens in een Stream Analytics-invoerstroom
Referentiegegevens (ook wel bekend als een opzoektabel) is een beperkte verzameling die is statisch of vertraging wijzigen van aard gebruikt tooperform een lookup- of toocorrelate met uw gegevensstroom. gebruik van referentiegegevens toomake in uw Azure Stream Analytics-taak in het algemeen gebruikt u een [verwijzing gegevens Join](https://msdn.microsoft.com/library/azure/dn949258.aspx) in uw Query. Stream Analytics maakt gebruik van Azure Blob storage als Hallo opslaglaag voor referentiegegevens, en met Azure Data Factory-verwijzing gegevens kan getransformeerd en/of gekopieerde tooAzure Blob-opslag voor gebruik als referentie-gegevens van [een willekeurig aantal cloud-gebaseerde en lokale gegevensarchieven](../data-factory/data-factory-data-movement-activities.md). Referentiegegevens is gemodelleerd als een reeks blobs (gedefinieerd in de invoer configuratie Hallo) in oplopende volgorde van Hallo datum/tijd in Hallo blob-naam opgegeven. Deze **alleen** ondersteunt toohello einde van Hallo reeks toe te voegen met behulp van een datum/tijd **groter** dan Hallo opgegeven in de laatste blob Hallo in Hallo reeks.

Stream Analytics is een **limiet van 100 MB per blob** maar taken kunnen meerdere verwijzing blobs verwerken met behulp van Hallo **pad patroon** eigenschap.


## <a name="configuring-reference-data"></a>Referentiegegevens configureren
tooconfigure uw referentiegegevens, moet u eerst toocreate invoer van het type **referentiegegevens**. Hallo in de volgende tabel wordt elke eigenschap die u tijdens het Hallo verwijzing gegevensinvoer maken met de beschrijving tooprovide moet uitgelegd:


<table>
<tbody>
<tr>
<td>De naam van eigenschap</td>
<td>Beschrijving</td>
</tr>
<tr>
<td>Invoeralias</td>
<td>Een beschrijvende naam die wordt gebruikt in Hallo taak query tooreference deze invoer.</td>
</tr>
<tr>
<td>Storage-Account</td>
<td>Hallo-naam van de opslagaccount Hallo waar uw BLOB's zich bevinden. Als het zich in Hallo hetzelfde abonnement als uw Stream Analytics-taak kunt u deze selecteren in de vervolgkeuzelijst Hallo.</td>
</tr>
<tr>
<td>De sleutel van opslagaccount</td>
<td>de geheime sleutel Hallo Hallo storage-account gekoppeld. Dit wordt automatisch gevuld als Hallo storage-account in Hallo is hetzelfde abonnement als uw Stream Analytics-taak.</td>
</tr>
<tr>
<td>Storage-Container</td>
<td>Containers bieden een logische groepering van blobs die zijn opgeslagen in Hallo Microsoft Azure Blob-service. U moet een container voor blob opgeven tijdens het uploaden van een blob toohello Blob-service.</td>
</tr>
<tr>
<td>Het pad</td>
<td>Hallo pad gebruikt toolocate uw blobs in de opgegeven container Hallo. Binnen Hallo pad, kunt u kiezen toospecify een of meer exemplaren van Hallo 2 variabelen te volgen:<BR>{date} {time}<BR>Voorbeeld 1: products/{date}/{time}/product-list.csv<BR>Voorbeeld 2: products/{date}/product-list.csv
</tr>
<tr>
<td>[Optioneel] datumnotatie</td>
<td>Als u {date} binnen Hallo pad patroon die u hebt opgegeven gebruikt hebt, kunt u de datumnotatie Hallo waarin uw blobs zijn ingedeeld in Hallo vervolgkeuzelijst met ondersteunde indelingen selecteren.<BR>Voorbeeld: Jjjj/MM/DD, DD-MM-jjjj, enzovoort.</td>
</tr>
<tr>
<td>[Optioneel] tijdnotatie</td>
<td>Als u {time} binnen Hallo pad patroon die u hebt opgegeven gebruikt hebt, kunt u de tijdnotatie Hallo waarin uw blobs zijn ingedeeld in Hallo vervolgkeuzelijst met ondersteunde indelingen selecteren.<BR>Bijvoorbeeld: HH uu/mm of uu mm</td>
</tr>
<tr>
<td>Gebeurtenis serialisatie-indeling</td>
<td>controleren of dat uw query's werken Hallo zoals verwacht, Stream Analytics toomake moet tooknow welke serialisatie-indeling wordt gebruikt voor inkomende gegevensstromen. Hallo ondersteunde indelingen zijn voor referentiegegevens, CSV en JSON.</td>
</tr>
<tr>
<td>Encoding</td>
<td>UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment</td>
</tr>
</tbody>
</table>

## <a name="generating-reference-data-on-a-schedule"></a>Referentiegegevens volgens een schema genereren
Als uw referentiegegevens een langzaam veranderende gegevensset is, wordt ondersteuning voor het vernieuwen van referentiegegevens ingeschakeld door het opgeven van een pad-patroon in invoer Hallo-configuratie met behulp van Hallo {date} en {time} vervanging tokens. Stream Analytics hervat Hallo bijgewerkt verwijzing gegevensdefinities op basis van dit patroon pad. Bijvoorbeeld, een patroon van `sample/{date}/{time}/products.csv` met een datumnotatie van **'Jjjj-MM-DD'** en tijdnotatie **'Uu mm'** Hiermee geeft u Stream Analytics toopick up Hallo bijgewerkt blob `sample/2015-04-16/17-30/products.csv` om 5:30 uur April 16de, 2015 UTC-tijdzone.

> [!NOTE]
> Momenteel zoekt Stream Analytics-taken Hallo blob vernieuwen alleen wanneer toohello tijd gecodeerd in de blob-naam Hallo Hallo machinetijd wordt bestuurd. Bijvoorbeeld, Hallo taak zoekt `sample/2015-04-16/17-30/products.csv` zo snel mogelijk, maar geen eerder dan 5:30 PM 16de April 2015 UTC tijdzone. Het *nooit* zoekt u naar een blob met een gecodeerde tijd eerder dan Hallo laatste Count(*)) wordt gedetecteerd.
> 
> Bijvoorbeeld Zodra de taak Hallo Hallo blob vindt `sample/2015-04-16/17-30/products.csv` negeert deze bestanden met een gecodeerde datum ouder is dan 5:30 PM 16de April 2015 als een laat binnenkomen `sample/2015-04-16/17-25/products.csv` blob wordt gemaakt in Hallo dezelfde container Hallo taak maakt geen gebruik.
> 
> Op dezelfde manier als `sample/2015-04-16/17-30/products.csv` alleen op 10:03 PM 16de April 2015 wordt geproduceerd, maar geen blob met een eerdere datum is aanwezig in de container hello, Hallo taak wordt dit bestand begint bij 10:03 PM 16de April 2015 gebruiken en vorige referentiegegevens hello gebruiken tot.
> 
> Een uitzondering toothis is als Hallo-taak toore-proces gegevens terug in tijd moet of wanneer het Hallo-taak voor het eerst wordt gestart. Aan begin zoekt tijd Hallo taak naar de meest recente blob Hallo geproduceerd voordat de taak Hallo begintijd opgegeven. Dit wordt gedaan tooensure dat er een **niet-lege** verwijst naar gegevensset wanneer Hallo-taak wordt gestart. Als er een kan niet worden gevonden, Hallo-taak wordt weergegeven na diagnostische Hallo: `Initializing input without a valid reference data blob for UTC time <start time>`.
> 
> 

[Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) gebruikte tooorchestrate Hallo taak voor het maken van Hallo bijgewerkt blobs is vereist voor Stream Analytics tooupdate verwijzing gegevensdefinities kan zijn. Data Factory is een cloud-gebaseerde gegevens integration-service die is ingedeeld en automatiseert Hallo verplaatsing en transformatie van gegevens. Data Factory ondersteunt [tooa groot aantal in de cloud en on-premises gegevensopslagexemplaren verbinden](../data-factory/data-factory-data-movement-activities.md) en gemakkelijk verplaatsen van gegevens op een vaste planning die u opgeeft. Voor meer informatie en stapsgewijze instructies over hoe tooset van een Data Factory met toogenerate referentiegegevens voor Stream Analytics die wordt vernieuwd op basis van een vooraf gedefinieerde planning pipeline, Bekijk dit [GitHub voorbeeld](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs).

## <a name="tips-on-refreshing-your-reference-data"></a>Tips voor het vernieuwen van uw verwijzingsgegevens
1. Stream Analytics tooreload Hallo blob leidt niet tot verwijzing gegevensblobs overschrijven en in sommige gevallen kan dit leiden tot Hallo taak toofail. Hallo aanbevolen manier toochange referentiegegevens tooadd is een nieuwe blob Hallo container en het pad patroon gedefinieerd in Hallo taak invoer met en gebruik van een datum/tijd **groter** dan Hallo opgegeven in de laatste blob Hallo in Hallo reeks.
2. Verwijzing naar gegevensblobs zijn **niet** geordend door 'Laatst gewijzigd' Hallo-blob-tijd, maar alleen door Hallo-tijd en datum in Hallo Hallo {date} en {time} vervangingen met blob-naam opgegeven.
3. In enkele gevallen kan een taak moet teruggaan in tijd, daarom verwijzing gegevensblobs mag niet worden gewijzigd of verwijderd.

## <a name="get-help"></a>Help opvragen
Voor verdere hulp kunt u mogelijk terecht op het [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Volgende stappen
U hebt ingevoerd tooStream Analytics, een beheerde service voor streaminganalyse van gegevens van Hallo Internet der dingen zijn. toolearn meer informatie over deze service, Zie:

* [Aan de slag met Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md)
* [Azure Stream Analytics-taken schalen](stream-analytics-scale-jobs.md)
* [Naslaggids voor Azure Stream Analytics Query](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [REST API-naslaggids voor Azure Stream Analytics Management](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
