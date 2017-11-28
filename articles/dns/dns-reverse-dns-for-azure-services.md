---
title: aaaReverse DNS voor Azure-services | Microsoft Docs
description: Meer informatie over hoe tooconfigure reverse DNS-zoekacties voor services die worden gehost in Azure
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
ms.openlocfilehash: c6fe1d80232f124be86dd7fc57abc20699be7eba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a><span data-ttu-id="5f5e3-103">Omgekeerde DNS voor services die worden gehost in Azure configureren</span><span class="sxs-lookup"><span data-stu-id="5f5e3-103">Configure reverse DNS for services hosted in Azure</span></span>

<span data-ttu-id="5f5e3-104">Dit artikel wordt uitgelegd hoe tooconfigure reverse DNS-zoekacties voor services die worden gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-104">This article explains how tooconfigure reverse DNS lookups for services hosted in Azure.</span></span>

<span data-ttu-id="5f5e3-105">Services in Azure gebruiken IP-adressen toegewezen door Azure en het eigendom van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-105">Services in Azure use IP addresses assigned by Azure and owned by Microsoft.</span></span> <span data-ttu-id="5f5e3-106">Deze omgekeerde DNS-records (PTR-records) moeten worden gemaakt in Hallo bijbehorende die eigendom zijn van Microsoft omgekeerde DNS-lookup zones.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-106">These reverse DNS records (PTR records) must be created in hello corresponding Microsoft-owned reverse DNS lookup zones.</span></span> <span data-ttu-id="5f5e3-107">Dit artikel wordt uitgelegd hoe toodo dit.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-107">This article explains how toodo this.</span></span>

<span data-ttu-id="5f5e3-108">Dit scenario moet niet verwarren met Hallo mogelijkheid te[Hallo omgekeerde DNS-zones lookup voor uw toegewezen IP-adresbereiken in Azure DNS hosten](dns-reverse-dns-hosting.md).</span><span class="sxs-lookup"><span data-stu-id="5f5e3-108">This scenario should not be confused with hello ability too[host hello reverse DNS lookup zones for your assigned IP ranges in Azure DNS](dns-reverse-dns-hosting.md).</span></span> <span data-ttu-id="5f5e3-109">In dit geval moeten Hallo IP-adresbereiken dat wordt vertegenwoordigd door een zone voor reverse lookup Hallo worden toegewezen tooyour organisatie, doorgaans door uw Internetprovider.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-109">In this case, hello IP ranges represented by hello reverse lookup zone must be assigned tooyour organization, typically by your ISP.</span></span>

