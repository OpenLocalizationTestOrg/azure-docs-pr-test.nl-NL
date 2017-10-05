---
title: Mutiple VIP's voor een cloudservice
description: Overzicht van multiVIP en het instellen van meerdere VIP's op een cloudservice
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
ms.openlocfilehash: f40e0501eed8d5f296e7c79d8a35705a695ae6fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-multiple-vips-for-a-cloud-service"></a><span data-ttu-id="1fcc4-103">Meerdere VIP's voor een cloudservice configureren</span><span class="sxs-lookup"><span data-stu-id="1fcc4-103">Configure multiple VIPs for a cloud service</span></span>

<span data-ttu-id="1fcc4-104">U kunt toegang tot Azure-cloudservices via het openbare Internet met behulp van een IP-adres opgegeven door Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-104">You can access Azure cloud services over the public Internet by using an IP address provided by Azure.</span></span> <span data-ttu-id="1fcc4-105">Dit openbare IP-adres wordt aangeduid als een VIP-adres (virtuele IP) omdat deze is gekoppeld aan de Azure load balancer en geen virtuele Machine (VM) in de cloudservice-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-105">This public IP address is referred to as a VIP (virtual IP) since it is linked to the Azure load balancer, and not the Virtual Machine (VM) instances within the cloud service.</span></span> <span data-ttu-id="1fcc4-106">Met behulp van een enkele VIP kunt u een VM-instantie binnen een cloudservice openen.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-106">You can access any VM instance within a cloud service by using a single VIP.</span></span>

<span data-ttu-id="1fcc4-107">Er zijn echter scenario's waarin u wellicht meer dan een VIP als een vermelding in het verwijzen naar dezelfde cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-107">However, there are scenarios in which you may need more than one VIP as an entry point to the same cloud service.</span></span> <span data-ttu-id="1fcc4-108">Uw cloudservice kan bijvoorbeeld meerdere websites die moeten SSL-verbindingen via de standaardpoort 443, zoals elke site wordt gehost voor een andere klant of tenant te hosten.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-108">For instance, your cloud service may host multiple websites that require SSL connectivity using the default port of 443, as each site is hosted for a different customer, or tenant.</span></span> <span data-ttu-id="1fcc4-109">In dit scenario moet u een andere openbare internetgerichte IP-adres voor elke website.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-109">In this scenario, you need to have a different public facing IP address for each website.</span></span> <span data-ttu-id="1fcc4-110">Het onderstaande diagram ziet u een multitenant Standaardwebthema die als host fungeert voor meerdere SSL-certificaten op dezelfde openbare poort.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-110">The diagram below illustrates a typical multi-tenant web hosting with a need for multiple SSL certificates on the same public port.</span></span>

![Meerdere VIP SSL-scenario](./media/load-balancer-multivip/Figure1.png)

<span data-ttu-id="1fcc4-112">Alle VIP's gebruiken dezelfde openbare poort (443) in het bovenstaande voorbeeld en verkeer wordt omgeleid naar een of meer virtuele machines op een unieke particuliere poort voor het interne IP-adres van de cloudservice die als host fungeert voor alle websites gelijke taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-112">In the example above, all VIPs use the same public port (443) and traffic is redirected to one or more load balanced VMs on a unique private port for the internal IP address of the cloud service hosting all the websites.</span></span>

> [!NOTE]
> <span data-ttu-id="1fcc4-113">Een andere situatie die het gebruik van de meerdere VIP's als host fungeert voor meerdere SQL AlwaysOn availability beschikbaarheidsgroeplisteners op dezelfde set van virtuele Machines.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-113">Another situation requiring the use the multiple VIPs is hosting multiple SQL AlwaysOn availability group listeners on the same set of Virtual Machines.</span></span>

