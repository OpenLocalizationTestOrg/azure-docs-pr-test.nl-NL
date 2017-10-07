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
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="788f2-103">Meerdere VIP's voor een cloudservice configureren</span><span class="sxs-lookup"><span data-stu-id="788f2-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="788f2-104">Azure-cloudservices is toegankelijk via Hallo openbare Internet met behulp van een IP-adres opgegeven door Azure.</span><span class="sxs-lookup"><span data-stu-id="788f2-104">You can access Azure cloud services over hello public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="788f2-105">Dit openbare IP-adres waarnaar wordt verwezen tooas een VIP-adres (virtuele IP) is sinds het is gekoppeld toohello Azure load balancer en niet Hallo exemplaren van de virtuele Machine (VM) binnen het Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="788f2-105">This public IP address is referred tooas a VIP (virtual IP) since it is linked toohello Azure load balancer, and not hello Virtual Machine (VM) instances within hello cloud service.</span></span> <span data-ttu-id="788f2-106">Met behulp van een enkele VIP kunt u een VM-instantie binnen een cloudservice openen.</span><span class="sxs-lookup"><span data-stu-id="788f2-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="788f2-107">Er zijn echter scenario's waarin u meer dan één VIP moet als een vermelding punt toohello dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="788f2-107">However, there are scenarios in which you may need more than one VIP as an entry point toohello same cloud service.</span></span> <span data-ttu-id="788f2-108">Uw cloudservice kan bijvoorbeeld meerdere websites die moeten SSL-verbindingen met Hallo standaardpoort 443, zoals elke site wordt gehost voor een andere klant of tenant te hosten.</span><span class="sxs-lookup"><span data-stu-id="788f2-108">For instance, your cloud service may host multiple websites that require SSL connectivity using hello default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="788f2-109">In dit scenario moet u een ander openbaar internetgerichte IP-adres toohave voor elke website.</span><span class="sxs-lookup"><span data-stu-id="788f2-109">In this scenario, you need toohave a different public facing IP address for each website.</span></span> <span data-ttu-id="788f2-110">Hallo onderstaande diagram ziet u een typische multitenant webhosting die een hebben meerdere SSL-certificaten op Hallo dezelfde openbare poort.</span><span class="sxs-lookup"><span data-stu-id="788f2-110">hello diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on hello same public port.</span></span>

