---
title: aaaManage Azure gereserveerde IP-adressen (klassiek) - PowerShell | Microsoft Docs
description: Gereserveerde IP-adressen (klassiek) te begrijpen en hoe toomanage ze met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 34652a55-3ab8-4c2d-8fb2-43684033b191
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: c0a77b2ab8b1ab9bef6015c903eb735ea4358a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reserved-ip-addresses-classic"></a><span data-ttu-id="5571c-103">Gereserveerde IP-adressen (klassiek)</span><span class="sxs-lookup"><span data-stu-id="5571c-103">Reserved IP addresses (Classic)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5571c-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5571c-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="5571c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5571c-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="5571c-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5571c-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="5571c-107">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="5571c-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="5571c-108">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="5571c-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

<span data-ttu-id="5571c-109">IP-adressen in Azure worden onderverdeeld in twee categorieën: dynamische en gereserveerd.</span><span class="sxs-lookup"><span data-stu-id="5571c-109">IP addresses in Azure fall into two categories: dynamic and reserved.</span></span> <span data-ttu-id="5571c-110">Openbare IP-adressen die worden beheerd door Azure worden standaard dynamisch.</span><span class="sxs-lookup"><span data-stu-id="5571c-110">Public IP addresses managed by Azure are dynamic by default.</span></span> <span data-ttu-id="5571c-111">Dat betekent dat Hallo IP-adres voor een bepaalde cloud-service (VIP) of tooaccess een virtuele machine gebruikt of rechtstreeks rolinstantie (ILPIP) van tijd tootime, wijzigen kunt wanneer resources worden afgesloten of gestopt (toewijzing ongedaan gemaakt).</span><span class="sxs-lookup"><span data-stu-id="5571c-111">That means that hello IP address used for a given cloud service (VIP) or tooaccess a VM or role instance directly (ILPIP) can change from time tootime, when resources are shut down or stopped (deallocated).</span></span>

<span data-ttu-id="5571c-112">tooprevent IP-adressen kunnen wijzigen, kunt u een IP-adres reserveren.</span><span class="sxs-lookup"><span data-stu-id="5571c-112">tooprevent IP addresses from changing, you can reserve an IP address.</span></span> <span data-ttu-id="5571c-113">Gereserveerd IP-adressen kan alleen worden gebruikt als een VIP, waarbij u ervoor zorgt dat Hallo IP-adres voor de cloudservice Hallo blijft Hallo dezelfde zijn, zelfs als bronnen worden afgesloten of gestopt (toewijzing ongedaan gemaakt).</span><span class="sxs-lookup"><span data-stu-id="5571c-113">Reserved IPs can be used only as a VIP, ensuring that hello IP address for hello cloud service remains hello same, even as resources are shut down or stopped (deallocated).</span></span> <span data-ttu-id="5571c-114">Bovendien kunt u als een VIP tooa gereserveerd IP-adres gebruikt bestaande dynamische IP-adressen converteren.</span><span class="sxs-lookup"><span data-stu-id="5571c-114">Furthermore, you can convert existing dynamic IPs used as a VIP tooa reserved IP address.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5571c-115">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5571c-115">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5571c-116">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5571c-116">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5571c-117">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5571c-117">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5571c-118">Meer informatie over hoe een statische openbare IP-adres met tooreserve Hallo [Resource Manager-implementatiemodel](virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="5571c-118">Learn how tooreserve a static public IP address using hello [Resource Manager deployment model](virtual-network-ip-addresses-overview-arm.md).</span></span>