<span data-ttu-id="1fcc4-114">VIP's zijn standaard dynamisch, wat betekent dat de IP-adres toegewezen aan de cloudservice na verloop van tijd kan worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-114">VIPs are dynamic by default, which means that the actual IP address assigned to the cloud service may change over time.</span></span> <span data-ttu-id="1fcc4-115">Om dat te voorkomen, kunt u een VIP-adres reserveren voor uw service.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-115">To prevent that from happening, you can reserve a VIP for your service.</span></span> <span data-ttu-id="1fcc4-116">Zie voor meer informatie over gereserveerde VIP's, [gereserveerde openbare IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc4-116">To learn more about reserved VIPs, see [Reserved Public IP](../virtual-network/virtual-networks-reserved-public-ip.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1fcc4-117">Zie [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses/) voor informatie over de prijzen van VIP's en gereserveerde IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-117">Please see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/) for information on pricing on VIPs and reserved IPs.</span></span>

<span data-ttu-id="1fcc4-118">U kunt PowerShell gebruiken om te controleren of de VIP's die worden gebruikt door uw cloudservices, evenals toevoegen en verwijderen van VIP's, een VIP-adres naar een eindpunt koppelen en taakverdeling op een specifieke VIP-adres configureren.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-118">You can use PowerShell to verify the VIPs used by your cloud services, as well as add and remove VIPs, associate a VIP to an endpoint, and configure load balancing on a specific VIP.</span></span>

## <a name="limitations"></a><span data-ttu-id="1fcc4-119">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1fcc4-119">Limitations</span></span>

<span data-ttu-id="1fcc4-120">Op dit moment is meerdere VIP-functionaliteit beperkt tot de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-120">At this time, Multi VIP functionality is limited to the following scenarios:</span></span>

* <span data-ttu-id="1fcc4-121">**Alleen IaaS**.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-121">**IaaS only**.</span></span> <span data-ttu-id="1fcc4-122">U kunt meerdere VIP alleen inschakelen voor cloudservices met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-122">You can only enable Multi VIP for cloud services that contain VMs.</span></span> <span data-ttu-id="1fcc4-123">U kunt meerdere VIP niet gebruiken voor PaaS-scenario's met rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-123">You cannot use Multi VIP in PaaS scenarios with role instances.</span></span>
* <span data-ttu-id="1fcc4-124">**Alleen PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-124">**PowerShell only**.</span></span> <span data-ttu-id="1fcc4-125">U kunt meerdere VIP alleen beheren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-125">You can only manage Multi VIP by using PowerShell.</span></span>

<span data-ttu-id="1fcc4-126">Deze beperkingen zijn tijdelijk en kunnen op elk gewenst moment worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-126">These limitations are temporary, and may change at any time.</span></span> <span data-ttu-id="1fcc4-127">Zorg ervoor dat deze pagina om te controleren of toekomstige wijzigingen aangepast.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-127">Make sure to revisit this page to verify future changes.</span></span>

## <a name="how-to-add-a-vip-to-a-cloud-service"></a><span data-ttu-id="1fcc4-128">Een VIP-adres toevoegen aan een cloudservice</span><span class="sxs-lookup"><span data-stu-id="1fcc4-128">How to add a VIP to a cloud service</span></span>
<span data-ttu-id="1fcc4-129">Om een VIP-adres toevoegen aan uw service, voer de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-129">To add a VIP to your service, run the following PowerShell command:</span></span>

```powershell
Add-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

<span data-ttu-id="1fcc4-130">Deze opdracht geeft u een resultaat vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-130">This command displays a result similar to the following sample:</span></span>

    OperationDescription OperationId                          OperationStatus
    -------------------- -----------                          ---------------
    Add-AzureVirtualIP   4bd7b638-d2e7-216f-ba38-5221233d70ce Succeeded

## <a name="how-to-remove-a-vip-from-a-cloud-service"></a><span data-ttu-id="1fcc4-131">Een VIP-adres van een service in de cloud verwijderen</span><span class="sxs-lookup"><span data-stu-id="1fcc4-131">How to remove a VIP from a cloud service</span></span>
<span data-ttu-id="1fcc4-132">Voer de volgende PowerShell-opdracht voor het verwijderen van de VIP toegevoegd aan uw service in het bovenstaande voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-132">To remove the VIP added to your service in the example above, run the following PowerShell command:</span></span>

```powershell
Remove-AzureVirtualIP -VirtualIPName Vip3 -ServiceName myService
```

> [!IMPORTANT]
> <span data-ttu-id="1fcc4-133">U kunt alleen een VIP-adres verwijderen als er geen eindpunten zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-133">You can only remove a VIP if it has no endpoints associated to it.</span></span>


## <a name="how-to-retrieve-vip-information-from-a-cloud-service"></a><span data-ttu-id="1fcc4-134">Hoe VIP-gegevens ophalen uit een Cloud-Service</span><span class="sxs-lookup"><span data-stu-id="1fcc4-134">How to retrieve VIP information from a Cloud Service</span></span>
<span data-ttu-id="1fcc4-135">Voer de volgende PowerShell-script voor het ophalen van de VIP's die zijn gekoppeld aan een cloudservice:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-135">To retrieve the VIPs associated with a cloud service, run the following PowerShell script:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="1fcc4-136">Het script geeft een resultaat vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-136">The script displays a result similar to the following sample:</span></span>

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

<span data-ttu-id="1fcc4-137">In dit voorbeeld heeft de cloudservice 3 VIP's:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-137">In this example, the cloud service has 3 VIPs:</span></span>

* <span data-ttu-id="1fcc4-138">**Vip1** is de standaard-VIP u weet dat omdat de waarde voor IsDnsProgrammedName is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-138">**Vip1** is the default VIP, you know that because the value for IsDnsProgrammedName is set to true.</span></span>
* <span data-ttu-id="1fcc4-139">**Vip2** en **Vip3** niet als er geen IP-adressen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-139">**Vip2** and **Vip3** are not used as they do not have any IP addresses.</span></span> <span data-ttu-id="1fcc4-140">Deze wordt alleen gebruikt als u een eindpunt naar het VIP koppelt.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-140">They will only be used if you associate an endpoint to the VIP.</span></span>

> [!NOTE]
> <span data-ttu-id="1fcc4-141">Uw abonnement wordt alleen in rekening gebracht voor extra VIP's zodra ze gekoppeld aan een eindpunt zijn.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-141">Your subscription will only be charged for extra VIPs once they are associated with an endpoint.</span></span> <span data-ttu-id="1fcc4-142">Zie voor meer informatie over prijzen [IP-adres prijzen](https://azure.microsoft.com/pricing/details/ip-addresses/).</span><span class="sxs-lookup"><span data-stu-id="1fcc4-142">For more information on pricing, see [IP Address pricing](https://azure.microsoft.com/pricing/details/ip-addresses/).</span></span>

## <a name="how-to-associate-a-vip-to-an-endpoint"></a><span data-ttu-id="1fcc4-143">Het koppelen van een VIP-adres naar een eindpunt</span><span class="sxs-lookup"><span data-stu-id="1fcc4-143">How to associate a VIP to an endpoint</span></span>

<span data-ttu-id="1fcc4-144">Om te koppelen van een VIP-adres op een cloudservice om een eindpunt, voer de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-144">To associate a VIP on a cloud service to an endpoint, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -Protocol tcp -LocalPort 8080 -PublicPort 80 -VirtualIPName Vip2 |
    Update-AzureVM
```

<span data-ttu-id="1fcc4-145">De opdracht maakt u een eindpunt dat is gekoppeld aan de VIP aangeroepen *Vip2* op poort *80*, gekoppeld aan de virtuele machine met de naam *myVM1* in een cloudservice met de naam *MijnService* met *TCP* op poort *8080*.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-145">The command creates an endpoint linked to the VIP called *Vip2* on port *80*, and links it to the VM named *myVM1* in a cloud service named *myService* using *TCP* on port *8080*.</span></span>

<span data-ttu-id="1fcc4-146">Om te controleren of de configuratie, moet u de volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-146">To verify the configuration, run the following PowerShell command:</span></span>

```powershell
$deployment = Get-AzureDeployment -ServiceName myService
$deployment.VirtualIPs
```

<span data-ttu-id="1fcc4-147">De uitvoer lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-147">The output looks similar to the following example:</span></span>

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

## <a name="how-to-enable-load-balancing-on-a-specific-vip"></a><span data-ttu-id="1fcc4-148">Het inschakelen van taakverdeling op een specifieke VIP-adres</span><span class="sxs-lookup"><span data-stu-id="1fcc4-148">How to enable load balancing on a specific VIP</span></span>

<span data-ttu-id="1fcc4-149">U kunt een enkel VIP koppelen aan meerdere virtuele machines voor load balancing-doeleinden.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-149">You can associate a single VIP with multiple virtual machines for load balancing purposes.</span></span> <span data-ttu-id="1fcc4-150">Bijvoorbeeld: u hebt een cloudservice met de naam *MijnService*, en twee virtuele machines met de naam *myVM1* en *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-150">For example, you have a cloud service named *myService*, and two virtual machines named *myVM1* and *myVM2*.</span></span> <span data-ttu-id="1fcc4-151">En uw cloudservice heeft meerdere VIP's, een van deze met de naam *Vip2*.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-151">And your cloud service has multiple VIPs, one of them named *Vip2*.</span></span> <span data-ttu-id="1fcc4-152">Als u zorgen wilt dat alle verkeer op poort *81* op *Vip2* wordt verdeeld tussen *myVM1* en *myVM2* op poort *8181* , voer het volgende PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-152">If you want to ensure that all traffic to port *81* on *Vip2* is balanced between *myVM1* and *myVM2* on port *8181*, run the following PowerShell script:</span></span>

```powershell
Get-AzureVM -ServiceName myService -Name myVM1 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2 -DefaultProbe |
    Update-AzureVM

Get-AzureVM -ServiceName myService -Name myVM2 |
    Add-AzureEndpoint -Name myEndpoint -LoadBalancedEndpointSetName myLBSet -Protocol tcp -LocalPort 8181 -PublicPort 81 -VirtualIPName Vip2  -DefaultProbe |
    Update-AzureVM
```

<span data-ttu-id="1fcc4-153">U kunt ook de load balancer voor het gebruik van een andere VIP bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1fcc4-153">You can also update your load balancer to use a different VIP.</span></span> <span data-ttu-id="1fcc4-154">Als u de onderstaande PowerShell-opdracht uitvoert, wordt u bijvoorbeeld is ingesteld op het gebruik van een VIP Vip1 met de naam van de taakverdeling wijzigen:</span><span class="sxs-lookup"><span data-stu-id="1fcc4-154">For example, if you run the PowerShell command below, you will change the load balancing set to use a VIP named Vip1:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName myService -LBSetName myLBSet -VirtualIPName Vip1
```

## <a name="next-steps"></a><span data-ttu-id="1fcc4-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1fcc4-155">Next Steps</span></span>

[<span data-ttu-id="1fcc4-156">Taakverdeling van de Azure-logboekanalyse</span><span class="sxs-lookup"><span data-stu-id="1fcc4-156">Log analytics for Azure Load Balance</span></span>](load-balancer-monitor-log.md)

[<span data-ttu-id="1fcc4-157">Internet gerichte load balancer-overzicht</span><span class="sxs-lookup"><span data-stu-id="1fcc4-157">Internet facing load balancer overview</span></span>](load-balancer-internet-overview.md)

[<span data-ttu-id="1fcc4-158">Aan de slag op Internet gerichte load balancer</span><span class="sxs-lookup"><span data-stu-id="1fcc4-158">Get started on Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="1fcc4-159">Overzicht van Virtual Network</span><span class="sxs-lookup"><span data-stu-id="1fcc4-159">Virtual Network Overview</span></span>](../virtual-network/virtual-networks-overview.md)

[<span data-ttu-id="1fcc4-160">Gereserveerd IP-adres REST-API 's</span><span class="sxs-lookup"><span data-stu-id="1fcc4-160">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)
