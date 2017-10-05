---
title: Taakstatus Azure Import/Export - v1 controleren | Microsoft Docs
description: Informatie over het gebruik van de logboekbestanden gemaakt wanneer de taak importeren of exporteren werd uitgevoerd voor de status van de taak voor importeren/exporteren.
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
ms.openlocfilehash: bdb30bc28c36ab9e969efc8be3b87b97e4027b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="6c0ac-103">De status van de Azure Import/Export-taak controleren met logboekbestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="6c0ac-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="6c0ac-104">Wanneer de Microsoft Azure Import/Export-service stations die zijn gekoppeld aan een taak importeren of exporteren verwerkt, schrijft kopie logboekbestanden naar het opslagaccount naar of van waaruit u importeert of exporteert blobs.</span><span class="sxs-lookup"><span data-stu-id="6c0ac-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="6c0ac-105">Het logboekbestand bevat een gedetailleerde status van elk bestand dat is geïmporteerd of geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="6c0ac-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="6c0ac-106">De URL naar het logboekbestand van elke kopie wordt geretourneerd wanneer u een query uitvoeren op de status van een voltooide taak; Zie [Get Job](/rest/api/storageservices/Get-Job3) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c0ac-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="6c0ac-107">Voorbeeld-URL 's</span><span class="sxs-lookup"><span data-stu-id="6c0ac-107">Example URLs</span></span>

<span data-ttu-id="6c0ac-108">Het volgende zijn voorbeeld-URL's voor kopiëren-logboekbestanden voor een import-taak met twee schijven:</span><span class="sxs-lookup"><span data-stu-id="6c0ac-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="6c0ac-109">Zie [Import/Export-service indeling van logboekbestand](../storage-import-export-file-format-log.md) voor de indeling van de logboeken van kopiëren en een volledige lijst met statuscodes.</span><span class="sxs-lookup"><span data-stu-id="6c0ac-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="6c0ac-110">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c0ac-110">Next steps</span></span>
 
 * [<span data-ttu-id="6c0ac-111">Instellen van het hulpprogramma Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="6c0ac-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="6c0ac-112">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="6c0ac-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="6c0ac-113">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="6c0ac-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="6c0ac-114">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="6c0ac-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="6c0ac-115">Problemen met het hulpprogramma Azure Import/Export oplossen</span><span class="sxs-lookup"><span data-stu-id="6c0ac-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
