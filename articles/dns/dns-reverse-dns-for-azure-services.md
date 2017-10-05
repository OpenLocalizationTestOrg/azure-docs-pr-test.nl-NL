---
title: Omgekeerde DNS voor Azure-services | Microsoft Docs
description: Informatie over het configureren van de reverse DNS-zoekacties voor services die worden gehost in Azure
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/29/2017
ms.author: jonatul
ms.openlocfilehash: 63701e1ce0c1c6dcf2ce02ebce272b8280395e7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="69314-103">Omgekeerde DNS voor services die worden gehost in Azure configureren</span><span class="sxs-lookup"><span data-stu-id="69314-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="69314-104">In dit artikel wordt uitgelegd hoe het configureren van de reverse DNS-zoekacties voor services die worden gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="69314-104">This article explains how to configure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="69314-105">Services in Azure gebruiken IP-adressen toegewezen door Azure en het eigendom van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="69314-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="69314-106">Deze omgekeerde DNS-records (PTR-records) moeten worden gemaakt in de bijbehorende die eigendom zijn van Microsoft omgekeerde DNS-lookup zones.</span><span class="sxs-lookup"><span data-stu-id="69314-106">These reverse DNS records (PTR records) must be created in the corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="69314-107">Dit artikel wordt uitgelegd hoe u dit doet.</span><span class="sxs-lookup"><span data-stu-id="69314-107">This article explains how to do this.</span></span>

