---
title: Wat is er gebeurd met mijn ASP.NET-project? | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt nadat Azure Storage toe te voegen aan een ASP.NET-project met Visual Studio services verbonden
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: e1fe1b6d-4e3d-476d-8b2f-f7ade050515e
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: e2cdc2ff4df85f0224352bd32a3ec62480c3e6e5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-happened-to-my-aspnet-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="714dd-104">Wat is er gebeurd met mijn ASP.NET-project (Visual Studio Azure Storage verbonden service)?</span><span class="sxs-lookup"><span data-stu-id="714dd-104">What happened to my ASP.NET project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="714dd-105">Verwijzingen die zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="714dd-105">References added</span></span>
<span data-ttu-id="714dd-106">Het Azure Storage NuGet-pakket is toegevoegd aan uw Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="714dd-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="714dd-107">Dit pakket voegt de volgende .NET verwijzingen toe:</span><span class="sxs-lookup"><span data-stu-id="714dd-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="714dd-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="714dd-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="714dd-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="714dd-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="714dd-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="714dd-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="714dd-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="714dd-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="714dd-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="714dd-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="714dd-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="714dd-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="714dd-114">**Systeem.gegevens**</span><span class="sxs-lookup"><span data-stu-id="714dd-114">**System.Data**</span></span>
* <span data-ttu-id="714dd-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="714dd-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="714dd-116">Verbindingsreeks voor Azure Storage toegevoegd</span><span class="sxs-lookup"><span data-stu-id="714dd-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="714dd-117">In het bestand web.config van uw project is een element gemaakt met de verbindingsreeks en de sleutel van het geselecteerde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="714dd-117">In the web.config file of your project, an element was created with the selected storage account's connection string and key.</span></span>

<span data-ttu-id="714dd-118">Zie voor meer informatie [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="714dd-118">For more information, see [ASP.NET](http://www.asp.net).</span></span>

