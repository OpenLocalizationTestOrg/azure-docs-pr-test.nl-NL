---
title: aaaReviewing taakstatus Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe toouse Hallo logboekbestanden wanneer Hallo importeren of exporteren van de taak toosee Hallo status van Hallo Import/Export-taak werd uitgevoerd.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="54eaf-103">De status van de Azure Import/Export-taak controleren met logboekbestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="54eaf-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="54eaf-104">Wanneer Hallo Microsoft Azure Import/Export-service stations die zijn gekoppeld aan een taak importeren of exporteren verwerkt, schrijft deze kopie logboek bestanden toohello storage account tooor van waaruit u importeert of exporteert blobs.</span><span class="sxs-lookup"><span data-stu-id="54eaf-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="54eaf-105">Hallo-logboekbestand bevat gedetailleerde status van elk bestand dat is geïmporteerd of geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="54eaf-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="54eaf-106">Hallo URL tooeach kopie-logboekbestand wordt geretourneerd wanneer u een query uitvoeren op Hallo status van een voltooide taak; Zie [Get Job](/rest/api/storageservices/Get-Job3) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="54eaf-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="54eaf-107">Voorbeeld-URL 's</span><span class="sxs-lookup"><span data-stu-id="54eaf-107">Example URLs</span></span>

<span data-ttu-id="54eaf-108">Hallo hieronder vindt u voorbeeld-URL's voor kopiëren-logboekbestanden voor een import-taak met twee schijven:</span><span class="sxs-lookup"><span data-stu-id="54eaf-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="54eaf-109">Zie [Import/Export-service indeling van logboekbestand](../storage-import-export-file-format-log.md) voor Hallo-indeling van Logboeken voor kopiëren en Hallo volledige lijst met statuscodes.</span><span class="sxs-lookup"><span data-stu-id="54eaf-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="54eaf-110">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54eaf-110">Next steps</span></span>
 
 * [<span data-ttu-id="54eaf-111">Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="54eaf-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="54eaf-112">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="54eaf-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="54eaf-113">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="54eaf-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="54eaf-114">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="54eaf-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="54eaf-115">Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="54eaf-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
