---
title: aaaMutiple VIP's voor een cloudservice
description: Overzicht van multiVIP en hoe tooset meerdere VIP's op een cloudservice
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 85f6d26a-3df5-4b8e-96a1-92b2793b5284
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: b3e0f2b24968cb75a7064484a09ffe94505bb70b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a>Meerdere VIP's voor een cloudservice configureren

Azure-cloudservices is toegankelijk via Hallo openbare Internet met behulp van een IP-adres opgegeven door Azure. Dit openbare IP-adres waarnaar wordt verwezen tooas een VIP-adres (virtuele IP) is sinds het is gekoppeld toohello Azure load balancer en niet Hallo exemplaren van de virtuele Machine (VM) binnen het Hallo-cloudservice. Met behulp van een enkele VIP kunt u een VM-instantie binnen een cloudservice openen.

Er zijn echter scenario's waarin u meer dan één VIP moet als een vermelding punt toohello dezelfde cloudservice. Uw cloudservice kan bijvoorbeeld meerdere websites die moeten SSL-verbindingen met Hallo standaardpoort 443, zoals elke site wordt gehost voor een andere klant of tenant te hosten. In dit scenario moet u een ander openbaar internetgerichte IP-adres toohave voor elke website. Hallo onderstaande diagram ziet u een typische multitenant webhosting die een hebben meerdere SSL-certificaten op Hallo dezelfde openbare poort.

![Meerdere VIP SSL-scenario](./media/load-balancer-multivip/Figure1.png)

In voorbeeld hierboven alle VIP's gebruik Hallo Hallo dezelfde openbare poort (443) en verkeer wordt omgeleid tooone of meer load taakverdeling VM's op een unieke particuliere poort voor het interne IP-adres Hallo van Hallo cloudservice die als host fungeert voor alle Hallo websites.

> [!NOTE]
> Een andere situatie vereisen Hallo gebruik Hallo meerdere VIP's als host fungeert voor meerdere SQL AlwaysOn availability group listeners op Hallo dezelfde van virtuele Machines set.

VIP's zijn standaard dynamisch, wat betekent dat Hallo werkelijke toegewezen IP-adres toohello cloudservice na verloop van tijd kan worden gewijzigd. tooprevent gebeurt, kunt u een VIP-adres reserveren voor uw service. toolearn meer informatie over gereserveerde VIP's, Zie [gereserveerde openbare IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md).

> [!NOTE]
> Zie [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses/) voor informatie over de prijzen van VIP's en gereserveerde IP-adressen.

U kunt PowerShell tooverify Hallo VIP's die worden gebruikt door uw cloudservices, gebruiken, evenals toevoegen en verwijderen van de VIP's, een VIP-eindpunt tooan koppelen en taakverdeling op een specifieke VIP-adres configureren.

## <a name="limitations"></a>Beperkingen

Op dit moment is meerdere VIP-functionaliteit beperkt toohello volgen scenario's:

* **Alleen IaaS**. U kunt meerdere VIP alleen inschakelen voor cloudservices met virtuele machines. U kunt meerdere VIP niet gebruiken voor PaaS-scenario's met rolinstanties.
* **Alleen PowerShell**. U kunt meerdere VIP alleen beheren met behulp van PowerShell.

Deze beperkingen zijn tijdelijk en kunnen op elk gewenst moment worden gewijzigd. Zorg ervoor dat toorevisit deze pagina tooverify toekomstige wijzigingen.

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a>Hoe tooa tooadd een VIP-cloudservice
een VIP tooadd tooyour service, Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

Deze opdracht geeft u een resultaat vergelijkbaar toohello voorbeeld te volgen:

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a>Hoe tooremove een VIP-adres van een cloudservice
tooyour service tooremove Hallo VIP toegevoegd in Hallo voorbeeld hierboven uitvoeren Hallo volgende PowerShell-opdracht:

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> U kunt alleen een VIP-adres verwijderen als er geen tooit eindpunten die zijn gekoppeld.


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a>Hoe VIP tooretrieve gegevens van een Cloudservice
tooretrieve hello VIP's die zijn gekoppeld aan een cloudservice, Hallo volgende PowerShell-script uitvoeren:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

Hallo-script wordt een resultaat vergelijkbaar toohello voorbeeld te volgen:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

In dit voorbeeld heeft de service in de cloud Hallo 3 VIP's:

* **Vip1** is standaard VIP hello, u weet dat omdat Hallo-waarde voor IsDnsProgrammedName tootrue is ingesteld.
* **Vip2** en **Vip3** niet als er geen IP-adressen worden gebruikt. Deze wordt alleen gebruikt als u een eindpunt toohello VIP koppelt.

> [!NOTE]
> Uw abonnement wordt alleen in rekening gebracht voor extra VIP's zodra ze gekoppeld aan een eindpunt zijn. Zie voor meer informatie over prijzen [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses/).

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a>Hoe een VIP tooassociate tooan eindpunt

tooassociate een VIP-adres op een cloud service tooan-eindpunt, Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

Hallo opdracht maakt u een eindpunt gekoppelde toohello VIP aangeroepen *Vip2* op poort *80*, en koppelt dat de virtuele machine met de naam toohello *myVM1* in een cloudservice met de naam  *MijnService* met *TCP* op poort *8080*.

tooverify hello configuratie, Hallo volgende PowerShell-opdracht uitvoeren:

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:

    Address         : 191.238.74.148
    IsDnsProgrammed : True
    Name            : Vip1
    ReservedIPName  :
    ExtensionData   :

    Address         : 191.238.74.13
    IsDnsProgrammed :
    Name            : Vip2
    ReservedIPName  :
    ExtensionData   :

    Address         :
    IsDnsProgrammed :
    Name            : Vip3
    ReservedIPName  :
    ExtensionData   :

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a>Hoe tooenable taakverdeling op een specifieke VIP-adres

U kunt een enkel VIP koppelen aan meerdere virtuele machines voor load balancing-doeleinden. Bijvoorbeeld: u hebt een cloudservice met de naam *MijnService*, en twee virtuele machines met de naam *myVM1* en *myVM2*. En uw cloudservice heeft meerdere VIP's, een van deze met de naam *Vip2*. Als u wilt dat alle verkeer tooport tooensure *81* op *Vip2* wordt verdeeld tussen *myVM1* en *myVM2* op poort *8181* , voert hello volgende PowerShell-script:

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

U kunt ook de load balancer toouse een andere VIP bijwerken. Als u Hallo onderstaande PowerShell-opdracht uitvoert, wordt u bijvoorbeeld set toouse een VIP Vip1 met de naam van de taakverdeling Hallo wijzigen:

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a>Volgende stappen

[Taakverdeling van de Azure-logboekanalyse](load-balancer-monitor-log.md)

[Internet gerichte load balancer-overzicht](load-balancer-internet-overview.md)

[Aan de slag op Internet gerichte load balancer](load-balancer-get-started-internet-arm-ps.md)

[Overzicht van Virtual Network](../virtual-network/virtual-networks-overview.md)

[Gereserveerd IP-adres REST-API 's](https://msdn.microsoft.com/library/azure/dn722420.aspx)