<span data-ttu-id="5571c-119">toolearn meer over IP-adressen in Azure, Hallo lezen [IP-adressen](virtual-network-ip-addresses-overview-classic.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="5571c-119">toolearn more about IP addresses in Azure, read hello [IP addresses](virtual-network-ip-addresses-overview-classic.md) article.</span></span>

## <a name="when-do-i-need-a-reserved-ip"></a><span data-ttu-id="5571c-120">Wanneer moet ik een gereserveerde IP-adres?</span><span class="sxs-lookup"><span data-stu-id="5571c-120">When do I need a reserved IP?</span></span>
* <span data-ttu-id="5571c-121">**U wilt dat tooensure die Hallo IP is gereserveerd in uw abonnement**.</span><span class="sxs-lookup"><span data-stu-id="5571c-121">**You want tooensure that hello IP is reserved in your subscription**.</span></span> <span data-ttu-id="5571c-122">Als u wilt dat een IP-adres dat wordt niet vrijgegeven tooreserve uit uw abonnement onder enkel beding, moet u een gereserveerde openbare IP-adres gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5571c-122">If you want tooreserve an IP address that is not released from your subscription under any circumstance, you should use a reserved public IP.</span></span>  
* <span data-ttu-id="5571c-123">**U wilt dat uw IP-toostay met uw cloudservice zelfs meerdere gestopt of toewijzing opgeheven status (VM's)**.</span><span class="sxs-lookup"><span data-stu-id="5571c-123">**You want your IP toostay with your cloud service even across stopped or deallocated state (VMs)**.</span></span> <span data-ttu-id="5571c-124">Als u wilt dat uw service toobe toegankelijk via een IP-adres dat niet verandert, zelfs wanneer virtuele machines in Hallo cloud-service worden afgesloten of gestopt (toewijzing ongedaan gemaakt).</span><span class="sxs-lookup"><span data-stu-id="5571c-124">If you want your service toobe accessed by using an IP address that doesn't change, even when VMs in hello cloud service are shut down or stop (deallocated).</span></span>
* <span data-ttu-id="5571c-125">**U wilt dat uitgaand verkeer vanuit Azure gebruikmaakt van een voorspelbare IP-adres tooensure**.</span><span class="sxs-lookup"><span data-stu-id="5571c-125">**You want tooensure that outbound traffic from Azure uses a predictable IP address**.</span></span> <span data-ttu-id="5571c-126">Mogelijk hebt u uw lokale geconfigureerde firewall tooallow alleen het verkeer van specifieke IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="5571c-126">You may have your on-premises firewall configured tooallow only traffic from specific IP addresses.</span></span> <span data-ttu-id="5571c-127">Door een IP-adres reserveren, weet u Hallo bron-IP adres en hoeft niet tooupdate uw firewallregels vanwege tooan IP-wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5571c-127">By reserving an IP, you know hello source IP address, and don't need tooupdate your firewall rules due tooan IP change.</span></span>

## <a name="faq"></a><span data-ttu-id="5571c-128">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="5571c-128">FAQ</span></span>
1. <span data-ttu-id="5571c-129">Kan ik een gereserveerde IP-adres gebruiken voor alle Azure-services?</span><span class="sxs-lookup"><span data-stu-id="5571c-129">Can I use a reserved IP for all Azure services?</span></span> <br>
    <span data-ttu-id="5571c-130">Nee.</span><span class="sxs-lookup"><span data-stu-id="5571c-130">No.</span></span> <span data-ttu-id="5571c-131">Gereserveerd IP-adressen kan alleen worden gebruikt voor virtuele machines en cloud service-exemplaar rollen weergegeven via een VIP-adres.</span><span class="sxs-lookup"><span data-stu-id="5571c-131">Reserved IPs can only be used for VMs and cloud service instance roles exposed through a VIP.</span></span>
2. <span data-ttu-id="5571c-132">Het aantal gereserveerde IP's kan ik hebben?</span><span class="sxs-lookup"><span data-stu-id="5571c-132">How many reserved IPs can I have?</span></span> <br>
    <span data-ttu-id="5571c-133">Zie voor meer informatie, Hallo [Azure beperkt](../azure-subscription-service-limits.md#networking-limits) artikel.</span><span class="sxs-lookup"><span data-stu-id="5571c-133">For details, see hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
3. <span data-ttu-id="5571c-134">Is er kosten met zich mee voor gereserveerde IP's?</span><span class="sxs-lookup"><span data-stu-id="5571c-134">Is there a charge for reserved IPs?</span></span> <br>
    <span data-ttu-id="5571c-135">Soms.</span><span class="sxs-lookup"><span data-stu-id="5571c-135">Sometimes.</span></span> <span data-ttu-id="5571c-136">Zie voor prijsinformatie, Hallo [gereserveerde IP-adres prijsinformatie](http://go.microsoft.com/fwlink/?LinkID=398482) pagina.</span><span class="sxs-lookup"><span data-stu-id="5571c-136">For pricing details, see hello [Reserved IP Address Pricing Details](http://go.microsoft.com/fwlink/?LinkID=398482) page.</span></span>
4. <span data-ttu-id="5571c-137">Hoe ik een IP-adres reserveren?</span><span class="sxs-lookup"><span data-stu-id="5571c-137">How do I reserve an IP address?</span></span> <br>
    <span data-ttu-id="5571c-138">U kunt PowerShell gebruiken, hello [Management REST API van Azure](https://msdn.microsoft.com/library/azure/dn722420.aspx), of Hallo [Azure-portal](https://portal.azure.com) tooreserve een IP-adres in een Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="5571c-138">You can use PowerShell, hello [Azure Management REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx), or hello [Azure portal](https://portal.azure.com) tooreserve an IP address in an Azure region.</span></span> <span data-ttu-id="5571c-139">Een gereserveerd IP-adres is gekoppeld tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="5571c-139">A reserved IP address is associated tooyour subscription.</span></span>
5. <span data-ttu-id="5571c-140">Kan ik een gereserveerde IP-adres gebruiken met VNets op basis van een affiniteitsgroep</span><span class="sxs-lookup"><span data-stu-id="5571c-140">Can I use a reserved IP with affinity group-based VNets?</span></span> <br>
    <span data-ttu-id="5571c-141">Nee.</span><span class="sxs-lookup"><span data-stu-id="5571c-141">No.</span></span> <span data-ttu-id="5571c-142">Gereserveerd IP-adressen worden alleen ondersteund in regionaal vnet's.</span><span class="sxs-lookup"><span data-stu-id="5571c-142">Reserved IPs are only supported in regional VNets.</span></span> <span data-ttu-id="5571c-143">Gereserveerd IP-adressen worden niet ondersteund voor VNets die zijn gekoppeld aan affiniteitsgroepen.</span><span class="sxs-lookup"><span data-stu-id="5571c-143">Reserved IPs are not supported for VNets that are associated with affinity groups.</span></span> <span data-ttu-id="5571c-144">Zie voor meer informatie over het koppelen van een VNet met een regio of affiniteitsgroep hello [over regionaal vnet's en Affiniteitsgroepen](virtual-networks-migrate-to-regional-vnet.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="5571c-144">For more information about associating a VNet with a region or affinity group, see hello [About Regional VNets and Affinity Groups](virtual-networks-migrate-to-regional-vnet.md) article.</span></span>

## <a name="manage-reserved-vips"></a><span data-ttu-id="5571c-145">Gereserveerde VIP's beheren</span><span class="sxs-lookup"><span data-stu-id="5571c-145">Manage reserved VIPs</span></span>

<span data-ttu-id="5571c-146">Zorg ervoor dat u hebt geïnstalleerd en geconfigureerd PowerShell via Hallo stappen in Hallo [installeren en configureren van PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="5571c-146">Ensure you have installed and configured PowerShell by completing hello steps in hello [Install and configure PowerShell](/powershell/azure/overview) article.</span></span> 

<span data-ttu-id="5571c-147">Voordat u gereserveerde IP's gebruiken kunt, moet u deze tooyour abonnement toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5571c-147">Before you can use reserved IPs, you must add it tooyour subscription.</span></span> <span data-ttu-id="5571c-148">toocreate een gereserveerde IP-adres van de groep Hallo met openbare IP-adressen beschikbaar zijn in Hallo *VS-midden* locatie, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5571c-148">toocreate a reserved IP from hello pool of public IP addresses available in hello *Central US* location, run hello following command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"
```

<span data-ttu-id="5571c-149">U ziet, echter, u niet opgeven wat IP wordt gereserveerd.</span><span class="sxs-lookup"><span data-stu-id="5571c-149">Notice, however, that you cannot specify what IP is being reserved.</span></span> <span data-ttu-id="5571c-150">tooview welke IP-adressen zijn gereserveerd in uw abonnement, Hallo volgende PowerShell-opdracht uitvoeren en Let op Hallo waarden voor *ReservedIPName* en *adres*:</span><span class="sxs-lookup"><span data-stu-id="5571c-150">tooview what IP addresses are reserved in your subscription, run hello following PowerShell command, and notice hello values for *ReservedIPName* and *Address*:</span></span>

```powershell
Get-AzureReservedIP
```

<span data-ttu-id="5571c-151">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5571c-151">Expected output:</span></span>

    ReservedIPName       : MyReservedIP
    Address              : 23.101.114.211
    Id                   : d73be9dd-db12-4b5e-98c8-bc62e7c42041
    Label                :
    Location             : Central US
    State                : Created
    InUse                : False
    ServiceName          :
    DeploymentName       :
    OperationDescription : Get-AzureReservedIP
    OperationId          : 55e4f245-82e4-9c66-9bd8-273e815ce30a
    OperationStatus      : Succeeded

>[!NOTE]
><span data-ttu-id="5571c-152">Wanneer u een gereserveerd IP-adres met PowerShell maakt, kunt u een resource groep toocreate Hallo gereserveerd IP-adres in niet opgeven.</span><span class="sxs-lookup"><span data-stu-id="5571c-152">When you create a reserved IP address with PowerShell, you cannot specify a resource group toocreate hello reserved IP in.</span></span> <span data-ttu-id="5571c-153">Azure plaatsen in een resourcegroep met de naam *standaard netwerken* automatisch.</span><span class="sxs-lookup"><span data-stu-id="5571c-153">Azure places it into a resource group named *Default-Networking* automatically.</span></span> <span data-ttu-id="5571c-154">Als u Hallo gereserveerd IP met Hallo maakt [Azure-portal](http://portal.azure.com), kunt u een resourcegroep die u kiest.</span><span class="sxs-lookup"><span data-stu-id="5571c-154">If you create hello reserved IP using hello [Azure portal](http://portal.azure.com), you can specify any resource group you choose.</span></span> <span data-ttu-id="5571c-155">Als u Hallo gereserveerd IP anders dan in een resourcegroep maken *standaard netwerken* echter, wanneer u verwijst naar Hallo gereserveerde IP-adres met opdrachten zoals `Get-AzureReservedIP` en `Remove-AzureReservedIP`, moet u verwijzen naar Hallo naam *Resourcegroepnaam gereserveerd-ip-naam van de groep*.</span><span class="sxs-lookup"><span data-stu-id="5571c-155">If you create hello reserved IP in a resource group other than *Default-Networking* however, whenever you reference hello reserved IP with commands such as `Get-AzureReservedIP` and `Remove-AzureReservedIP`, you must reference hello name *Group resource-group-name reserved-ip-name*.</span></span>  <span data-ttu-id="5571c-156">Bijvoorbeeld, als u een gereserveerde IP-adres met de naam *myReservedIP* in een resourcegroep met de naam *myResourceGroup*, u moet verwijzen naar de naam van Hallo gereserveerd IP-adres als Hallo *groep myResourceGroup myReservedIP*.</span><span class="sxs-lookup"><span data-stu-id="5571c-156">For example, if you create a reserved IP named *myReservedIP* in a resource group named *myResourceGroup*, you must reference hello name of hello reserved IP as *Group myResourceGroup myReservedIP*.</span></span>   

<span data-ttu-id="5571c-157">Nadat een IP-adres is gereserveerd, blijft deze gekoppelde tooyour abonnement totdat u het verwijdert.</span><span class="sxs-lookup"><span data-stu-id="5571c-157">Once an IP is reserved, it remains associated tooyour subscription until you delete it.</span></span> <span data-ttu-id="5571c-158">toodelete een gereserveerde IP-adres, Voer Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="5571c-158">toodelete a reserved IP, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIP -ReservedIPName "MyReservedIP"
```

## <a name="reserve-hello-ip-address-of-an-existing-cloud-service"></a><span data-ttu-id="5571c-159">Reserveer Hallo IP-adres van een bestaande cloudservice</span><span class="sxs-lookup"><span data-stu-id="5571c-159">Reserve hello IP address of an existing cloud service</span></span>
<span data-ttu-id="5571c-160">U kunt Hallo IP-adres van een bestaande cloudservice reserveren door toe te voegen Hallo `-ServiceName` parameter.</span><span class="sxs-lookup"><span data-stu-id="5571c-160">You can reserve hello IP address of an existing cloud service by adding hello `-ServiceName` parameter.</span></span> <span data-ttu-id="5571c-161">tooreserve hello IP-adres van een cloudservice *TestService* in Hallo *VS-midden* locatie, Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5571c-161">tooreserve hello IP address of a cloud service *TestService* in hello *Central US* location, run hello following PowerShell command:</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US" -ServiceName TestService
```

## <a name="associate-a-reserved-ip-tooa-new-cloud-service"></a><span data-ttu-id="5571c-162">Koppelen van een gereserveerd IP-tooa nieuwe cloudservice</span><span class="sxs-lookup"><span data-stu-id="5571c-162">Associate a reserved IP tooa new cloud service</span></span>
<span data-ttu-id="5571c-163">Hallo volgende script maakt een nieuw gereserveerd IP-adres en vervolgens koppelt u deze tooa nieuwe cloudservice met de naam *TestService*.</span><span class="sxs-lookup"><span data-stu-id="5571c-163">hello following script creates a new reserved IP, then associates it tooa new cloud service named *TestService*.</span></span>

```powershell
New-AzureReservedIP –ReservedIPName MyReservedIP –Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService -ReservedIPName MyReservedIP -Location "Central US"
```

> [!NOTE]
> <span data-ttu-id="5571c-164">Wanneer u een gereserveerd IP-toouse met een cloudservice maakt, u nog steeds toohello VM verwijzen met behulp van *VIP:&lt;poortnummer >* voor binnenkomende communicatie.</span><span class="sxs-lookup"><span data-stu-id="5571c-164">When you create a reserved IP toouse with a cloud service, you still refer toohello VM by using *VIP:&lt;port number>* for inbound communication.</span></span> <span data-ttu-id="5571c-165">Een IP-adres reserveren betekent niet dat toohello virtuele machine rechtstreeks kan worden aangesloten.</span><span class="sxs-lookup"><span data-stu-id="5571c-165">Reserving an IP does not mean you can connect toohello VM directly.</span></span> <span data-ttu-id="5571c-166">Hallo gereserveerde IP-adres is toegewezen toohello cloud service die Hallo VM is geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="5571c-166">hello reserved IP is assigned toohello cloud service that hello VM has been deployed to.</span></span> <span data-ttu-id="5571c-167">Als u rechtstreeks tooconnect tooa VM door IP wilt, hebt u tooconfigure een openbaar IP op exemplaarniveau.</span><span class="sxs-lookup"><span data-stu-id="5571c-167">If you want tooconnect tooa VM by IP directly, you have tooconfigure an instance-level public IP.</span></span> <span data-ttu-id="5571c-168">Een openbaar IP op exemplaarniveau is een openbaar IP-adres (een ILPIP genoemd) die rechtstreeks tooyour VM is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5571c-168">An instance-level public IP is a type of public IP (called an ILPIP) that is assigned directly tooyour VM.</span></span> <span data-ttu-id="5571c-169">Deze kan niet worden gereserveerd.</span><span class="sxs-lookup"><span data-stu-id="5571c-169">It cannot be reserved.</span></span> <span data-ttu-id="5571c-170">Lees voor meer informatie, Hallo [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="5571c-170">For more information, read hello [Instance-level Public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) article.</span></span>
> 

## <a name="remove-a-reserved-ip-from-a-running-deployment"></a><span data-ttu-id="5571c-171">Een gereserveerd IP-adres van een actieve implementatie verwijderen</span><span class="sxs-lookup"><span data-stu-id="5571c-171">Remove a reserved IP from a running deployment</span></span>
<span data-ttu-id="5571c-172">tooremove een gereserveerde IP-adres toegevoegd tooa nieuwe cloudservice Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5571c-172">tooremove a reserved IP added tooa new cloud service, run hello following PowerShell command:</span></span>

```powershell
Remove-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService
```

> [!NOTE]
> <span data-ttu-id="5571c-173">Een gereserveerd IP-adres worden van een actieve implementatie niet verwijderd Hallo reservering uit uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5571c-173">Removing a reserved IP from a running deployment does not remove hello reservation from your subscription.</span></span> <span data-ttu-id="5571c-174">Het wordt gewoon vrijgemaakt Hallo IP-toobe gebruikt door een andere resource in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5571c-174">It simply frees hello IP toobe used by another resource in your subscription.</span></span>
> 

## <a name="associate-a-reserved-ip-tooa-running-deployment"></a><span data-ttu-id="5571c-175">Koppelen van een gereserveerd IP-tooa waarop implementatie wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5571c-175">Associate a reserved IP tooa running deployment</span></span>
<span data-ttu-id="5571c-176">Hallo volgende opdrachten een cloudservice maken met de naam *TestService2* met een nieuwe virtuele machine met de naam *TestVM2*.</span><span class="sxs-lookup"><span data-stu-id="5571c-176">hello following commands create a cloud service named *TestService2* with a new VM named *TestVM2*.</span></span> <span data-ttu-id="5571c-177">Hallo bestaande gereserveerde IP-adres met de naam *MyReservedIP* zich bevindt, wordt het bijbehorende toohello cloudservice.</span><span class="sxs-lookup"><span data-stu-id="5571c-177">hello existing reserved IP named *MyReservedIP* is then associated toohello cloud service.</span></span>

```powershell
$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}

New-AzureVMConfig -Name TestVM2 -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| New-AzureVM -ServiceName TestService2 -Location "Central US"

Set-AzureReservedIPAssociation -ReservedIPName MyReservedIP -ServiceName TestService2
```

## <a name="associate-a-reserved-ip-tooa-cloud-service-by-using-a-service-configuration-file"></a><span data-ttu-id="5571c-178">Een gereserveerd IP-tooa cloudservice koppelen via een configuratiebestand voor de service</span><span class="sxs-lookup"><span data-stu-id="5571c-178">Associate a reserved IP tooa cloud service by using a service configuration file</span></span>
<span data-ttu-id="5571c-179">U kunt ook een gereserveerd IP-tooa cloudservice koppelen met behulp van een service-configuratiebestand (CSCFG).</span><span class="sxs-lookup"><span data-stu-id="5571c-179">You can also associate a reserved IP tooa cloud service by using a service configuration (CSCFG) file.</span></span> <span data-ttu-id="5571c-180">Hallo volgende XML-code voorbeeld ziet u hoe tooconfigure een cloud service toouse een gereserveerd VIP-adres met de naam *MyReservedIP*:</span><span class="sxs-lookup"><span data-stu-id="5571c-180">hello following sample xml shows how tooconfigure a cloud service toouse a reserved VIP named *MyReservedIP*:</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ReservedIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
        <ConfigurationSettings>
          <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
        </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <ReservedIPs>
           <ReservedIP name="MyReservedIP"/>
          </ReservedIPs>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>

## <a name="next-steps"></a><span data-ttu-id="5571c-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5571c-181">Next steps</span></span>
* <span data-ttu-id="5571c-182">Begrijpen hoe [IP-adressering](virtual-network-ip-addresses-overview-classic.md) werkt in het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="5571c-182">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="5571c-183">Meer informatie over [privé IP-adressen gereserveerd](virtual-networks-reserved-private-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5571c-183">Learn about [reserved private IP addresses](virtual-networks-reserved-private-ip.md).</span></span>
* <span data-ttu-id="5571c-184">Meer informatie over [Instance Level Public IP (ILPIP) adressen](virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="5571c-184">Learn about [Instance Level Public IP (ILPIP) addresses](virtual-networks-instance-level-public-ip.md).</span></span>

