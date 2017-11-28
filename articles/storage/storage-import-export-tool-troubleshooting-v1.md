---
title: aaaTroubleshooting hello Azure-hulpprogramma voor importeren/exporteren | Microsoft Docs
description: Meer informatie over van Hallo voorkomende problemen die worden weergegeven wanneer u hello Azure-hulpprogramma voor importeren/exporteren en hoe toohandle ze.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="f493c-103">Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="f493c-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="f493c-104">Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren retourneert foutberichten worden weergegeven als deze wordt uitgevoerd in de problemen.</span><span class="sxs-lookup"><span data-stu-id="f493c-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="f493c-105">Dit onderwerp worden enkele veelvoorkomende problemen die gebruikers kunnen uitvoeren in.</span><span class="sxs-lookup"><span data-stu-id="f493c-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="f493c-106">Een kopieersessie is mislukt, wat ik moet nemen?</span><span class="sxs-lookup"><span data-stu-id="f493c-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="f493c-107">Wanneer een sessie kopiëren is mislukt, zijn er twee opties:</span><span class="sxs-lookup"><span data-stu-id="f493c-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="f493c-108">Als het Hallo-fout is een herstelbare, bijvoorbeeld als de netwerkshare Hallo offline was voor een korte periode en nu weer online is, kunt u Hallo kopieersessie hervatten.</span><span class="sxs-lookup"><span data-stu-id="f493c-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="f493c-109">Als het Hallo-fout is geen herstelbare, bijvoorbeeld als u verkeerde bronmap bestand Hallo opgegeven in de opdrachtregelparameters Hallo, moet u tooabort Hallo kopieersessie.</span><span class="sxs-lookup"><span data-stu-id="f493c-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="f493c-110">Zie [harde schijven voorbereiden voor een Import-taak](storage-import-export-tool-preparing-hard-drives-import-v1.md) voor meer informatie over wordt hervat en wordt afgebroken sessies kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f493c-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="f493c-111">Ik kan hervatten of afbreken van een kopieersessie.</span><span class="sxs-lookup"><span data-stu-id="f493c-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="f493c-112">Als Hallo kopieersessie Hallo eerste kopieersessie voor een station, wordt fout het Hallo-bericht moet status: "hello eerste kopieersessie kan niet worden hervat of afgebroken."</span><span class="sxs-lookup"><span data-stu-id="f493c-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="f493c-113">In dit geval kunt u Hallo oude journaalbestand verwijderen en Voer Hallo opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="f493c-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="f493c-114">Als een kopieersessie is de eerste is voor een station niet hello, kan altijd hervat of afgebroken.</span><span class="sxs-lookup"><span data-stu-id="f493c-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="f493c-115">Hallo journal-bestand is verbroken, kan ik nog steeds Hallo taak maken?</span><span class="sxs-lookup"><span data-stu-id="f493c-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="f493c-116">Hallo journal-bestand voor een station Hallo volledige informatie van het kopiëren van schijf toothis bevat en dit is nodig tooadd meer bestanden toohello station en gebruikte toocreate een import-taak kan worden.</span><span class="sxs-lookup"><span data-stu-id="f493c-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="f493c-117">Als Hallo journal-bestand verloren gegaan is, hebt u tooredo alle Hallo kopie-sessies voor Hallo-station.</span><span class="sxs-lookup"><span data-stu-id="f493c-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f493c-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f493c-118">Next steps</span></span>
 
* [<span data-ttu-id="f493c-119">Instellen van hello azure import/export-hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="f493c-119">Setting up hello azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="f493c-120">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="f493c-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="f493c-121">De taakstatus controleren met kopielogboekbestanden</span><span class="sxs-lookup"><span data-stu-id="f493c-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="f493c-122">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="f493c-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="f493c-123">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="f493c-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
