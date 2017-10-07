---
title: aaaDiagnostics en fout herstel voor Azure Import/Export-taken | Microsoft Docs
description: Meer informatie over hoe de taken voor tooenable uitgebreide logboekregistratie voor Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Diagnostische gegevens en de fout herstel voor Azure Import/Export-taken
Voor elk station verwerkt maakt hello Azure Import/Export-service een foutenlogboek in het opslagaccount Hallo die zijn gekoppeld. U kunt ook uitgebreide logboekregistratie inschakelen door de instelling Hallo `LogLevel` eigenschap te`Verbose` bij het aanroepen van Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerkingen.

 Standaard Logboeken geschreven tooa container met de naam `waimportexport`. U kunt een andere naam opgeven door de instelling Hallo `DiagnosticsPath` eigenschap bij het aanroepen van Hallo `Put Job` of `Update Job Properties` bewerkingen. Hallo logboeken worden opgeslagen als blok-blobs Hello volgende naamconventie: `waies/jobname_driveid_timestamp_logtype.xml`.

 U kunt ophalen Hallo URI van Hallo-logboeken voor een taak door de aanroepende Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking. Hallo URI voor de uitgebreide logboek hello wordt geretourneerd als Hallo `VerboseLogUri` eigenschap voor elk station terwijl Hallo URI voor Hallo foutenlogboek wordt geretourneerd als Hallo `ErrorLogUri` eigenschap.

U kunt Hallo logboekregistratie gegevens tooidentify Hallo problemen te volgen.

## <a name="drive-errors"></a>Station fouten

Hallo volgende items zijn geclassificeerd als station fouten:

-   Fouten in de toegang tot of het lezen van Hallo-manifestbestand

-   Onjuiste BitLocker-sleutels

-   Schijf lezen/schrijven-fouten

## <a name="blob-errors"></a>BLOB-fouten

Hallo volgende items zijn geclassificeerd als blob fouten:

-   Onjuiste of conflicterende blob of -namen

-   Ontbrekende bestanden

-   BLOB is niet gevonden

-   Afgekapte bestanden (bestanden op schijf Hallo Hallo zijn kleiner is dan de opgegeven in het manifest Hallo)

-   Beschadigd bestand inhoud (voor importtaken die is gedetecteerd met een MD5-checksum komt niet overeen)

-   Beschadigde blob-eigenschap bestanden met metagegevens en (gedetecteerd met een MD5-checksum komt niet overeen)

-   Onjuist schema voor Hallo blob eigenschappen en/of bestanden met metagegevens

Mogelijk zijn er gevallen waarbij sommige onderdelen van een taak importeren of exporteren komen niet voltooid, terwijl hello algemene taak nog steeds is voltooid. In dit geval kunt u uploaden of downloaden Hallo Hallo gegevens via netwerk ontbreekt of u een nieuwe taak tootransfer Hallo gegevens kunt maken. Zie Hallo [Azure Import/Export hulpprogramma verwijzing](storage-import-export-tool-how-to-v1.md) toolearn hoe toorepair gegevens Hallo via netwerk.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van REST-API voor Hallo Import/Export-service](storage-import-export-using-the-rest-api.md)
