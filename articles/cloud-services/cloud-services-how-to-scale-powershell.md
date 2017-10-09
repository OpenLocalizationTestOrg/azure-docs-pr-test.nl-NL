---
title: een Azure-cloud-service in Windows PowerShell aaaScale | Microsoft Docs
description: (klassiek) Meer informatie over hoe toouse PowerShell tooscale een Webrol of worker-rol in of uit in Azure.
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Hoe tooscale een cloud-service in PowerShell

Kunt u Windows PowerShell tooscale een Webrol of worker-rol in- of door toe te voegen of te verwijderen van exemplaren.  

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Voordat u geen bewerkingen uit op uw abonnement via PowerShell uitvoeren kunt, moet u zich aanmeldt:

```powershell
Add-AzureAccount
```

Als u meerdere abonnementen die zijn gekoppeld aan uw account hebt, moet u mogelijk toochange Hallo huidige abonnement, afhankelijk van waar uw cloudservice zich bevindt. toocheck hello huidige abonnement, uitvoeren:

```powershell
Get-AzureSubscription -Current
```

Als u toochange Hallo huidige abonnement moet, uitvoeren:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Hallo huidige aantal exemplaren voor uw rol controleren

toocheck hello huidige status van uw rol uitvoeren:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Ontvangt u informatie over het Hallo-functie, inclusief de huidige OS-versie en exemplaar aantal. In dit geval heeft Hallo rol één exemplaar.

![Informatie over het Hallo-rol](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Hallo rol uitbreiden door meer exemplaren toe te voegen

tooscale uit uw rol pass Hallo gewenst aantal exemplaren als Hallo **aantal** parameter toohello **Set AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

Hallo cmdlet blokken tijdelijk worden tijdens het Hallo nieuwe exemplaren worden ingericht en gestart. Tijdens deze periode, als u een nieuwe PowerShell-venster en aanroep openen **Get-AzureRole** zoals eerder besproken, ziet u de nieuwe doel Hallo-exemplaren. En als u Hallo Rolstatus in Hallo-portal inspecteren, ziet u Hallo nieuw exemplaar gestart:

![VM-instantie in de portal wordt gestart](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Zodra nieuwe exemplaren van Hallo hebt gestart, wordt Hallo cmdlet is geretourneerd:

![Rol exemplaar toename geslaagd](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>In de rol Hallo schalen door het verwijderen van instanties

U kunt schalen in een rol door het verwijderen van instanties in Hallo dezelfde manier. Set Hallo **aantal** parameter op **Set AzureRole** toohello aantal exemplaren dat u wilt toohave nadat Hallo schaal in de bewerking voltooid is.

## <a name="next-steps"></a>Volgende stappen

Het is niet mogelijk tooconfigure automatisch geschaald voor cloudservices van PowerShell. toodo die Zie [hoe tooauto schalen voor een cloudservice](cloud-services-how-to-scale-portal.md).
