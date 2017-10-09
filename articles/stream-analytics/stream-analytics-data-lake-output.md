---
title: aaaStream Analytics Data Lake Store uitvoer | Microsoft Docs
description: Configuratie van verificatie en autorisatie van een Azure Data Lake Store in een Stream Analytics-taak
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Stream Analytics Data Lake Store-uitvoer
Stream Analytics-taken ondersteunen verschillende uitvoermethoden, een wordt een [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Azure Data Lake Store is een ondernemingsbrede opslagplaats op hyperschaal voor analytische workloads van big data. Data Lake Store kunt u toostore gegevens van elke grootte, type en opnamesnelheid snelheid voor operationele en experimentele analyses.

## <a name="authorize-a-data-lake-store-account"></a>Een Data Lake Store-account toestaan
1. Wanneer Data Lake Store als uitvoer in hello Azure-portal is geselecteerd, wordt u gevraagd tooauthorize gebruik van uw bestaande Data Lake Store of toorequest access toohello Data Lake Store via Hallo klassieke Portal.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Als u al hebt tooData Lake Store, klik op 'Nu autoriseren' en gedurende een korte periode een pagina wordt weergegeven dat aangeeft 'Omleidt tooauthorization'. Hallo pagina automatisch wordt gesloten en u krijgt Hallo pagina waarmee u tooconfigure Hallo Data Lake Store-uitvoer.

Als u niet hebt aangemeld voor Data Lake Store, kunt u volgen Hallo 'Nu aanmelden' koppeling tooinitiate Hallo aanvraag of volg Hallo [gestart instructies](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Hallo Data Lake Store uitvoereigenschappen configureren
Zodra u Hallo geverifieerde Data Lake Store-account hebt, kunt u Hallo eigenschappen configureren voor de uitvoer van uw Data Lake Store. Hallo onderstaande tabel is Hallo lijst met namen van eigenschappen en hun beschrijving tooconfigure uitvoer van uw Data Lake Store.

<table>
<tbody>
<tr>
<td><B>DE NAAM VAN EIGENSCHAP</B></td>
<td><B>BESCHRIJVING</B></td>
</tr>
<tr>
<td>Uitvoeraliassen</td>
<td>Dit is een beschrijvende naam die is gebruikt in query's toodirect Hallo query uitvoer toothis Data Lake Store.</td>
</tr>
<tr>
<td>Data Lake Store-Account</td>
<td>Hallo-naam van Hallo storage-account waarin u de uitvoer wilt verzenden. Er verschijnt een lijst met Hallo aangemelde gebruiker toegang tot de heeft Data Lake Store-accounts.</td>
</tr>
<tr>
<td>Pad voorvoegsel patroon [<I>optionele</I>]</td>
<td>Hallo bestand pad gebruikt toowrite uw bestanden binnen Hallo Data Lake Store-Account opgegeven. <BR>{date} {time}<BR>Voorbeeld 1: Map1/logs / {date} / {time}<BR>Voorbeeld 2: Map1/logs / {date}</td>
</tr>
<tr>
<td>Datum notatie [<I>optionele</I>]</td>
<td>Als Hallo datum token in Hallo voorvoegsel pad wordt gebruikt, kunt u Hallo datumnotatie waarin de bestanden zijn ingedeeld. Voorbeeld: Jjjj/MM/DD</td>
</tr>
<tr>
<td>Tijdnotatie [<I>optionele</I>]</td>
<td>Als Hallo tijd token in Hallo voorvoegsel pad wordt gebruikt, geeft u de tijdnotatie Hallo waarin de bestanden zijn ingedeeld. Hallo alleen ondersteunde waarde is momenteel HH.</td>
</tr>
<tr>
<td>Gebeurtenis serialisatie-indeling</td>
<td>Serialisatie-indeling voor uitvoergegevens. JSON, CSV en Avro worden ondersteund.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Als CSV- of JSON-indeling, moet een codering worden opgegeven. UTF-8 wordt de coderingsindeling Hallo alleen ondersteund op dit moment.</td>
</tr>
<tr>
<td>Scheidingsteken</td>
<td>Alleen van toepassing voor CSV-serialisatie. Stream Analytics ondersteunt een aantal algemene scheidingstekens voor het serialiseren van CSV-gegevens. Ondersteunde waarden zijn komma, puntkomma, spatie, tab en de verticale balk.</td>
</tr>
<tr>
<td>Indeling</td>
<td>Alleen van toepassing op JSON-serialisatie. Lijn gescheiden geeft aan dat Hallo uitvoer wordt ingedeeld door elk JSON-object dat is gescheiden door een nieuwe regel. Matrix geeft aan dat Hallo uitvoer wordt ingedeeld als een matrix met JSON-objecten.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Vernieuwen van Data Lake Store-autorisatie
Er is momenteel een beperking waarin Hallo-verificatietoken toobe handmatig moeten worden vernieuwd om de 90 dagen voor alle taken met Data Lake Store-uitvoer moet. U moet ook toore-verificatie van uw Data Lake Store-account als u uw wachtwoord is gewijzigd sinds de taak is gemaakt of laatst geverifieerd. Een symptoom zijn van dit probleem is geen taakuitvoer en een fout in Hallo Bewerkingslogboeken nodig voor nieuwe autorisatie waarmee wordt aangegeven.

tooresolve dit probleem op door de actieve taak stoppen en ga tooyour Data Lake Store-uitvoer. Klik op de koppeling 'Vernieuwen autorisatie' hello en gedurende een korte periode een pagina wordt weergegeven dat aangeeft 'Omleidt tooauthorization..'. Hallo-pagina wordt automatisch gesloten en als dit lukt, wordt aangegeven 'Autorisatie is vernieuwd'. U moet tooclick 'Opgeslagen' Hallo Hallo pagina onderaan in, en kan worden voortgezet door de taak in de laatste tijd geëindigd tooavoid gegevensverlies Hallo opnieuw te starten.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

