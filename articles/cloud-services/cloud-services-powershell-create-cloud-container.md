---
title: aaaCreate een cloud service-container met PowerShell | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe toocreate een cloud service-container met PowerShell. Hallo-container fungeert als host voor web-en werkrollen.
services: cloud-services
documentationcenter: .net
author: cawaMS
manager: timlt
editor: 
ms.assetid: c8f32469-610e-4f37-a3aa-4fac5c714e13
ms.service: cloud-services
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 4c47b10b5ba1f9cc39594a45cd869bf04fcaadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a><span data-ttu-id="515e3-104">Een Azure PowerShell-opdracht toocreate een leeg cloud service-container gebruiken</span><span class="sxs-lookup"><span data-stu-id="515e3-104">Use an Azure PowerShell command toocreate an empty cloud service container</span></span>
<span data-ttu-id="515e3-105">Dit artikel wordt uitgelegd hoe tooquickly maken voor een Cloud Services-container met Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="515e3-105">This article explains how tooquickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="515e3-106">Volg onderstaande stappen voor Hallo:</span><span class="sxs-lookup"><span data-stu-id="515e3-106">Please follow hello steps below:</span></span>

1. <span data-ttu-id="515e3-107">Hallo Microsoft Azure PowerShell-cmdlet installeren vanaf Hallo [Azure PowerShell downloadt](http://aka.ms/webpi-azps) pagina.</span><span class="sxs-lookup"><span data-stu-id="515e3-107">Install hello Microsoft Azure PowerShell cmdlet from hello [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="515e3-108">Open Hallo PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="515e3-108">Open hello PowerShell command prompt.</span></span>
3. <span data-ttu-id="515e3-109">Gebruik Hallo [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span><span class="sxs-lookup"><span data-stu-id="515e3-109">Use hello [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="515e3-110">Raadpleeg te voor verdere instructies over het installeren van hello Azure PowerShell-cmdlet en verbinding maken met Azure-abonnement tooyour[hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="515e3-110">For further instruction on installing hello Azure PowerShell cmdlet and connecting tooyour Azure subscription, refer too[How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="515e3-111">Gebruik Hallo **New-AzureService** cmdlet toocreate een leeg Azure cloud service-container.</span><span class="sxs-lookup"><span data-stu-id="515e3-111">Use hello **New-AzureService** cmdlet toocreate an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="515e3-112">Ga als volgt in dit voorbeeld tooinvoke Hallo-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="515e3-112">Follow this example tooinvoke hello cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="515e3-113">Voor meer informatie over het maken van hello Azure cloudservice uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="515e3-113">For more information about creating hello Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="515e3-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="515e3-114">Next steps</span></span>
* <span data-ttu-id="515e3-115">toomanage hello cloud service-implementatie, raadpleeg dan toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), en [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) opdrachten.</span><span class="sxs-lookup"><span data-stu-id="515e3-115">toomanage hello cloud service deployment, refer toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="515e3-116">U kunt ook te verwijzen[hoe tooconfigure cloudservices](cloud-services-how-to-configure.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="515e3-116">You may also refer too[How tooconfigure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="515e3-117">toopublish uw cloudservice tooAzure project, raadpleegt u toohello **PublishCloudService.ps1** codevoorbeeld van [continue leveringsmethode voor de cloudservice in Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="515e3-117">toopublish your cloud service project tooAzure, refer toohello  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
