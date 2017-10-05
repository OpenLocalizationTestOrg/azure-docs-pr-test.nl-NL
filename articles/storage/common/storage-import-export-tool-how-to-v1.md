---
title: Met het hulpprogramma Azure Import/Export - v1 | Microsoft Docs
description: Informatie over het gebruik van het hulpprogramma voor importeren/exporteren voor het voorbereiden van harde schijven voor een import-taak, een import-taak herstellen of herstellen van een taak voor het exporteren.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 4ce2273cc0dcc456c2edc8c5dd2fc22496f20380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool-classic-deployment-model"></a><span data-ttu-id="0055f-103">Hulpprogramma voor het Azure Import/Export (klassieke implementatiemodel)</span><span class="sxs-lookup"><span data-stu-id="0055f-103">Using the Azure Import/Export Tool (classic deployment model)</span></span>

<span data-ttu-id="0055f-104">Het Azure Import/Export-hulpprogramma (WAImportExport.exe) wordt gebruikt voor het maken en beheren van taken voor de Azure Import/Export-service, zodat u kunt brengen grote hoeveelheden gegevens van of naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0055f-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="0055f-105">Deze documentatie is voor het klassieke implementatiemodel van het Azure Import/Export-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="0055f-105">This documentation is for the classic deployment model of the Azure Import/Export Tool.</span></span> <span data-ttu-id="0055f-106">Zie voor meer informatie over het gebruik van de meest recente versie van het hulpprogramma [hulpprogramma voor het Azure Import/Export](../storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="0055f-106">For information about using the most recent version of the tool, see [Using the Azure Import/Export Tool](../storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="0055f-107">De volgende artikelen laten zien hoe u naar:</span><span class="sxs-lookup"><span data-stu-id="0055f-107">The following articles show you how to:</span></span>

- <span data-ttu-id="0055f-108">Installeren en instellen van het hulpprogramma voor importeren/exporteren.</span><span class="sxs-lookup"><span data-stu-id="0055f-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="0055f-109">Bereid uw harde schijven voor een taak waar u gegevens van uw schijven naar Azure Blob Storage importeren.</span><span class="sxs-lookup"><span data-stu-id="0055f-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="0055f-110">Controleer de status van een taak met logboekbestanden kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0055f-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="0055f-111">Herstellen van een import-taak.</span><span class="sxs-lookup"><span data-stu-id="0055f-111">Repair an import job.</span></span> 
- <span data-ttu-id="0055f-112">Een exporttaak herstellen.</span><span class="sxs-lookup"><span data-stu-id="0055f-112">Repair an export job.</span></span> 
- <span data-ttu-id="0055f-113">Problemen met het Azure Import/Export-hulpprogramma voor het geval er een probleem opgetreden tijdens het.</span><span class="sxs-lookup"><span data-stu-id="0055f-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0055f-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0055f-114">Next steps</span></span>

* [<span data-ttu-id="0055f-115">Instellen van het hulpprogramma WAImportExport</span><span class="sxs-lookup"><span data-stu-id="0055f-115">Setting up the WAImportExport tool</span></span>](../storage-import-export-tool-how-to.md)