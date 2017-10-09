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
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a><span data-ttu-id="eff32-103">Aan de slag met het maken van een interne load balancer (klassiek) met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="eff32-103">Get started creating an internal load balancer (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eff32-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eff32-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="eff32-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eff32-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="eff32-106">Cloudservices</span><span class="sxs-lookup"><span data-stu-id="eff32-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="eff32-107">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eff32-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="eff32-108">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="eff32-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="eff32-109">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eff32-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="eff32-110">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="eff32-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="eff32-111">Een interne load balancer-set maken voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="eff32-111">Create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="eff32-112">toocreate een interne load balancer ingesteld en Hallo servers die hun tooit verkeer wordt verzonden, hebt u toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="eff32-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you have toodo hello following:</span></span>

1. <span data-ttu-id="eff32-113">Een instantie van de interne Load Balancing die Hallo-eindpunt van het binnenkomende verkeer toobe gelijkmatig verdeeld zijn over Hallo-servers van een set met gelijke taakverdeling maken.</span><span class="sxs-lookup"><span data-stu-id="eff32-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="eff32-114">Het toevoegen van eindpunten overeenkomt toohello virtuele machines die Hallo binnenkomend verkeer ontvangt.</span><span class="sxs-lookup"><span data-stu-id="eff32-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="eff32-115">Hallo-servers die worden verzonden hello verkeer toobe met gelijke taakverdeling toosend hun verkeer toohello virtuele IP-adres (VIP) van Hallo interne Load Balancing-exemplaar te configureren.</span><span class="sxs-lookup"><span data-stu-id="eff32-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

### <a name="step-1-create-an-internal-load-balancing-instance"></a><span data-ttu-id="eff32-116">Stap 1: Een exemplaar van Interne taakverdeling maken</span><span class="sxs-lookup"><span data-stu-id="eff32-116">Step 1: Create an Internal Load Balancing instance</span></span>

<span data-ttu-id="eff32-117">Voor een bestaande cloudservice of een cloudservice die onder een regionaal virtueel netwerk is geïmplementeerd, kunt u een interne Load Balancing-exemplaar met de volgende Windows PowerShell-opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="eff32-117">For an existing cloud service or a cloud service deployed under a regional virtual network, you can create an Internal Load Balancing instance with hello following Windows PowerShell commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

<span data-ttu-id="eff32-118">Houd er rekening mee dat dit gebruik van Hallo [toevoegen AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) hello DefaultProbe parameterset maakt gebruik van Windows PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eff32-118">Note that this use of hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Windows PowerShell cmdlet uses hello DefaultProbe parameter set.</span></span> <span data-ttu-id="eff32-119">Zie [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) voor meer informatie over aanvullende parametersets.</span><span class="sxs-lookup"><span data-stu-id="eff32-119">For more information on additional parameter sets, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).</span></span>

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a><span data-ttu-id="eff32-120">Stap 2: Eindpunten toohello interne Load Balancing exemplaar toevoegen</span><span class="sxs-lookup"><span data-stu-id="eff32-120">Step 2: Add endpoints toohello Internal Load Balancing instance</span></span>

<span data-ttu-id="eff32-121">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eff32-121">Here is an example:</span></span>

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

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a><span data-ttu-id="eff32-122">Stap 3: Uw servers toosend hun verkeer toohello nieuwe interne Load Balancing-eindpunt configureren</span><span class="sxs-lookup"><span data-stu-id="eff32-122">Step 3: Configure your servers toosend their traffic toohello new Internal Load Balancing endpoint</span></span>

<span data-ttu-id="eff32-123">U hebt Hallo-servers waarvan het verkeer is gaat toobe taakverdeling toouse Hallo nieuwe IP-adres (VIP hello) Hallo exemplaar interne Load Balancing te configureren.</span><span class="sxs-lookup"><span data-stu-id="eff32-123">You have too configure hello servers whose traffic is going toobe load balanced toouse hello new IP address (hello VIP) of hello Internal Load Balancing instance.</span></span> <span data-ttu-id="eff32-124">Dit is Hallo adres welke Hallo interne Load Balancing exemplaar luistert.</span><span class="sxs-lookup"><span data-stu-id="eff32-124">This is hello address on which hello Internal Load Balancing instance is listening.</span></span> <span data-ttu-id="eff32-125">In de meeste gevallen moet u toojust toevoegen of wijzigen van een DNS-record voor Hallo VIP van Hallo interne Load Balancing-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="eff32-125">In most cases, you need toojust add or modify a DNS record for hello VIP of hello Internal Load Balancing instance.</span></span>

<span data-ttu-id="eff32-126">Als u Hallo IP-adres tijdens het maken van interne Load Balancing Hallo-exemplaar hello opgegeven, hebt u al Hallo VIP.</span><span class="sxs-lookup"><span data-stu-id="eff32-126">If you specified hello IP address during hello creation of hello Internal Load Balancing instance, you already have hello VIP.</span></span> <span data-ttu-id="eff32-127">Anders kunt u het VIP van de volgende opdrachten Hallo Hallo zien:</span><span class="sxs-lookup"><span data-stu-id="eff32-127">Otherwise, you can see hello VIP from hello following commands:</span></span>

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="eff32-128">toouse deze opdrachten Hallo waarden en invullen verwijderen Hallo < en >.</span><span class="sxs-lookup"><span data-stu-id="eff32-128">toouse these commands, fill in hello values and remove hello < and >.</span></span> <span data-ttu-id="eff32-129">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eff32-129">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

<span data-ttu-id="eff32-130">Uit Hallo weergave van de opdracht Get-AzureInternalLoadBalancer hello, houd er rekening mee Hallo IP-adres en zorg Hallo noodzakelijke wijzigingen tooyour servers of DNS-records tooensure die verkeer toohello VIP wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="eff32-130">From hello display of hello Get-AzureInternalLoadBalancer command, note hello IP address and make hello necessary changes tooyour servers or DNS records tooensure that traffic gets sent toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="eff32-131">Hallo Microsoft Azure-platform gebruikt een statisch, openbaar routeerbare IPv4-adres voor een verscheidenheid aan scenario's voor beheer.</span><span class="sxs-lookup"><span data-stu-id="eff32-131">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="eff32-132">Hallo IP-adres is 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="eff32-132">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="eff32-133">Dit IP-adres mag niet door firewalls worden geblokkeerd. Dit kan onverwacht gedrag veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="eff32-133">This IP address should not be blocked by any firewalls, because it can cause unexpected behavior.</span></span>
> <span data-ttu-id="eff32-134">Met de tooAzure ten opzichte van interne Load Balancing, wordt dit IP-adres gebruikt door de bewaking van de tests uit Hallo load balancer toodetermine Hallo-status voor virtuele machines in een set met gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="eff32-134">With respect tooAzure Internal Load Balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load balanced set.</span></span> <span data-ttu-id="eff32-135">Als een Netwerkbeveiligingsgroep gebruikte toorestrict verkeer tooAzure virtuele machines in een set met gelijke taakverdeling intern is of toegepaste tooa virtueel netwerksubnet, zorg ervoor dat een Netwerkbeveiligingsregel tooallow verkeer vanuit 168.63.129.16 wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="eff32-135">If a Network Security Group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa Virtual Network Subnet, ensure that a Network Security Rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="example-of-internal-load-balancing"></a><span data-ttu-id="eff32-136">Voorbeeld van intern gelijke taakverdeling</span><span class="sxs-lookup"><span data-stu-id="eff32-136">Example of internal load balancing</span></span>

<span data-ttu-id="eff32-137">toostep die u via Hallo end tooend proces voor het maken van een set taakverdeling voor voorbeeldconfiguraties met twee zien Hallo volgende secties.</span><span class="sxs-lookup"><span data-stu-id="eff32-137">toostep you through hello end-tooend process of creating a load-balanced set for two example configurations, see hello following sections.</span></span>

### <a name="an-internet-facing-multi-tier-application"></a><span data-ttu-id="eff32-138">Een internetgerichte toepassing met meerdere lagen</span><span class="sxs-lookup"><span data-stu-id="eff32-138">An Internet facing, multi-tier application</span></span>

<span data-ttu-id="eff32-139">Wilt u tooprovide een database-service voor taakverdeling voor een set van internetgerichte webservers.</span><span class="sxs-lookup"><span data-stu-id="eff32-139">You want tooprovide a load balanced database service for  a set of Internet-facing web servers.</span></span> <span data-ttu-id="eff32-140">Beide serversets worden gehost in één Azure-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="eff32-140">Both sets of servers are hosted in a single Azure cloud service.</span></span> <span data-ttu-id="eff32-141">Web server verkeer tooTCP poort 1433 moet worden verdeeld over twee virtuele machines in Hallo databaselaag.</span><span class="sxs-lookup"><span data-stu-id="eff32-141">Web server traffic tooTCP port 1433 must be distributed among two virtual machines in hello database tier.</span></span> <span data-ttu-id="eff32-142">Afbeelding 1 toont Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="eff32-142">Figure 1 shows hello configuration.</span></span>

![Interne set met taakverdeling voor Hallo databaselaag](./media/load-balancer-internal-getstarted/IC736321.png)

<span data-ttu-id="eff32-144">Hallo configuratie bestaat uit de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="eff32-144">hello configuration consists of hello following:</span></span>

* <span data-ttu-id="eff32-145">Hallo bestaande cloudservice hosten van virtuele machines van Hallo heet mytestcloud.</span><span class="sxs-lookup"><span data-stu-id="eff32-145">hello existing cloud service hosting hello virtual machines is named mytestcloud.</span></span>
* <span data-ttu-id="eff32-146">Hallo twee bestaande database-servers zijn benoemde DB1, DB2.</span><span class="sxs-lookup"><span data-stu-id="eff32-146">hello two existing database servers are named DB1, DB2.</span></span>
* <span data-ttu-id="eff32-147">Webservers in de weblaag Hallo verbinding toohello databaseservers in Hallo databaselaag via Hallo privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="eff32-147">Web servers in hello web tier connect toohello database servers in hello database tier by using hello private IP address.</span></span> <span data-ttu-id="eff32-148">Een andere optie toouse is uw eigen DNS voor Hallo virtueel netwerk en een A-record voor Hallo interne load balancer-set handmatig registreren.</span><span class="sxs-lookup"><span data-stu-id="eff32-148">Another option is toouse your own DNS for hello virtual network and manually register an A record for hello internal load balancer set.</span></span>

<span data-ttu-id="eff32-149">Hallo volgende opdrachten een nieuwe interne taakverdeling exemplaar configureren met de naam **ILBset** en eindpunten toohello virtuele machines overeenkomt toohello twee databaseservers toevoegen:</span><span class="sxs-lookup"><span data-stu-id="eff32-149">hello following commands configure a new Internal Load Balancing instance named **ILBset** and add endpoints toohello virtual machines corresponding toohello two database servers:</span></span>

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

## <a name="remove-an-internal-load-balancing-configuration"></a><span data-ttu-id="eff32-150">Een configuratie van Interne taakverdeling verwijderen</span><span class="sxs-lookup"><span data-stu-id="eff32-150">Remove an Internal Load Balancing configuration</span></span>

<span data-ttu-id="eff32-151">tooremove een virtuele machine als een eindpunt van een interne load balancer-exemplaar gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="eff32-151">tooremove a virtual machine as an endpoint from an internal load balancer instance, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="eff32-152">toouse vult u deze opdrachten Hallo waarden, verwijderen van Hallo < en >.</span><span class="sxs-lookup"><span data-stu-id="eff32-152">toouse these commands, fill in hello values, removing hello < and >.</span></span>

<span data-ttu-id="eff32-153">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eff32-153">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

<span data-ttu-id="eff32-154">tooremove een exemplaar van de interne load balancer van een cloudservice, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="eff32-154">tooremove an internal load balancer instance from a cloud service, use hello following commands:</span></span>

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

<span data-ttu-id="eff32-155">Deze opdrachten, toouse Hallo-waarde in te vullen en verwijder Hallo < en >.</span><span class="sxs-lookup"><span data-stu-id="eff32-155">toouse these commands, fill in hello value and remove hello < and >.</span></span>

<span data-ttu-id="eff32-156">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eff32-156">Here is an example:</span></span>

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a><span data-ttu-id="eff32-157">Meer informatie over cmdlets voor interne load balancers</span><span class="sxs-lookup"><span data-stu-id="eff32-157">Additional information about internal load balancer cmdlets</span></span>

<span data-ttu-id="eff32-158">tooobtain meer informatie over de interne Load Balancing-cmdlets uitvoeren Hallo volgende opdrachten bij de opdrachtprompt van Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="eff32-158">tooobtain additional information about Internal Load Balancing cmdlets, run hello following commands at a Windows PowerShell prompt:</span></span>

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a><span data-ttu-id="eff32-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eff32-159">Next steps</span></span>

[<span data-ttu-id="eff32-160">Een distributiemodus voor de load balancer configureren met bron-IP-affiniteit</span><span class="sxs-lookup"><span data-stu-id="eff32-160">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="eff32-161">TCP-time-outinstellingen voor inactiviteit voor de load balancer configureren</span><span class="sxs-lookup"><span data-stu-id="eff32-161">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

