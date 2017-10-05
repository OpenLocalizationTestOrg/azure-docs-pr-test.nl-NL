---
title: Wat is er gebeurd met mijn webtaak-project (Visual Studio Azure Storage verbonden service)? | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurd is in een project Azure webtaak nadat verbinding te maken met een opslagaccount met Visual Studio services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 36ae7ff7-c22c-47eb-b220-049d61618c74
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3b28ddeadc87937941d60b16fae817e59a220b22
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-webjob-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="e4d23-104">Wat is er gebeurd met mijn webtaak-project (Visual Studio Azure Storage verbonden service)?</span><span class="sxs-lookup"><span data-stu-id="e4d23-104">What happened to my WebJob project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="e4d23-105">Verwijzingen die zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="e4d23-105">References Added</span></span>
<span data-ttu-id="e4d23-106">Het Azure Storage NuGet-pakket is toegevoegd aan of bijgewerkt in Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="e4d23-106">The Azure Storage NuGet package was added to or updated in your Visual Studio project.</span></span>  
<span data-ttu-id="e4d23-107">Dit pakket voegt de volgende .NET verwijzingen toe:</span><span class="sxs-lookup"><span data-stu-id="e4d23-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="e4d23-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="e4d23-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="e4d23-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="e4d23-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="e4d23-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="e4d23-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="e4d23-111">**Microsoft.WindowsAzure.ConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="e4d23-111">**Microsoft.WindowsAzure.ConfigurationManager**</span></span>
* <span data-ttu-id="e4d23-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="e4d23-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="e4d23-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="e4d23-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="e4d23-114">**Systeem.gegevens**</span><span class="sxs-lookup"><span data-stu-id="e4d23-114">**System.Data**</span></span>
* <span data-ttu-id="e4d23-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="e4d23-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="e4d23-116">Verbindingsreeks voor Azure Storage toegevoegd</span><span class="sxs-lookup"><span data-stu-id="e4d23-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="e4d23-117">In het bestand App.config van uw project de **AzureWebJobsStorage** en **AzureWebJobsDashboard** -items zijn bijgewerkt met de verbindingsreeks en de sleutel van het geselecteerde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e4d23-117">In the App.config file of your project, the **AzureWebJobsStorage** and **AzureWebJobsDashboard** entries were updated with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="e4d23-118">Zie voor meer informatie [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="e4d23-118">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

