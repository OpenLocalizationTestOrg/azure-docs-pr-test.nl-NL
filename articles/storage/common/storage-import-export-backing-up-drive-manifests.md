---
title: aaaBacking up Azure Import/Export station manifesten | Microsoft Docs
description: Meer informatie over hoe toohave station manifesten voor Hallo Microsoft Azure Import/Export-service automatisch een back-up gemaakt.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Back-ups van schijf manifesten voor Azure Import/Export-taken

Station manifesten kunnen automatisch een back-up tooblobs door Hallo instelling `BackupDriveManifest` eigenschap te`true` in Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) REST-API-bewerkingen. Standaard Hallo station manifesten zijn geen back-up gemaakt. Hallo station manifest back-ups worden opgeslagen als blok-blobs in een container in Hallo storage-account aan Hallo taak zijn gekoppeld. Hallo-containernaam is standaard `waimportexport`, maar u kunt een andere naam opgeven in Hallo `DiagnosticsPath` eigenschap bij het aanroepen van Hallo `Put Job` of `Update Job Properties` bewerkingen. Hallo back-manifest blob zijn met de naam in de volgende indeling Hallo: `waies/jobname_driveid_timestamp_manifest.xml`.

 U kunt de URI van de back-station Hallo voor een taak door de aanroepende Hallo manifesten Hallo ophalen [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) bewerking. Hallo blob URI wordt geretourneerd als Hallo `ManifestUri` eigenschap voor elk station.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van REST-API voor Hallo Import/Export-service](storage-import-export-using-the-rest-api.md)
