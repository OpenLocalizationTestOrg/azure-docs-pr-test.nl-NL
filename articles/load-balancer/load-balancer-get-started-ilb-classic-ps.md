---
title: een Azure-interne aaaCreate de load balancer - klassieke PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate een interne netwerktaakverdeler met PowerShell in het klassieke implementatiemodel Hallo
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Aan de slag met het maken van een interne load balancer (klassiek) met behulp van PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Cloudservices](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).  In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Een interne load balancer-set maken voor virtuele machines

toocreate een interne load balancer ingesteld en Hallo servers die hun tooit verkeer wordt verzonden, hebt u toodo Hallo volgende:

1. Een instantie van de interne Load Balancing die Hallo-eindpunt van het binnenkomende verkeer toobe gelijkmatig verdeeld zijn over Hallo-servers van een set met gelijke taakverdeling maken.
2. Het toevoegen van eindpunten overeenkomt toohello virtuele machines die Hallo binnenkomend verkeer ontvangt.
3. Hallo-servers die worden verzonden hello verkeer toobe met gelijke taakverdeling toosend hun verkeer toohello virtuele IP-adres (VIP) van Hallo interne Load Balancing-exemplaar te configureren.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Stap 1: Een exemplaar van Interne taakverdeling maken

Voor een bestaande cloudservice of een cloudservice die onder een regionaal virtueel netwerk is geïmplementeerd, kunt u een interne Load Balancing-exemplaar met de volgende Windows PowerShell-opdrachten Hallo:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Houd er rekening mee dat dit gebruik van Hallo [toevoegen AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) hello DefaultProbe parameterset maakt gebruik van Windows PowerShell-cmdlet. Zie [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) voor meer informatie over aanvullende parametersets.

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Stap 2: Eindpunten toohello interne Load Balancing exemplaar toevoegen

Hier volgt een voorbeeld:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Stap 3: Uw servers toosend hun verkeer toohello nieuwe interne Load Balancing-eindpunt configureren

U hebt Hallo-servers waarvan het verkeer is gaat toobe taakverdeling toouse Hallo nieuwe IP-adres (VIP hello) Hallo exemplaar interne Load Balancing te configureren. Dit is Hallo adres welke Hallo interne Load Balancing exemplaar luistert. In de meeste gevallen moet u toojust toevoegen of wijzigen van een DNS-record voor Hallo VIP van Hallo interne Load Balancing-exemplaar.

Als u Hallo IP-adres tijdens het maken van interne Load Balancing Hallo-exemplaar hello opgegeven, hebt u al Hallo VIP. Anders kunt u het VIP van de volgende opdrachten Hallo Hallo zien:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse deze opdrachten Hallo waarden en invullen verwijderen Hallo < en >. Hier volgt een voorbeeld:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

Uit Hallo weergave van de opdracht Get-AzureInternalLoadBalancer hello, houd er rekening mee Hallo IP-adres en zorg Hallo noodzakelijke wijzigingen tooyour servers of DNS-records tooensure die verkeer toohello VIP wordt verzonden.

> [!NOTE]
> Hallo Microsoft Azure-platform gebruikt een statisch, openbaar routeerbare IPv4-adres voor een verscheidenheid aan scenario's voor beheer. Hallo IP-adres is 168.63.129.16. Dit IP-adres mag niet door firewalls worden geblokkeerd. Dit kan onverwacht gedrag veroorzaken.
> Met de tooAzure ten opzichte van interne Load Balancing, wordt dit IP-adres gebruikt door de bewaking van de tests uit Hallo load balancer toodetermine Hallo-status voor virtuele machines in een set met gelijke taakverdeling. Als een Netwerkbeveiligingsgroep gebruikte toorestrict verkeer tooAzure virtuele machines in een set met gelijke taakverdeling intern is of toegepaste tooa virtueel netwerksubnet, zorg ervoor dat een Netwerkbeveiligingsregel tooallow verkeer vanuit 168.63.129.16 wordt toegevoegd.

## <a name="example-of-internal-load-balancing"></a>Voorbeeld van intern gelijke taakverdeling

toostep die u via Hallo end tooend proces voor het maken van een set taakverdeling voor voorbeeldconfiguraties met twee zien Hallo volgende secties.

### <a name="an-internet-facing-multi-tier-application"></a>Een internetgerichte toepassing met meerdere lagen

Wilt u tooprovide een database-service voor taakverdeling voor een set van internetgerichte webservers. Beide serversets worden gehost in één Azure-cloudservice. Web server verkeer tooTCP poort 1433 moet worden verdeeld over twee virtuele machines in Hallo databaselaag. Afbeelding 1 toont Hallo-configuratie.

![Interne set met taakverdeling voor Hallo databaselaag](./media/load-balancer-internal-getstarted/IC736321.png)

Hallo configuratie bestaat uit de volgende Hallo:

* Hallo bestaande cloudservice hosten van virtuele machines van Hallo heet mytestcloud.
* Hallo twee bestaande database-servers zijn benoemde DB1, DB2.
* Webservers in de weblaag Hallo verbinding toohello databaseservers in Hallo databaselaag via Hallo privé IP-adres. Een andere optie toouse is uw eigen DNS voor Hallo virtueel netwerk en een A-record voor Hallo interne load balancer-set handmatig registreren.

Hallo volgende opdrachten een nieuwe interne taakverdeling exemplaar configureren met de naam **ILBset** en eindpunten toohello virtuele machines overeenkomt toohello twee databaseservers toevoegen:

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>Een configuratie van Interne taakverdeling verwijderen

tooremove een virtuele machine als een eindpunt van een interne load balancer-exemplaar gebruik Hallo volgende opdrachten:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse vult u deze opdrachten Hallo waarden, verwijderen van Hallo < en >.

Hier volgt een voorbeeld:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove een exemplaar van de interne load balancer van een cloudservice, gebruik Hallo volgende opdrachten:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

Deze opdrachten, toouse Hallo-waarde in te vullen en verwijder Hallo < en >.

Hier volgt een voorbeeld:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Meer informatie over cmdlets voor interne load balancers

tooobtain meer informatie over de interne Load Balancing-cmdlets uitvoeren Hallo volgende opdrachten bij de opdrachtprompt van Windows PowerShell:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Volgende stappen

[Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit](load-balancer-distribution-mode.md)

[TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren](load-balancer-tcp-idle-timeout.md)

