---
title: Azure PowerShell-klassiek de load balancer - aaaCreate een internetgerichte | Microsoft Docs
description: Meer informatie over hoe de toocreate een Internet gerichte load balancer in de klassieke modus met behulp van PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Aan de slag met het maken van een internetgerichte load balancer (klassiek) in PowerShell

> [!div class="op_single_selector"]
> * [klassieke Azure-portal](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Voordat u met Azure-resources werkt, is het belangrijk toounderstand dat Azure momenteel twee implementatiemodellen heeft: Azure Resource Manager en het klassieke model. Zorg ervoor dat u begrijpt wat [implementatiemodellen en hulpprogramma's](../azure-classic-rm.md) zijn voordat u met een Azure-resource gaat werken. U kunt Hallo-documentatie voor verschillende hulpprogramma's bekijken door te klikken op de tabbladen Hallo Hallo boven aan dit artikel. In dit artikel bevat informatie over Hallo klassieke implementatiemodel. U kunt ook [meer informatie over hoe een internetverbinding toocreate netwerktaakverdeler met Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Een load balancer instellen met behulp van PowerShell

tooset van een load balancer met behulp van powershell, Hallo volgende stappen:

1. Als u Azure PowerShell nog nooit hebt gebruikt, raadpleegt u [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) en volg de instructies Hallo alle Hallo manier toohello toosign beëindigen in Azure en uw abonnement te selecteren.
2. Nadat een virtuele machine is gemaakt, kunt u PowerShell-cmdlets tooadd een load balancer tooa virtuele machine binnen Hallo dezelfde cloudservice.

In Hallo naam volgende voorbeeld voegt u toe een load balancer-set aangeroepen toocloud 'webfarm' service 'mytestcloud' (of myctestcloud.cloudapp.net) toe te voegen Hallo eindpunten voor Hallo load balancer toovirtual machines 'web1' en 'web2'. Hallo load balancer ontvangt netwerkverkeer op poort 80 en een compromis tussen de werklast tussen Hallo virtuele machines zijn gedefinieerd door het lokale eindpunt hello (in dit geval poort 80) via TCP.

### <a name="step-1"></a>Stap 1

Een eindpunt van de taakverdeling voor de eerste VM 'web1' hello maken

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Stap 2

Maken van een ander eindpunt voor hello tweede VM 'web2' hello met dezelfde load balancer setnaam

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Verwijder een virtuele machine uit een load balancer

U kunt verwijderen AzureEndpoint tooremove een eindpunt van de virtuele machine van Hallo load balancer

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Volgende stappen

U kunt ook [aan de slag gaan met het maken van een interne load balancer](load-balancer-get-started-ilb-classic-ps.md) en configureren welk type [distributiemodus](load-balancer-distribution-mode.md) er moet worden gebruikt voor specifiek gedrag voor netwerkverkeer van de load balancer.

Als uw toepassing tookeep verbindingen voor servers achter een load balancer actief is moet, kunt u meer begrip over [inactieve TCP-time-outinstellingen voor een load balancer](load-balancer-tcp-idle-timeout.md). Dit helpt toolearn over niet-actieve Verbindingsgedrag wanneer u van Azure Load Balancer gebruikmaakt.