![Meerdere VIP SSL-scenario](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="788f2-112">In voorbeeld hierboven alle VIP's gebruik Hallo Hallo dezelfde openbare poort (443) en verkeer wordt omgeleid tooone of meer load taakverdeling VM's op een unieke particuliere poort voor het interne IP-adres Hallo van Hallo cloudservice die als host fungeert voor alle Hallo websites.</span><span class="sxs-lookup"><span data-stu-id="788f2-112">In hello example above, all VIPs use hello same public port (443) and traffic is redirected tooone or more load balanced VMs on a unique private port for hello internal IP address of hello cloud service hosting all hello websites.</span></span>

> [!NOTE]
> <span data-ttu-id="788f2-113">Een andere situatie vereisen Hallo gebruik Hallo meerdere VIP's als host fungeert voor meerdere SQL AlwaysOn availability group listeners op Hallo dezelfde van virtuele Machines set.</span><span class="sxs-lookup"><span data-stu-id="788f2-113">Another situation requiring hello use hello multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on hello same set of Virtual Machines.</span></span>

<span data-ttu-id="788f2-114">VIP's zijn standaard dynamisch, wat betekent dat Hallo werkelijke toegewezen IP-adres toohello cloudservice na verloop van tijd kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="788f2-114">VIPs are dynamic by default, which means that hello actual IP address assigned toohello cloud service may change over time.</span></span> <span data-ttu-id="788f2-115">tooprevent gebeurt, kunt u een VIP-adres reserveren voor uw service.</span><span class="sxs-lookup"><span data-stu-id="788f2-115">tooprevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="788f2-116">toolearn meer informatie over gereserveerde VIP's, Zie [gereserveerde openbare IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="788f2-116">toolearn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="788f2-117">Zie [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses/) voor informatie over de prijzen van VIP's en gereserveerde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="788f2-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="788f2-118">U kunt PowerShell tooverify Hallo VIP's die worden gebruikt door uw cloudservices, gebruiken, evenals toevoegen en verwijderen van de VIP's, een VIP-eindpunt tooan koppelen en taakverdeling op een specifieke VIP-adres configureren.</span><span class="sxs-lookup"><span data-stu-id="788f2-118">You can use PowerShell tooverify hello VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP tooan endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="788f2-119">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="788f2-119">Limitations</span></span>

<span data-ttu-id="788f2-120">Op dit moment is meerdere VIP-functionaliteit beperkt toohello volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="788f2-120">At this time, Multi VIP functionality is limited toohello following scenarios:</span></span>

* <span data-ttu-id="788f2-121">**Alleen IaaS**.</span><span class="sxs-lookup"><span data-stu-id="788f2-121">**IaaS only**.</span></span> <span data-ttu-id="788f2-122">U kunt meerdere VIP alleen inschakelen voor cloudservices met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="788f2-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="788f2-123">U kunt meerdere VIP niet gebruiken voor PaaS-scenario's met rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="788f2-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="788f2-124">**Alleen PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="788f2-124">**PowerShell only**.</span></span> <span data-ttu-id="788f2-125">U kunt meerdere VIP alleen beheren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="788f2-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="788f2-126">Deze beperkingen zijn tijdelijk en kunnen op elk gewenst moment worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="788f2-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="788f2-127">Zorg ervoor dat toorevisit deze pagina tooverify toekomstige wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="788f2-127">Make sure toorevisit this page tooverify future changes.</span></span>

## <a name="how-tooadd-a-vip-tooa-cloud-service"></a><span data-ttu-id="788f2-128">Hoe tooa tooadd een VIP-cloudservice</span><span class="sxs-lookup"><span data-stu-id="788f2-128">How tooadd a VIP tooa cloud service</span></span>
<span data-ttu-id="788f2-129">een VIP tooadd tooyour service, Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="788f2-129">tooadd a VIP tooyour service, run hello following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="788f2-130">Deze opdracht geeft u een resultaat vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="788f2-130">This command displays a result similar toohello following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-tooremove-a-vip-from-a-cloud-service"></a><span data-ttu-id="788f2-131">Hoe tooremove een VIP-adres van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="788f2-131">How tooremove a VIP from a cloud service</span></span>
<span data-ttu-id="788f2-132">tooyour service tooremove Hallo VIP toegevoegd in Hallo voorbeeld hierboven uitvoeren Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="788f2-132">tooremove hello VIP added tooyour service in hello example above, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="788f2-133">U kunt alleen een VIP-adres verwijderen als er geen tooit eindpunten die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="788f2-133">You can only remove a VIP if it has no endpoints associated tooit.</span></span>


## <a name="how-tooretrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="788f2-134">Hoe VIP tooretrieve gegevens van een Cloudservice</span><span class="sxs-lookup"><span data-stu-id="788f2-134">How tooretrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="788f2-135">tooretrieve hello VIP's die zijn gekoppeld aan een cloudservice, Hallo volgende PowerShell-script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="788f2-135">tooretrieve hello VIPs associated with a cloud service, run hello following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="788f2-136">Hallo-script wordt een resultaat vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="788f2-136">hello script displays a result similar toohello following sample:</span></span>

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

<span data-ttu-id="788f2-137">In dit voorbeeld heeft de service in de cloud Hallo 3 VIP's:</span><span class="sxs-lookup"><span data-stu-id="788f2-137">In this example, hello cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="788f2-138">**Vip1** is standaard VIP hello, u weet dat omdat Hallo-waarde voor IsDnsProgrammedName tootrue is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="788f2-138">**Vip1** is hello default VIP, you know that because hello value for IsDnsProgrammedName is set tootrue.</span></span>
* <span data-ttu-id="788f2-139">**Vip2** en **Vip3** niet als er geen IP-adressen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="788f2-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="788f2-140">Deze wordt alleen gebruikt als u een eindpunt toohello VIP koppelt.</span><span class="sxs-lookup"><span data-stu-id="788f2-140">They will only be used if you associate an endpoint toohello VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="788f2-141">Uw abonnement wordt alleen in rekening gebracht voor extra VIP's zodra ze gekoppeld aan een eindpunt zijn.</span><span class="sxs-lookup"><span data-stu-id="788f2-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="788f2-142">Zie voor meer informatie over prijzen [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="788f2-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-tooassociate-a-vip-tooan-endpoint"></a><span data-ttu-id="788f2-143">Hoe een VIP tooassociate tooan eindpunt</span><span class="sxs-lookup"><span data-stu-id="788f2-143">How tooassociate a VIP tooan endpoint</span></span>

<span data-ttu-id="788f2-144">tooassociate een VIP-adres op een cloud service tooan-eindpunt, Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="788f2-144">tooassociate a VIP on a cloud service tooan endpoint, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="788f2-145">Hallo opdracht maakt u een eindpunt gekoppelde toohello VIP aangeroepen *Vip2* op poort *80*, en koppelt dat de virtuele machine met de naam toohello *myVM1* in een cloudservice met de naam  *MijnService* met *TCP* op poort *8080*.</span><span class="sxs-lookup"><span data-stu-id="788f2-145">hello command creates an endpoint linked toohello VIP called *Vip2* on port *80*, and links it toohello VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="788f2-146">tooverify hello configuratie, Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="788f2-146">tooverify hello configuration, run hello following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="788f2-147">Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="788f2-147">hello output looks similar toohello following example:</span></span>

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

## <a name="how-tooenable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="788f2-148">Hoe tooenable taakverdeling op een specifieke VIP-adres</span><span class="sxs-lookup"><span data-stu-id="788f2-148">How tooenable load balancing on a specific VIP</span></span>

<span data-ttu-id="788f2-149">U kunt een enkel VIP koppelen aan meerdere virtuele machines voor load balancing-doeleinden.</span><span class="sxs-lookup"><span data-stu-id="788f2-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="788f2-150">Bijvoorbeeld: u hebt een cloudservice met de naam *MijnService*, en twee virtuele machines met de naam *myVM1* en *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="788f2-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="788f2-151">En uw cloudservice heeft meerdere VIP's, een van deze met de naam *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="788f2-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="788f2-152">Als u wilt dat alle verkeer tooport tooensure *81* op *Vip2* wordt verdeeld tussen *myVM1* en *myVM2* op poort *8181* , voert hello volgende PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="788f2-152">If you want tooensure that all traffic tooport *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run hello following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="788f2-153">U kunt ook de load balancer toouse een andere VIP bijwerken.</span><span class="sxs-lookup"><span data-stu-id="788f2-153">You can also update your load balancer toouse a different VIP.</span></span> <span data-ttu-id="788f2-154">Als u Hallo onderstaande PowerShell-opdracht uitvoert, wordt u bijvoorbeeld set toouse een VIP Vip1 met de naam van de taakverdeling Hallo wijzigen:</span><span class="sxs-lookup"><span data-stu-id="788f2-154">For example, if you run hello PowerShell command below, you will change hello load balancing set toouse a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="788f2-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="788f2-155">Next Steps</span></span>

[<span data-ttu-id="788f2-156">Taakverdeling van de Azure-logboekanalyse</span><span class="sxs-lookup"><span data-stu-id="788f2-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="788f2-157">Internet gerichte load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="788f2-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="788f2-158">Aan de slag op Internet gerichte load balancer</span><span class="sxs-lookup"><span data-stu-id="788f2-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="788f2-159">Overzicht van Virtual Network</span><span class="sxs-lookup"><span data-stu-id="788f2-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="788f2-160">Gereserveerd IP-adres REST-API 's</span><span class="sxs-lookup"><span data-stu-id="788f2-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
