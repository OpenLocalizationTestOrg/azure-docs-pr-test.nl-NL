---
title: Wat is er gebeurd met mijn cloudserviceproject? | Microsoft Docs
description: Hierin wordt beschreven wat er gebeurt in een cloud services-project nadat verbinding te maken met een Azure storage-account met Visual Studio services verbonden
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: ca0ea68d-f417-4ce8-9413-40d76f69cdea
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 4c9de56f6daf07097c0f593db37d14dce3bce05f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="what-happened-to-my-cloud-services-project-visual-studio-azure-storage-connected-service"></a><span data-ttu-id="ae00d-104">Wat is er gebeurd met mijn cloud services-project (Visual Studio Azure Storage verbonden service)?</span><span class="sxs-lookup"><span data-stu-id="ae00d-104">What happened to my cloud services project (Visual Studio Azure Storage connected service)?</span></span>
## <a name="references-added"></a><span data-ttu-id="ae00d-105">Verwijzingen die zijn toegevoegd</span><span class="sxs-lookup"><span data-stu-id="ae00d-105">References added</span></span>
<span data-ttu-id="ae00d-106">Het Azure Storage NuGet-pakket is toegevoegd aan uw Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="ae00d-106">The Azure Storage NuGet package was added to your Visual Studio project.</span></span>  
<span data-ttu-id="ae00d-107">Dit pakket voegt de volgende .NET verwijzingen toe:</span><span class="sxs-lookup"><span data-stu-id="ae00d-107">This package adds the following .NET references:</span></span>

* <span data-ttu-id="ae00d-108">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="ae00d-108">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="ae00d-109">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="ae00d-109">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="ae00d-110">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="ae00d-110">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="ae00d-111">**Microsoft.WindowsAzure.Configuration**</span><span class="sxs-lookup"><span data-stu-id="ae00d-111">**Microsoft.WindowsAzure.Configuration**</span></span>
* <span data-ttu-id="ae00d-112">**Microsoft.WindowsAzure.Storage**</span><span class="sxs-lookup"><span data-stu-id="ae00d-112">**Microsoft.WindowsAzure.Storage**</span></span>
* <span data-ttu-id="ae00d-113">**Newtonsoft.Json**</span><span class="sxs-lookup"><span data-stu-id="ae00d-113">**Newtonsoft.Json**</span></span>
* <span data-ttu-id="ae00d-114">**Systeem.gegevens**</span><span class="sxs-lookup"><span data-stu-id="ae00d-114">**System.Data**</span></span>
* <span data-ttu-id="ae00d-115">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="ae00d-115">**System.Spatial**</span></span>

## <a name="connection-string-for-azure-storage-added"></a><span data-ttu-id="ae00d-116">Verbindingsreeks voor Azure Storage toegevoegd</span><span class="sxs-lookup"><span data-stu-id="ae00d-116">Connection string for Azure Storage added</span></span>
<span data-ttu-id="ae00d-117">Elementen zijn gemaakt met de verbindingsreeks en de sleutel van het geselecteerde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ae00d-117">Elements were created with the selected storage account's connection string and key.</span></span> <span data-ttu-id="ae00d-118">Wijzigingen zijn aangebracht in de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="ae00d-118">Modifications were made to the following files:</span></span>

* <span data-ttu-id="ae00d-119">**ServiceDefinition.csdef**</span><span class="sxs-lookup"><span data-stu-id="ae00d-119">**ServiceDefinition.csdef**</span></span>
* <span data-ttu-id="ae00d-120">**ServiceConfiguration.Cloud.cscfg**</span><span class="sxs-lookup"><span data-stu-id="ae00d-120">**ServiceConfiguration.Cloud.cscfg**</span></span>
* <span data-ttu-id="ae00d-121">**ServiceConfiguration.Local.cscfg**</span><span class="sxs-lookup"><span data-stu-id="ae00d-121">**ServiceConfiguration.Local.cscfg**</span></span>