<span data-ttu-id="5f5e3-110">Voordat u dit artikel leest, moet u bekend bent met dit [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f5e3-110">Before reading this article, you should be familiar with this [Overview of reverse DNS and support in Azure](dns-reverse-dns-overview.md).</span></span>

<span data-ttu-id="5f5e3-111">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5f5e3-111">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>
* <span data-ttu-id="5f5e3-112">Hallo Resource Manager-implementatiemodel, compute-bronnen (zoals virtuele machines, virtuele-machineschaalsets of Service Fabric-clusters) beschikbaar worden gemaakt via een PublicIpAddress-resource.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-112">In hello Resource Manager deployment model, compute resources (such as virtual machines, virtual machine scale sets, or Service Fabric clusters) are exposed via a PublicIpAddress resource.</span></span> <span data-ttu-id="5f5e3-113">Omgekeerde DNS-zoekacties zijn geconfigureerd met Hallo 'ReverseFqdn'-eigenschap van Hallo PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-113">Reverse DNS lookups are configured using hello 'ReverseFqdn' property of hello PublicIpAddress.</span></span>
* <span data-ttu-id="5f5e3-114">In de klassieke implementatiemodel Hallo rekenresources zichtbaar cloudservices gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-114">In hello Classic deployment model, compute resources are exposed using Cloud Services.</span></span> <span data-ttu-id="5f5e3-115">Omgekeerde DNS-zoekacties zijn geconfigureerd met Hallo 'ReverseDnsFqdn'-eigenschap van Hallo Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-115">Reverse DNS lookups are configured using hello 'ReverseDnsFqdn' property of hello Cloud Service.</span></span>

<span data-ttu-id="5f5e3-116">Omgekeerde DNS is momenteel niet ondersteund voor hello Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-116">Reverse DNS is not currently supported for hello Azure App Service.</span></span>

## <a name="validation-of-reverse-dns-records"></a><span data-ttu-id="5f5e3-117">Validatie van de reverse DNS-records</span><span class="sxs-lookup"><span data-stu-id="5f5e3-117">Validation of reverse DNS records</span></span>

<span data-ttu-id="5f5e3-118">Een derde partij mag geen kunnen toocreate omgekeerde DNS-records voor de Azure-service toewijzing tooyour DNS-domeinen.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-118">A third party should not be able toocreate reverse DNS records for their Azure service mapping tooyour DNS domains.</span></span> <span data-ttu-id="5f5e3-119">tooprevent, Azure kunt alleen Hallo maken van een omgekeerde DNS-record waar domeinnaam in Hallo omgekeerde DNS-record is Hallo gelijk zijn aan of wordt omgezet in DNS-naam of IP-adres van een PublicIpAddress of Cloud Hallo-Service in Hallo dezelfde Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-119">tooprevent this, Azure only allows hello creation of a reverse DNS record where domain name specified in hello reverse DNS record is hello same as, or resolves to, hello DNS name or IP address of a PublicIpAddress or Cloud Service in hello same Azure subscription.</span></span>

<span data-ttu-id="5f5e3-120">Deze validatie wordt alleen uitgevoerd wanneer Hallo omgekeerde DNS-record wordt ingesteld of gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-120">This validation is only performed when hello reverse DNS record is set or modified.</span></span> <span data-ttu-id="5f5e3-121">Periodieke opnieuw validatie is niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-121">Periodic re-validation is not performed.</span></span>

<span data-ttu-id="5f5e3-122">Voorbeeld: Stel Hallo PublicIpAddress resource Hallo DNS-naam contosoapp1.northus.cloudapp.azure.com en IP-adres 23.96.52.53 heeft.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-122">For example: suppose hello PublicIpAddress resource has hello DNS name contosoapp1.northus.cloudapp.azure.com and IP address 23.96.52.53.</span></span> <span data-ttu-id="5f5e3-123">Hallo ReverseFqdn voor Hallo die publicipaddress kan worden opgegeven als:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-123">hello ReverseFqdn for hello PublicIpAddress can be specified as:</span></span>
* <span data-ttu-id="5f5e3-124">Hallo DNS-naam voor Hallo PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="5f5e3-124">hello DNS name for hello PublicIpAddress, contosoapp1.northus.cloudapp.azure.com</span></span>
* <span data-ttu-id="5f5e3-125">Hallo DNS-naam voor een andere PublicIpAddress in Hallo hetzelfde abonnement, zoals contosoapp2.westus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="5f5e3-125">hello DNS name for a different PublicIpAddress in hello same subscription, such as contosoapp2.westus.cloudapp.azure.com</span></span>
* <span data-ttu-id="5f5e3-126">Een vanity DNS-naam, zoals app1.contoso.com, zolang deze naam *eerste* geconfigureerd als een CNAME-toocontosoapp1.northus.cloudapp.azure.com of tooa verschillende PublicIpAddress in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-126">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as a CNAME toocontosoapp1.northus.cloudapp.azure.com, or tooa different PublicIpAddress in hello same subscription.</span></span>
* <span data-ttu-id="5f5e3-127">Een vanity DNS-naam, zoals app1.contoso.com, zolang deze naam *eerste* is geconfigureerd als een IP-adres van een record toohello 23.96.52.53 of toohello IP-adres van een andere PublicIpAddress in Hallo hetzelfde abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-127">A vanity DNS name, such as app1.contoso.com, so long as this name is *first* configured as an A record toohello IP address 23.96.52.53, or toohello IP address of a different PublicIpAddress in hello same subscription.</span></span>

<span data-ttu-id="5f5e3-128">Hallo dezelfde beperkingen gelden tooreverse DNS voor Cloud-Services.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-128">hello same constraints apply tooreverse DNS for Cloud Services.</span></span>


## <a name="reverse-dns-for-publicipaddress-resources"></a><span data-ttu-id="5f5e3-129">Omgekeerde DNS voor PublicIpAddress resources</span><span class="sxs-lookup"><span data-stu-id="5f5e3-129">Reverse DNS for PublicIpAddress resources</span></span>

<span data-ttu-id="5f5e3-130">Deze sectie bevat gedetailleerde instructies voor hoe tooconfigure reverse DNS-PublicIpAddress resources Hallo Resource Manager-implementatiemodel, met Azure PowerShell, Azure CLI 1.0 of 2.0 voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-130">This section provides detailed instructions for how tooconfigure reverse DNS for PublicIpAddress resources in hello Resource Manager deployment model, using either Azure PowerShell, Azure CLI 1.0, or Azure CLI 2.0.</span></span> <span data-ttu-id="5f5e3-131">Configureren van omgekeerde DNS voor PublicIpAddress bronnen is momenteel niet ondersteund via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-131">Configuring reverse DNS for PublicIpAddress resources is not currently supported via hello Azure portal.</span></span>

<span data-ttu-id="5f5e3-132">Azure momenteel ondersteunt reverse DNS alleen voor IPv4 PublicIpAddress resources.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-132">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources.</span></span> <span data-ttu-id="5f5e3-133">Dit wordt niet ondersteund voor IPv6.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-133">It is not supported for IPv6.</span></span>

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a><span data-ttu-id="5f5e3-134">Omgekeerde DNS-tooan bestaande PublicIpAddresses toevoegen</span><span class="sxs-lookup"><span data-stu-id="5f5e3-134">Add reverse DNS tooan existing PublicIpAddresses</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f5e3-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f5e3-135">PowerShell</span></span>

<span data-ttu-id="5f5e3-136">tooadd omgekeerde DNS-tooan PublicIpAddress bestaande:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-136">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

<span data-ttu-id="5f5e3-137">tooadd reverse DNS-tooan bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-137">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5f5e3-138">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-138">Azure CLI 1.0</span></span>

<span data-ttu-id="5f5e3-139">tooadd omgekeerde DNS-tooan PublicIpAddress bestaande:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-139">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="5f5e3-140">tooadd reverse DNS-tooan bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-140">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5f5e3-141">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-141">Azure CLI 2.0</span></span>

<span data-ttu-id="5f5e3-142">tooadd omgekeerde DNS-tooan PublicIpAddress bestaande:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-142">tooadd reverse DNS tooan existing PublicIpAddress:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

<span data-ttu-id="5f5e3-143">tooadd reverse DNS-tooan bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-143">tooadd reverse DNS tooan existing PublicIpAddress that doesn't already have a DNS name, you must also specify a DNS name:</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a><span data-ttu-id="5f5e3-144">Maken van een openbaar IP-adres met de reverse DNS</span><span class="sxs-lookup"><span data-stu-id="5f5e3-144">Create a Public IP Address with reverse DNS</span></span>

<span data-ttu-id="5f5e3-145">een nieuwe PublicIpAddress met Hallo omgekeerde DNS-eigenschap is al opgegeven toocreate:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-145">toocreate a new PublicIpAddress with hello reverse DNS property already specified:</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f5e3-146">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f5e3-146">PowerShell</span></span>

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5f5e3-147">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-147">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5f5e3-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-148">Azure CLI 2.0</span></span>

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a><span data-ttu-id="5f5e3-149">Weergave omgekeerde DNS voor een bestaande PublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5f5e3-149">View reverse DNS for an existing PublicIpAddress</span></span>

<span data-ttu-id="5f5e3-150">tooview hello geconfigureerde waarde voor een bestaande PublicIpAddress:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-150">tooview hello configured value for an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f5e3-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f5e3-151">PowerShell</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5f5e3-152">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-152">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5f5e3-153">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-153">Azure CLI 2.0</span></span>

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a><span data-ttu-id="5f5e3-154">Omgekeerde DNS verwijderen uit bestaande openbare IP-adressen</span><span class="sxs-lookup"><span data-stu-id="5f5e3-154">Remove reverse DNS from existing Public IP Addresses</span></span>

<span data-ttu-id="5f5e3-155">een omgekeerde DNS-eigenschap van een bestaande PublicIpAddress tooremove:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-155">tooremove a reverse DNS property from an existing PublicIpAddress:</span></span>

#### <a name="powershell"></a><span data-ttu-id="5f5e3-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f5e3-156">PowerShell</span></span>

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a><span data-ttu-id="5f5e3-157">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-157">Azure CLI 1.0</span></span>

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a><span data-ttu-id="5f5e3-158">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5f5e3-158">Azure CLI 2.0</span></span>

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a><span data-ttu-id="5f5e3-159">Omgekeerde DNS configureren voor Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="5f5e3-159">Configure reverse DNS for Cloud Services</span></span>

<span data-ttu-id="5f5e3-160">Deze sectie bevat gedetailleerde instructies voor hoe tooconfigure DNS reverse voor Cloudservices in Hallo klassieke implementatiemodel met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-160">This section provides detailed instructions for how tooconfigure reverse DNS for Cloud Services in hello Classic deployment model, using Azure PowerShell.</span></span> <span data-ttu-id="5f5e3-161">Omgekeerde DNS configureren voor Cloud-Services wordt niet ondersteund via hello Azure-portal, Azure CLI 1.0 of 2.0 voor Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-161">Configuring reverse DNS for Cloud Services is not supported via hello Azure portal, Azure CLI 1.0, or Azure CLI 2.0.</span></span>

### <a name="add-reverse-dns-tooexisting-cloud-services"></a><span data-ttu-id="5f5e3-162">Omgekeerde DNS-tooexisting Cloud Services toevoegen</span><span class="sxs-lookup"><span data-stu-id="5f5e3-162">Add reverse DNS tooexisting Cloud Services</span></span>

<span data-ttu-id="5f5e3-163">tooadd een omgekeerde DNS-record tooan bestaande Cloudservice:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-163">tooadd a reverse DNS record tooan existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a><span data-ttu-id="5f5e3-164">Maak een Cloudservice met omgekeerde DNS</span><span class="sxs-lookup"><span data-stu-id="5f5e3-164">Create a Cloud Service with reverse DNS</span></span>

<span data-ttu-id="5f5e3-165">een nieuwe Cloudservice met de Hallo omgekeerde DNS-eigenschap is al opgegeven toocreate:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-165">toocreate a new Cloud Service with hello reverse DNS property already specified:</span></span>

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a><span data-ttu-id="5f5e3-166">Weergave omgekeerde DNS voor bestaande Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="5f5e3-166">View reverse DNS for existing Cloud Services</span></span>

<span data-ttu-id="5f5e3-167">tooview hello omgekeerde DNS-eigenschap voor een bestaande Cloudservice:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-167">tooview hello reverse DNS property for an existing Cloud Service:</span></span>

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a><span data-ttu-id="5f5e3-168">Omgekeerde DNS verwijderen uit bestaande Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="5f5e3-168">Remove reverse DNS from existing Cloud Services</span></span>

<span data-ttu-id="5f5e3-169">een omgekeerde DNS-eigenschap van een bestaande Cloudservice tooremove:</span><span class="sxs-lookup"><span data-stu-id="5f5e3-169">tooremove a reverse DNS property from an existing Cloud Service:</span></span>

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a><span data-ttu-id="5f5e3-170">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="5f5e3-170">FAQ</span></span>

### <a name="how-much-do-reverse-dns-records-cost"></a><span data-ttu-id="5f5e3-171">Hoeveel reverse DNS-records kosten?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-171">How much do reverse DNS records cost?</span></span>

<span data-ttu-id="5f5e3-172">Ze zijn gratis!</span><span class="sxs-lookup"><span data-stu-id="5f5e3-172">They're free!</span></span>  <span data-ttu-id="5f5e3-173">Er is geen extra kosten voor omgekeerde DNS-records en query's.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-173">There is no additional cost for reverse DNS records or queries.</span></span>

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a><span data-ttu-id="5f5e3-174">Wordt mijn omgekeerde DNS-records omzetten vanuit internet Hallo?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-174">Will my reverse DNS records resolve from hello internet?</span></span>

<span data-ttu-id="5f5e3-175">Ja.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-175">Yes.</span></span> <span data-ttu-id="5f5e3-176">Als u Hallo omgekeerde DNS-eigenschap ingesteld voor uw Azure-service, Azure beheert alle Hallo DNS-delegeringen en DNS-zones vereist tooensure die reverse DNS-record wordt omgezet voor alle gebruikers van het Internet.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-176">Once you set hello reverse DNS property for your Azure service, Azure manages all hello DNS delegations and DNS zones required tooensure that reverse DNS record resolves for all Internet users.</span></span>

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a><span data-ttu-id="5f5e3-177">Worden standaard omgekeerde DNS-records gemaakt voor mijn Azure-services?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-177">Are default reverse DNS records created for my Azure services?</span></span>

<span data-ttu-id="5f5e3-178">Nee.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-178">No.</span></span> <span data-ttu-id="5f5e3-179">Omgekeerde DNS is een opt-in-functie.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-179">Reverse DNS is an opt-in feature.</span></span> <span data-ttu-id="5f5e3-180">Er is geen standaard omgekeerde DNS-records worden gemaakt als u ervoor geen tooconfigure kiest ze.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-180">No default reverse DNS records are created if you choose not tooconfigure them.</span></span>

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a><span data-ttu-id="5f5e3-181">Wat is Hallo-indeling voor Hallo volledig gekwalificeerde domeinnaam (FQDN)?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-181">What is hello format for hello fully-qualified domain name (FQDN)?</span></span>

<span data-ttu-id="5f5e3-182">FQDN-namen zijn opgegeven in oplopende volgorde en moeten worden afgesloten met een punt (bijvoorbeeld ' app1.contoso.com.').</span><span class="sxs-lookup"><span data-stu-id="5f5e3-182">FQDNs are specified in forward order, and must be terminated by a dot (for example, "app1.contoso.com.").</span></span>

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a><span data-ttu-id="5f5e3-183">Wat gebeurt er als de validatiecontrole Hallo op Hallo omgekeerde DNS ik hebt opgegeven mislukt?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-183">What happens if hello validation check for hello reverse DNS I've specified fails?</span></span>

<span data-ttu-id="5f5e3-184">Indien hello omgekeerde DNS-validatie van controle is mislukt, mislukt de Hallo bewerking tooconfigure Hallo omgekeerde DNS-record.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-184">Where hello reverse DNS validation check fails, hello operation tooconfigure hello reverse DNS record fails.</span></span> <span data-ttu-id="5f5e3-185">Juiste Hallo omgekeerde DNS-waarde als vereist, en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-185">Correct hello reverse DNS value as required, and retry.</span></span>

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a><span data-ttu-id="5f5e3-186">Kan ik omgekeerde DNS configureren voor Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-186">Can I configure reverse DNS for Azure App Service?</span></span>

<span data-ttu-id="5f5e3-187">Nee.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-187">No.</span></span> <span data-ttu-id="5f5e3-188">Omgekeerde DNS wordt niet ondersteund voor hello Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-188">Reverse DNS is not supported for hello Azure App Service.</span></span>

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a><span data-ttu-id="5f5e3-189">Kan ik meerdere omgekeerde DNS-records configureren voor mijn Azure-service?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-189">Can I configure multiple reverse DNS records for my Azure service?</span></span>

<span data-ttu-id="5f5e3-190">Nee.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-190">No.</span></span> <span data-ttu-id="5f5e3-191">Azure biedt ondersteuning voor één omgekeerde DNS-record voor elk Azure Cloud Service of PublicIpAddress.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-191">Azure supports a single reverse DNS record for each Azure Cloud Service or PublicIpAddress.</span></span>

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a><span data-ttu-id="5f5e3-192">Kan ik omgekeerde DNS voor IPv6-PublicIpAddress-resources configureren?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-192">Can I configure reverse DNS for IPv6 PublicIpAddress resources?</span></span>

<span data-ttu-id="5f5e3-193">Nee.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-193">No.</span></span> <span data-ttu-id="5f5e3-194">Azure momenteel ondersteunt reverse DNS alleen voor IPv4 PublicIpAddress resources en Cloudservices.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-194">Azure currently supports reverse DNS only for IPv4 PublicIpAddress resources and Cloud Services.</span></span>

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a><span data-ttu-id="5f5e3-195">Kan ik verzenden e-mailberichten tooexternal domeinen uit mijn Azure Compute-services?</span><span class="sxs-lookup"><span data-stu-id="5f5e3-195">Can I send emails tooexternal domains from my Azure Compute services?</span></span>

<span data-ttu-id="5f5e3-196">Nee.</span><span class="sxs-lookup"><span data-stu-id="5f5e3-196">No.</span></span> [<span data-ttu-id="5f5e3-197">Azure Compute-services bieden geen ondersteuning voor verzenden e-mailberichten tooexternal domeinen</span><span class="sxs-lookup"><span data-stu-id="5f5e3-197">Azure Compute services do not support sending emails tooexternal domains</span></span>](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a><span data-ttu-id="5f5e3-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f5e3-198">Next steps</span></span>

<span data-ttu-id="5f5e3-199">Zie voor meer informatie over omgekeerde DNS [achterwaartse DNS-zoekopdracht op Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span><span class="sxs-lookup"><span data-stu-id="5f5e3-199">For more information on reverse DNS, see [reverse DNS lookup on Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).</span></span>
<br>
<span data-ttu-id="5f5e3-200">Meer informatie over hoe te[host Hallo-zone voor reverse lookup voor uw Internetprovider toegewezen IP-adresbereik in Azure DNS](dns-reverse-dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="5f5e3-200">Learn how too[host hello reverse lookup zone for your ISP-assigned IP range in Azure DNS](dns-reverse-dns-for-azure-services.md).</span></span>

