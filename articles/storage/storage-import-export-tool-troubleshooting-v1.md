---
title: De Azure Import/Export-hulpprogramma voor probleemoplossing | Microsoft Docs
description: Meer informatie over enkele van de algemene problemen zichtbaar wanneer u de Azure-hulpprogramma voor importeren/exporteren en hoe deze te verwerken.
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
ms.openlocfilehash: 43b5d5a57df6bdda57a31ff0330ec6eff7aa732c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="72525-103">Problemen met het hulpprogramma Azure Import/Export oplossen</span><span class="sxs-lookup"><span data-stu-id="72525-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="72525-104">Het hulpprogramma Microsoft Azure Import/Export retourneert foutberichten worden weergegeven als deze wordt uitgevoerd in de problemen.</span><span class="sxs-lookup"><span data-stu-id="72525-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="72525-105">Dit onderwerp worden enkele veelvoorkomende problemen die gebruikers kunnen uitvoeren in.</span><span class="sxs-lookup"><span data-stu-id="72525-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="72525-106">Een kopieersessie is mislukt, wat ik moet nemen?</span><span class="sxs-lookup"><span data-stu-id="72525-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="72525-107">Wanneer een sessie kopiëren is mislukt, zijn er twee opties:</span><span class="sxs-lookup"><span data-stu-id="72525-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="72525-108">Als de fout herstelbare, bijvoorbeeld als de netwerkshare gedurende een korte periode offline was en nu weer online is, kunt u de kopieersessie hervatten.</span><span class="sxs-lookup"><span data-stu-id="72525-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="72525-109">Als de fout niet herstelbare, bijvoorbeeld als u de map van het verkeerde bron in de opdrachtregelparameters opgegeven is, moet u afbreken van de kopieersessie.</span><span class="sxs-lookup"><span data-stu-id="72525-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="72525-110">Zie [harde schijven voorbereiden voor een Import-taak](storage-import-export-tool-preparing-hard-drives-import-v1.md) voor meer informatie over wordt hervat en wordt afgebroken sessies kopiëren.</span><span class="sxs-lookup"><span data-stu-id="72525-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="72525-111">Ik kan hervatten of afbreken van een kopieersessie.</span><span class="sxs-lookup"><span data-stu-id="72525-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="72525-112">Als de sessie kopiëren de eerste kopieersessie voor een station, wordt het foutbericht moet zijn: "de eerste kopieersessie kan niet worden hervat of afgebroken."</span><span class="sxs-lookup"><span data-stu-id="72525-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="72525-113">In dit geval kunt u het oude journaalbestand verwijderen en voer de opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="72525-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="72525-114">Als een kopieersessie niet het eerste item voor een station, kan altijd hervat of afgebroken.</span><span class="sxs-lookup"><span data-stu-id="72525-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="72525-115">Het bestand van het wijzigingslogboek is verbroken, kan ik nog steeds maken de taak?</span><span class="sxs-lookup"><span data-stu-id="72525-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="72525-116">Het logboek-bestand voor een station bevat de volledige gegevens van het kopiëren van gegevens naar dit station en is nodig is voor de bestanden meer toevoegen aan het station en wordt gebruikt voor het maken van een import-taak.</span><span class="sxs-lookup"><span data-stu-id="72525-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="72525-117">Als het journaalbestand verbroken wordt, moet u de kopie-sessies voor het station opnieuw.</span><span class="sxs-lookup"><span data-stu-id="72525-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="72525-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="72525-118">Next steps</span></span>
 
* [<span data-ttu-id="72525-119">Instellen van het hulpprogramma azure import/export</span><span class="sxs-lookup"><span data-stu-id="72525-119">Setting up the azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="72525-120">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="72525-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="72525-121">De taakstatus controleren met kopielogboekbestanden</span><span class="sxs-lookup"><span data-stu-id="72525-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="72525-122">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="72525-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="72525-123">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="72525-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
