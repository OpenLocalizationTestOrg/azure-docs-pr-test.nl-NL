---
title: Naslaginformatie voor Azure Data Factory-ontwikkelaars
description: Meer informatie over de verschillende manieren om te maken, bewaken en beheren van Azure data Factory
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: dc752fa1-a6c3-4753-904e-9f32d0a940b7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/17/2017
ms.author: spelluru
redirect_url: https://azure.microsoft.com/services/data-factory/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: e0f6c078b60df6bb7381d066bebb3e400b3b97ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-data-factory-developer-reference"></a><span data-ttu-id="9eb77-103">Naslaginformatie voor Azure Data Factory-ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="9eb77-103">Azure Data Factory Developer Reference</span></span>
<span data-ttu-id="9eb77-104">U kunt maken, bewaken en beheren van de fabrieken met behulp van Azure-portal, Azure PowerShell, Class-bibliotheek voor .NET of REST-API.</span><span class="sxs-lookup"><span data-stu-id="9eb77-104">You can create, monitor, and manage the factories using either Azure portal, Azure PowerShell, .NET Class Library, or REST API.</span></span>

| <span data-ttu-id="9eb77-105">Methode</span><span class="sxs-lookup"><span data-stu-id="9eb77-105">Method</span></span> | <span data-ttu-id="9eb77-106">Resourcelocatie</span><span class="sxs-lookup"><span data-stu-id="9eb77-106">Resource Location</span></span> | <span data-ttu-id="9eb77-107">Referenties voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="9eb77-107">Developer References</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eb77-108">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9eb77-108">Azure portal</span></span> |[<span data-ttu-id="9eb77-109">https://Portal.Azure.com/</span><span class="sxs-lookup"><span data-stu-id="9eb77-109">https://portal.azure.com/</span></span>](https://portal.azure.com) |[<span data-ttu-id="9eb77-110">Aan de slag met Azure Data Factory (Azure-portal)</span><span class="sxs-lookup"><span data-stu-id="9eb77-110">Get started with Azure Data Factory (Azure portal)</span></span>](data-factory-build-your-first-pipeline-using-editor.md) |
| <span data-ttu-id="9eb77-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9eb77-111">Azure PowerShell</span></span> |<span data-ttu-id="9eb77-112">Download de meest recente [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="9eb77-112">Download the latest [Azure PowerShell](http://go.microsoft.com/?linkid=9811175&clcid=0x409)</span></span> |[<span data-ttu-id="9eb77-113">Cmdlet-verwijzing</span><span class="sxs-lookup"><span data-stu-id="9eb77-113">Cmdlet reference</span></span>](https://msdn.microsoft.com/library/dn820234.aspx) |
| <span data-ttu-id="9eb77-114">.NET-klassenbibliotheek</span><span class="sxs-lookup"><span data-stu-id="9eb77-114">.NET Class Library</span></span> |<span data-ttu-id="9eb77-115">Azure Data Factory .NET SDK kunt u, bewaken, en maken en beheren van Azure data factory's Data Factory met behulp van een activiteit .NET uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="9eb77-115">The Azure Data Factory .NET SDK enables you to create, monitor, and manage Azure data factories and extend Data Factory using a .NET activity.</span></span> <span data-ttu-id="9eb77-116">Zie [aangepaste activiteiten gebruiken in een Azure Data Factory-pijplijn](data-factory-use-custom-activities.md) en [maken, bewaken en beheren van Azure data Factory met .NET SDK voor Data Factory](data-factory-create-data-factories-programmatically.md) artikelen om u te helpen aan de slag.</span><span class="sxs-lookup"><span data-stu-id="9eb77-116">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) and [Create, monitor, and manage Azure data factories using Data Factory .NET SDK](data-factory-create-data-factories-programmatically.md) articles to help you get started.</span></span><br/><br/><span data-ttu-id="9eb77-117"><b>De meest recente Nuget downloaden</b></span><span class="sxs-lookup"><span data-stu-id="9eb77-117"><b>Downloading the latest Nuget</b></span></span><br/><span data-ttu-id="9eb77-118">U kunt de nieuwste Azure Data Factory Management bibliotheek Nuget-pakket van downloaden: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span><span class="sxs-lookup"><span data-stu-id="9eb77-118">You can download the latest Azure Data Factory Management Library Nuget package from: [https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories/)</span></span><br/><br/><span data-ttu-id="9eb77-119">**Met behulp van de Package Manager-Console in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="9eb77-119">**Using Package Manager Console in Visual Studio**</span></span><br/><span data-ttu-id="9eb77-120">U kunt de volgende opdracht uitvoeren in Visual Studio Package Manager-Console om op te halen van de nieuwste Azure Data Factory Management-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="9eb77-120">You can run the following command in Visual Studio’s Package Manager Console to get the latest Azure Data Factory Management Library</span></span><br/><br/><span data-ttu-id="9eb77-121">Install-Package Microsoft.Azure.Management.DataFactories</span><span class="sxs-lookup"><span data-stu-id="9eb77-121">Install-Package Microsoft.Azure.Management.DataFactories</span></span> |[<span data-ttu-id="9eb77-122">.NET SDK-naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="9eb77-122">.NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt415893.aspx) |
| <span data-ttu-id="9eb77-123">REST API</span><span class="sxs-lookup"><span data-stu-id="9eb77-123">REST API</span></span> |<span data-ttu-id="9eb77-124">U kunt de REST-API van Data Factory maken, bewaken en beheren van Azure data Factory.</span><span class="sxs-lookup"><span data-stu-id="9eb77-124">You can use the Data Factory REST API to create, monitor, and manage Azure data factories.</span></span> |[<span data-ttu-id="9eb77-125">Naslaginformatie over REST-API</span><span class="sxs-lookup"><span data-stu-id="9eb77-125">REST API Reference</span></span>](https://msdn.microsoft.com/library/dn906738.aspx) |

