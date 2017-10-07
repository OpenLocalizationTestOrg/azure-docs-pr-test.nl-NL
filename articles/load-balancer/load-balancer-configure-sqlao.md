---
title: aaaConfigure Load balancer voor de SQL AlwaysOn | Microsoft Docs
description: Load balancer toowork configureren met SQL altijd op en hoe tooleverage powershell toocreate load balancer voor Hallo SQL-implementatie
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: d7bc3790-47d3-4e95-887c-c533011e4afd
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: ac6200b18f725dadee2555b80055327d379417d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-load-balancer-for-sql-always-on"></a>Load balancer voor SQL altijd configureren op

SQL Server AlwaysOn-beschikbaarheidsgroepen kan nu worden uitgevoerd met ILB. Beschikbaarheidsgroep is SQL-Server vlaggenschip oplossing voor hoge beschikbaarheid en herstel na noodgevallen. Hallo beschikbaarheidsgroep-Listener clienttoepassingen in staat stelt tooseamlessly verbinding maken met de primaire replica toohello, ongeacht het aantal Hallo replica's in de configuratie van Hallo Hallo.

Hallo-listener (DNS)-naam is toegewezen tooa netwerktaakverdeling IP-adres en Azure load balancer Hallo binnenkomende verkeer tooonly Hallo primaire server stuurt in Hallo replicaset.

U kunt de ILB ondersteuning voor SQL Server AlwaysOn (listener)-eindpunten. U nu hebben controle over Hallo toegankelijkheid van Hallo-listener en Hallo netwerktaakverdeling IP-adres kunt kiezen uit een specifiek subnet in het virtuele netwerk (VNet).

Hallo via ILB Hallo-listener voor SQL server-eindpunt (bijvoorbeeld Server = tcp:ListenerName, 1433; Database = DatabaseName) is alleen toegankelijk is voor:

* Services en virtuele machines in hetzelfde virtuele netwerk Hallo
* Services en virtuele machines van de verbonden on-premises netwerk
* Services en virtuele machines van de VNets met elkaar verbonden

![ILB_SQLAO_NewPic](./media/load-balancer-configure-sqlao/sqlao1.png)

Afbeelding 1: de SQL AlwaysOn is geconfigureerd met Internet gerichte load balancer

## <a name="add-internal-load-balancer-toohello-service"></a>Interne Load Balancer toohello service toevoegen

1. In Hallo voorbeeld te volgen, wordt er een virtueel netwerk met een subnet met de naam Subnet-1 geconfigureerd:

    ```powershell
    Add-AzureInternalLoadBalancer -InternalLoadBalancerName ILB_SQL_AO -SubnetName Subnet-1 -ServiceName SqlSvc
    ```
2. Eindpunten van taakverdeling voor de ILB op elke virtuele machine toevoegen

    ```powershell
    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc1 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -
    DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM

    Get-AzureVM -ServiceName SqlSvc -Name sqlsvc2 | Add-AzureEndpoint -Name "LisEUep" -LBSetName "ILBSet1" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -DirectServerReturn $true -InternalLoadBalancerName ILB_SQL_AO | Update-AzureVM
    ```

    Hallo bovenstaande voorbeeld hebt u 2 VM genoemd 'sqlsvc1' en 'sqlsvc2' wordt uitgevoerd in de cloud Hallo service 'Sqlsvc'. Na het maken van Hallo ILB met `DirectServerReturn` overschakelen, u toevoegen taakverdeling eindpunten toohello ILB tooallow SQL tooconfigure Hallo listeners voor beschikbaarheidsgroepen Hallo laden.

Zie voor meer informatie over SQL AlwaysOn, [een interne load balancer voor een AlwaysOn-beschikbaarheidsgroep configureren in Azure](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

## <a name="see-also"></a>Zie ook
[De load balancer van een Internetgericht configureren aan de slag](load-balancer-get-started-internet-arm-ps.md)

[Een interne load balancer configureren aan de slag](load-balancer-get-started-ilb-arm-ps.md)

[Een distributiemodus voor de load balancer configureren](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)
