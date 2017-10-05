---
title: Een cloud service-container maken met PowerShell | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe u een cloud service-container maken met PowerShell. De container fungeert als host voor web-en werkrollen.
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
ms.openlocfilehash: 2023fa7b318f9f76ce1e1ea0a46110297be9a001
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-an-azure-powershell-command-to-create-an-empty-cloud-service-container"></a><span data-ttu-id="2aaa6-104">Een Azure PowerShell-opdracht gebruiken om te maken van een leeg cloud service-container</span><span class="sxs-lookup"><span data-stu-id="2aaa6-104">Use an Azure PowerShell command to create an empty cloud service container</span></span>
<span data-ttu-id="2aaa6-105">In dit artikel wordt uitgelegd hoe u snel een Cloud-Services en container te maken met Azure PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-105">This article explains how to quickly create a Cloud Services container using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2aaa6-106">Volg de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="2aaa6-106">Please follow the steps below:</span></span>

1. <span data-ttu-id="2aaa6-107">Installeer de Microsoft Azure PowerShell-cmdlet uit de [Azure PowerShell downloadt](http://aka.ms/webpi-azps) pagina.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-107">Install the Microsoft Azure PowerShell cmdlet from the [Azure PowerShell downloads](http://aka.ms/webpi-azps) page.</span></span>
2. <span data-ttu-id="2aaa6-108">Open de PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-108">Open the PowerShell command prompt.</span></span>
3. <span data-ttu-id="2aaa6-109">Gebruik de [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) aan te melden.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-109">Use the [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) to sign in.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2aaa6-110">Raadpleeg voor verdere instructies over het installeren van de Azure PowerShell-cmdlet en verbinding maken met uw Azure-abonnement [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2aaa6-110">For further instruction on installing the Azure PowerShell cmdlet and connecting to your Azure subscription, refer to [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
   >
   >
4. <span data-ttu-id="2aaa6-111">Gebruik de **New-AzureService** cmdlet voor het maken van een leeg Azure cloud service-container.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-111">Use the **New-AzureService** cmdlet to create an empty Azure cloud service container.</span></span>

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. <span data-ttu-id="2aaa6-112">Ga als volgt in dit voorbeeld voor het aanroepen van de cmdlet:</span><span class="sxs-lookup"><span data-stu-id="2aaa6-112">Follow this example to invoke the cmdlet:</span></span>

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

<span data-ttu-id="2aaa6-113">Voor meer informatie over het maken van de Azure-cloud-service worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="2aaa6-113">For more information about creating the Azure cloud service, run:</span></span>

```
Get-help New-AzureService
```

### <a name="next-steps"></a><span data-ttu-id="2aaa6-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2aaa6-114">Next steps</span></span>
* <span data-ttu-id="2aaa6-115">Voor het beheren van de cloud service-implementatie, verwijzen naar de [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), en [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-115">To manage the cloud service deployment, refer to the [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), and [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) commands.</span></span> <span data-ttu-id="2aaa6-116">U kunt ook verwijzen naar [het configureren van cloudservices](cloud-services-how-to-configure.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2aaa6-116">You may also refer to [How to configure cloud services](cloud-services-how-to-configure.md) for further information.</span></span>
* <span data-ttu-id="2aaa6-117">Als u wilt uw cloudserviceproject publiceren naar Azure, verwijzen naar de **PublishCloudService.ps1** codevoorbeeld van [continue leveringsmethode voor de cloudservice in Azure](cloud-services-dotnet-continuous-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="2aaa6-117">To publish your cloud service project to Azure, refer to the  **PublishCloudService.ps1** code sample from [Continuous delivery for cloud service in Azure](cloud-services-dotnet-continuous-delivery.md).</span></span>
