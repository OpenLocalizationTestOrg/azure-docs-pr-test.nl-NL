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
ms.openlocfilehash: 67bdfa8c2cd0f8314c82e2b334a3fa3a5c520c66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool-v1"></a><span data-ttu-id="a4ffd-103">Met behulp van de Azure Import/Export-hulpprogramma (v1)</span><span class="sxs-lookup"><span data-stu-id="a4ffd-103">Using the Azure Import/Export Tool (v1)</span></span>

<span data-ttu-id="a4ffd-104">Het Azure Import/Export-hulpprogramma (WAImportExport.exe) wordt gebruikt voor het maken en beheren van taken voor de Azure Import/Export-service, zodat u kunt brengen grote hoeveelheden gegevens van of naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="a4ffd-105">Deze documentatie is voor v1 van het Azure Import/Export-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-105">This documentation is for v1 of the Azure Import/Export Tool.</span></span> <span data-ttu-id="a4ffd-106">Raadpleeg voor informatie over het gebruik van de meest recente versie van het hulpprogramma [hulpprogramma voor het Azure Import/Export](storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="a4ffd-106">For information about using the most recent version of the tool, please see [Using the Azure Import/Export Tool](storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="a4ffd-107">In deze artikelen wordt uitgelegd hoe u het hulpprogramma te gebruiken voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="a4ffd-107">In these articles, you will see how to use the tool to do the following:</span></span>

- <span data-ttu-id="a4ffd-108">Installeren en instellen van het hulpprogramma voor importeren/exporteren.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="a4ffd-109">Bereid uw harde schijven voor een taak waar u gegevens van uw schijven naar Azure Blob Storage importeren.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="a4ffd-110">Controleer de status van een taak met logboekbestanden kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="a4ffd-111">Herstellen van een import-taak.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-111">Repair an import job.</span></span> 
- <span data-ttu-id="a4ffd-112">Een exporttaak herstellen.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-112">Repair an export job.</span></span> 
- <span data-ttu-id="a4ffd-113">Problemen met het Azure Import/Export-hulpprogramma voor het geval er een probleem opgetreden tijdens het.</span><span class="sxs-lookup"><span data-stu-id="a4ffd-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a4ffd-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4ffd-114">Next steps</span></span>

* [<span data-ttu-id="a4ffd-115">Instellen van het hulpprogramma WAImportExport</span><span class="sxs-lookup"><span data-stu-id="a4ffd-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-how-to.md)