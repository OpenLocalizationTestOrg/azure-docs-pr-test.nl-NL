---
title: Wat is er gebeurd met mijn 5 ASP.NET-project (Visual Studio verbonden services) | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt nadat verbinding te maken met een Azure storage-account in een Visual Studio-5 voor ASP.NET-project met Visual Studio services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e7caa9fa-c780-45eb-a546-299fc1c68455
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 4390993772eaf35516e48ad7adcdcec5f1df8d71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-5-project-visual-studio-azure-storage-connected-services"></a><span data-ttu-id="5d30f-103">Wat is er gebeurd met mijn 5 ASP.NET-project (Visual Studio Azure Storage verbonden services)?</span><span class="sxs-lookup"><span data-stu-id="5d30f-103">What happened to my ASP.NET 5 project (Visual Studio Azure Storage connected services)?</span></span>
## <a name="references-added"></a><span data-ttu-id="5d30f-104">Verwijzingen die zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="5d30f-104">References added</span></span>
<span data-ttu-id="5d30f-105">Het Azure Storage NuGet-pakket is toegevoegd aan uw Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="5d30f-105">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="5d30f-106">Dit pakket voegt de volgende .NET verwijzingen toe:</span><span class="sxs-lookup"><span data-stu-id="5d30f-106">This package adds the following .NET references:</span></span>

* <span data-ttu-id="5d30f-107">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="5d30f-107">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="5d30f-108">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="5d30f-108">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="5d30f-109">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="5d30f-109">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="5d30f-110">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="5d30f-110">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="5d30f-111">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="5d30f-111">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="5d30f-112">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="5d30f-112">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="5d30f-113">**Systeem.gegevens**</span><span class="sxs-lookup"><span data-stu-id="5d30f-113">**System.Data**</span></span>
* <span data-ttu-id="5d30f-114">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="5d30f-114">**System.Spatial**</span></span>

<span data-ttu-id="5d30f-115">Ook het NuGet-pakket **Microsoft.Framework.Configuration.Json** is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="5d30f-115">Also, the NuGet package **Microsoft.Framework.Configuration.Json** was added.</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="5d30f-116">Verbindingsreeks voor Azure Storage toegevoegd</span><span class="sxs-lookup"><span data-stu-id="5d30f-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="5d30f-117">In het bestand config.json van uw project, is een element gemaakt met de verbindingsreeks en de sleutel van het geselecteerde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5d30f-117">In the config.json file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="5d30f-118">Zie voor meer informatie [ASP.NET 5](http://www.asp.net/vnext).</span><span class="sxs-lookup"><span data-stu-id="5d30f-118">For more information, see [ASP.NET 5](http://www.asp.net/vnext).</span></span>