<span data-ttu-id="69314-108">Dit scenario moet niet de mogelijkheid om te verwarren [de zones voor reverse DNS-lookup voor uw toegewezen IP-adresbereiken in Azure DNS hosten](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="69314-108">This scenario should not be confused with the ability to [host the reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="69314-109">In dit geval moeten de IP-adresbereiken dat wordt vertegenwoordigd door de zone voor reverse lookup worden toegewezen aan uw organisatie gewoonlijk door uw Internetprovider.</span><span class="sxs-lookup"><span data-stu-id="69314-109">In this case, the IP ranges represented by the reverse lookup zone must be assigned to your organization, typically by your ISP.</span></span>

<span data-ttu-id="69314-110">Voordat u dit artikel leest, moet u bekend bent met dit [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="69314-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="69314-111">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="69314-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="69314-112">In het Resource Manager-implementatiemodel compute-bronnen (zoals virtuele machines, virtuele-machineschaalsets of Service Fabric-clusters) beschikbaar worden gemaakt via een PublicIpAddress-resource.</span><span class="sxs-lookup"><span data-stu-id="69314-112">In the Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="69314-113">Omgekeerde DNS-zoekacties zijn geconfigureerd met de eigenschap 'ReverseFqdn' van de PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="69314-113">Reverse DNS lookups are configured using the 'ReverseFqdn' property of the PublicIpAddress.</span></span>
* <span data-ttu-id="69314-114">In het klassieke implementatiemodel rekenresources zichtbaar met behulp van Cloudservices.</span><span class="sxs-lookup"><span data-stu-id="69314-114">In the Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="69314-115">Omgekeerde DNS-zoekacties zijn geconfigureerd met de eigenschap 'ReverseDnsFqdn' van de Cloudservice.</span><span class="sxs-lookup"><span data-stu-id="69314-115">Reverse DNS lookups are configured using the 'ReverseDnsFqdn' property of the Cloud Service.</span></span>

<span data-ttu-id="69314-116">Omgekeerde DNS is momenteel niet ondersteund voor de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="69314-116">Reverse DNS is not currently supported for the Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="69314-117">Validatie van de reverse DNS-records</span><span class="sxs-lookup"><span data-stu-id="69314-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="69314-118">Een derde partij zou niet mogen maken van de reverse DNS-records voor de Azure-service wordt toegewezen aan uw DNS-domeinen.</span><span class="sxs-lookup"><span data-stu-id="69314-118">A third party should not be able to create reverse DNS records for their Azure service mapping to your DNS domains.</span></span> <span data-ttu-id="69314-119">Om dit te voorkomen, Azure alleen het maken van een omgekeerde DNS-record domeinnaam opgegeven in de omgekeerde DNS-record hetzelfde als waar is of wordt omgezet naar de DNS-naam of IP-adres van een PublicIpAddress of de Cloudservice in dezelfde Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="69314-119">To prevent this, Azure only allows the creation of a reverse DNS record where domain name specified in the reverse DNS record is the same as, or resolves to, the DNS name or IP address of a PublicIpAddress or Cloud Service in the same Azure subscription.</span></span>

<span data-ttu-id="69314-120">Deze validatie wordt alleen uitgevoerd wanneer de omgekeerde DNS-record wordt ingesteld of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="69314-120">This validation is only performed when the reverse DNS record is set or modified.</span></span> <span data-ttu-id="69314-121">Periodieke opnieuw validatie is niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="69314-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="69314-122">Voorbeeld: Stel dat de PublicIpAddress-resource heeft de DNS-naam contosoapp1.northus.cloudapp.azure.com en het IP-adres 23.96.52.53.</span><span class="sxs-lookup"><span data-stu-id="69314-122">For example: suppose the PublicIpAddress resource has the DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="69314-123">De ReverseFqdn voor de PublicIpAddress kan worden opgegeven als:</span><span class="sxs-lookup"><span data-stu-id="69314-123">The ReverseFqdn for the PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="69314-124">De DNS-naam voor de PublicIpAddress contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="69314-124">The DNS name for the PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="69314-125">De DNS-naam voor een andere PublicIpAddress in hetzelfde abonnement behoren, zoals contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="69314-125">The DNS name for a different PublicIpAddress in the same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="69314-126">Een vanity DNS-naam, zoals app1.contoso.com, zolang deze naam *eerste* geconfigureerd als een CNAME contosoapp1.northus.cloudapp.azure.com of een andere PublicIpAddress in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="69314-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME to contosoapp1.northus.cloudapp.azure.com, or to a different PublicIpAddress in the same subscription.</span></span>
* <span data-ttu-id="69314-127">Een vanity DNS-naam, zoals app1.contoso.com, zolang deze naam *eerste* geconfigureerd als een A-record in de IP-adres 23.96.52.53 of het IP-adres van een andere PublicIpAddress in hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="69314-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record to the IP address 23.96.52.53, or to the IP address of a different PublicIpAddress in the same subscription.</span></span>

<span data-ttu-id="69314-128">De beperkingen voor dezelfde toepassing omgekeerde DNS voor Cloud-Services.</span><span class="sxs-lookup"><span data-stu-id="69314-128">The same constraints apply to reverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="69314-129">Omgekeerde DNS voor PublicIpAddress resources</span><span class="sxs-lookup"><span data-stu-id="69314-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="69314-130">Deze sectie bevat gedetailleerde instructies voor het configureren van omgekeerde DNS voor PublicIpAddress bronnen in het Resource Manager-implementatiemodel, met Azure PowerShell, Azure CLI 1.0 of 2.0 voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="69314-130">This section provides detailed instructions for how to configure reverse DNS for PublicIpAddress resources in the Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="69314-131">Configureren van omgekeerde DNS voor PublicIpAddress bronnen is momenteel niet ondersteund via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="69314-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via the Azure portal.</span></span>

<span data-ttu-id="69314-132">Azure momenteel ondersteunt reverse DNS alleen voor IPv4 PublicIpAddress resources.</span><span class="sxs-lookup"><span data-stu-id="69314-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="69314-133">Dit wordt niet ondersteund voor IPv6.</span><span class="sxs-lookup"><span data-stu-id="69314-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-to-an-existing-publicipaddresses"></a><span data-ttu-id="69314-134">Omgekeerde DNS toevoegen aan een bestaande PublicIpAddresses</span><span class="sxs-lookup"><span data-stu-id="69314-134">Add reverse DNS to an existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="69314-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69314-135">PowerShell</span></span>

<span data-ttu-id="69314-136">Omgekeerde DNS toevoegen aan een bestaande PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="69314-136">To add reverse DNS to an existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="69314-137">Als omgekeerde DNS toevoegen aan een bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="69314-137">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="69314-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="69314-138">Azure CLI 1.0</span></span>

<span data-ttu-id="69314-139">Omgekeerde DNS toevoegen aan een bestaande PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="69314-139">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="69314-140">Als omgekeerde DNS toevoegen aan een bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="69314-140">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="69314-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69314-141">Azure CLI 2.0</span></span>

<span data-ttu-id="69314-142">Omgekeerde DNS toevoegen aan een bestaande PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="69314-142">To add reverse DNS to an existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="69314-143">Als omgekeerde DNS toevoegen aan een bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="69314-143">To add reverse DNS to an existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="69314-144">Maken van een openbaar IP-adres met de reverse DNS</span><span class="sxs-lookup"><span data-stu-id="69314-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="69314-145">Een nieuwe PublicIpAddress maken met de reverse DNS-eigenschap is al opgegeven:</span><span class="sxs-lookup"><span data-stu-id="69314-145">To create a new PublicIpAddress with the reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="69314-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69314-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="69314-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="69314-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="69314-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69314-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="69314-149">Weergave omgekeerde DNS voor een bestaande PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="69314-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="69314-150">De geconfigureerde waarde voor een bestaande PublicIpAddress bekijken:</span><span class="sxs-lookup"><span data-stu-id="69314-150">To view the configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="69314-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69314-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="69314-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="69314-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="69314-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69314-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="69314-154">Omgekeerde DNS verwijderen uit bestaande openbare IP-adressen</span><span class="sxs-lookup"><span data-stu-id="69314-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="69314-155">Verwijdert een omgekeerde DNS-eigenschap van een bestaande PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="69314-155">To remove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="69314-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="69314-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="69314-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="69314-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="69314-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="69314-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="69314-159">Omgekeerde DNS configureren voor Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="69314-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="69314-160">Deze sectie bevat gedetailleerde instructies voor het omgekeerde DNS configureren voor Cloud-Services in het klassieke implementatiemodel met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="69314-160">This section provides detailed instructions for how to configure reverse DNS for Cloud Services in the Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="69314-161">Omgekeerde DNS configureren voor Cloud-Services wordt niet ondersteund via de Azure-portal, Azure CLI 1.0 of 2.0 voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="69314-161">Configuring reverse DNS for Cloud Services is not supported via the Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-to-existing-cloud-services"></a><span data-ttu-id="69314-162">Omgekeerde DNS toevoegen aan bestaande Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="69314-162">Add reverse DNS to existing Cloud Services</span></span>

<span data-ttu-id="69314-163">Een omgekeerde DNS-record toevoegen aan een bestaande Cloudservice:</span><span class="sxs-lookup"><span data-stu-id="69314-163">To add a reverse DNS record to an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="69314-164">Maak een Cloudservice met omgekeerde DNS</span><span class="sxs-lookup"><span data-stu-id="69314-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="69314-165">Een nieuwe Cloudservice maken met de reverse DNS-eigenschap is al opgegeven:</span><span class="sxs-lookup"><span data-stu-id="69314-165">To create a new Cloud Service with the reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="69314-166">Weergave omgekeerde DNS voor bestaande Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="69314-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="69314-167">De omgekeerde DNS-eigenschap voor een bestaande Cloudservice bekijken:</span><span class="sxs-lookup"><span data-stu-id="69314-167">To view the reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="69314-168">Omgekeerde DNS verwijderen uit bestaande Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="69314-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="69314-169">Een omgekeerde DNS-eigenschap van een bestaande Cloudservice verwijderen:</span><span class="sxs-lookup"><span data-stu-id="69314-169">To remove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="69314-170">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="69314-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="69314-171">Hoeveel reverse DNS-records kosten?</span><span class="sxs-lookup"><span data-stu-id="69314-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="69314-172">Ze zijn gratis!</span><span class="sxs-lookup"><span data-stu-id="69314-172">They're free!</span></span>  <span data-ttu-id="69314-173">Er is geen extra kosten voor omgekeerde DNS-records en query's.</span><span class="sxs-lookup"><span data-stu-id="69314-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-the-internet"></a><span data-ttu-id="69314-174">Wordt mijn omgekeerde DNS-records van het internet oplossen?</span><span class="sxs-lookup"><span data-stu-id="69314-174">Will my reverse DNS records resolve from the internet?</span></span>

<span data-ttu-id="69314-175">Ja.</span><span class="sxs-lookup"><span data-stu-id="69314-175">Yes.</span></span> <span data-ttu-id="69314-176">Als u de reverse DNS-eigenschap voor uw Azure-service hebt ingesteld, wordt Azure beheert alle DNS-delegeringen en DNS-zones die zijn vereist om ervoor te zorgen dat de reverse DNS-record wordt herleid voor alle gebruikers van Internet.</span><span class="sxs-lookup"><span data-stu-id="69314-176">Once you set the reverse DNS property for your Azure service, Azure manages all the DNS delegations and DNS zones required to ensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="69314-177">Worden standaard omgekeerde DNS-records gemaakt voor mijn Azure-services?</span><span class="sxs-lookup"><span data-stu-id="69314-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="69314-178">Nee.</span><span class="sxs-lookup"><span data-stu-id="69314-178">No.</span></span> <span data-ttu-id="69314-179">Omgekeerde DNS is een opt-in-functie.</span><span class="sxs-lookup"><span data-stu-id="69314-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="69314-180">Er zijn geen standaard omgekeerde DNS-records worden gemaakt als u niet om ze te configureren.</span><span class="sxs-lookup"><span data-stu-id="69314-180">No default reverse DNS records are created if you choose not to configure them.</span></span>

### <a name="what-is-the-format-for-the-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="69314-181">Wat is de indeling voor de volledig gekwalificeerde domeinnaam (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="69314-181">What is the format for the fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="69314-182">FQDN-namen zijn opgegeven in oplopende volgorde en moeten worden afgesloten met een punt (bijvoorbeeld ' app1.contoso.com.').</span><span class="sxs-lookup"><span data-stu-id="69314-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-the-validation-check-for-the-reverse-dns-ive-specified-fails"></a><span data-ttu-id="69314-183">Wat gebeurt er als de validatiecontrole voor de reverse DNS-server die ik hebt opgegeven mislukt?</span><span class="sxs-lookup"><span data-stu-id="69314-183">What happens if the validation check for the reverse DNS I've specified fails?</span></span>

<span data-ttu-id="69314-184">Wanneer de omgekeerde DNS-validatiecontrole mislukt, mislukt de bewerking voor het configureren van de reverse DNS-record.</span><span class="sxs-lookup"><span data-stu-id="69314-184">Where the reverse DNS validation check fails, the operation to configure the reverse DNS record fails.</span></span> <span data-ttu-id="69314-185">Corrigeer de reverse DNS-waarde als vereist en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="69314-185">Correct the reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="69314-186">Kan ik omgekeerde DNS configureren voor Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="69314-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="69314-187">Nee.</span><span class="sxs-lookup"><span data-stu-id="69314-187">No.</span></span> <span data-ttu-id="69314-188">Omgekeerde DNS wordt niet ondersteund voor de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="69314-188">Reverse DNS is not supported for the Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="69314-189">Kan ik meerdere omgekeerde DNS-records configureren voor mijn Azure-service?</span><span class="sxs-lookup"><span data-stu-id="69314-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="69314-190">Nee.</span><span class="sxs-lookup"><span data-stu-id="69314-190">No.</span></span> <span data-ttu-id="69314-191">Azure biedt ondersteuning voor één omgekeerde DNS-record voor elk Azure Cloud Service of PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="69314-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="69314-192">Kan ik omgekeerde DNS voor IPv6-PublicIpAddress-resources configureren?</span><span class="sxs-lookup"><span data-stu-id="69314-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="69314-193">Nee.</span><span class="sxs-lookup"><span data-stu-id="69314-193">No.</span></span> <span data-ttu-id="69314-194">Azure momenteel ondersteunt reverse DNS alleen voor IPv4 PublicIpAddress resources en Cloudservices.</span><span class="sxs-lookup"><span data-stu-id="69314-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-to-external-domains-from-my-azure-compute-services"></a><span data-ttu-id="69314-195">Kan ik e-mailberichten verzenden naar externe domeinen uit mijn Azure Compute-services?</span><span class="sxs-lookup"><span data-stu-id="69314-195">Can I send emails to external domains from my Azure Compute services?</span></span>

<span data-ttu-id="69314-196">Nee.</span><span class="sxs-lookup"><span data-stu-id="69314-196">No.</span></span> [<span data-ttu-id="69314-197">Azure Compute-services bieden geen ondersteuning voor externe domeinen verzenden e-mailberichten</span><span class="sxs-lookup"><span data-stu-id="69314-197">Azure Compute services do not support sending emails to external domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="69314-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="69314-198">Next steps</span></span>

<span data-ttu-id="69314-199">Zie voor meer informatie over omgekeerde DNS [achterwaartse DNS-zoekopdracht op Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="69314-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="69314-200">Meer informatie over hoe [zone voor reverse lookup voor uw Internetprovider toegewezen IP-adresbereik in Azure DNS hosten](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="69314-200">Learn how to [host the reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

