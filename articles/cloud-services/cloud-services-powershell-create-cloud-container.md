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
# <a name="use-an-azure-powershell-command-toocreate-an-empty-cloud-service-container"></a>Een Azure PowerShell-opdracht toocreate een leeg cloud service-container gebruiken
Dit artikel wordt uitgelegd hoe tooquickly maken voor een Cloud Services-container met Azure PowerShell-cmdlets. Volg onderstaande stappen voor Hallo:

1. Hallo Microsoft Azure PowerShell-cmdlet installeren vanaf Hallo [Azure PowerShell downloadt](http://aka.ms/webpi-azps) pagina.
2. Open Hallo PowerShell-opdrachtprompt.
3. Gebruik Hallo [Add-AzureAccount](https://msdn.microsoft.com/library/dn495128.aspx) toosign in.

   > [!NOTE]
   > Raadpleeg te voor verdere instructies over het installeren van hello Azure PowerShell-cmdlet en verbinding maken met Azure-abonnement tooyour[hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
   >
   >
4. Gebruik Hallo **New-AzureService** cmdlet toocreate een leeg Azure cloud service-container.

    ```
    New-AzureService [-ServiceName] <String> [-AffinityGroup] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
    New-AzureService [-ServiceName] <String> [-Location] <String> [[-Label] <String>] [[-Description] <String>] [[-ReverseDnsFqdn] <String>] [<CommonParameters>]
   ```
5. Ga als volgt in dit voorbeeld tooinvoke Hallo-cmdlet:

   ```
   New-AzureService -ServiceName "mytestcloudservice" -Location "Central US" -Label "mytestcloudservice"
   ```

Voor meer informatie over het maken van hello Azure cloudservice uitvoeren:

```
Get-help New-AzureService
```

### <a name="next-steps"></a>Volgende stappen
* toomanage hello cloud service-implementatie, raadpleeg dan toohello [Get-AzureService](https://msdn.microsoft.com/library/azure/dn495131.aspx), [Remove-AzureService](https://msdn.microsoft.com/library/azure/dn495120.aspx), en [Set-AzureService](https://msdn.microsoft.com/library/azure/dn495242.aspx) opdrachten. U kunt ook te verwijzen[hoe tooconfigure cloudservices](cloud-services-how-to-configure.md) voor meer informatie.
* toopublish uw cloudservice tooAzure project, raadpleegt u toohello **PublishCloudService.ps1** codevoorbeeld van [continue leveringsmethode voor de cloudservice in Azure](cloud-services-dotnet-continuous-delivery.md).
