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
# <a name="configure-reverse-dns-for-services-hosted-in-azure"></a>Omgekeerde DNS voor services die worden gehost in Azure configureren

Dit artikel wordt uitgelegd hoe tooconfigure reverse DNS-zoekacties voor services die worden gehost in Azure.

Services in Azure gebruiken IP-adressen toegewezen door Azure en het eigendom van Microsoft. Deze omgekeerde DNS-records (PTR-records) moeten worden gemaakt in Hallo bijbehorende die eigendom zijn van Microsoft omgekeerde DNS-lookup zones. Dit artikel wordt uitgelegd hoe toodo dit.

Dit scenario moet niet verwarren met Hallo mogelijkheid te[Hallo omgekeerde DNS-zones lookup voor uw toegewezen IP-adresbereiken in Azure DNS hosten](dns-reverse-dns-hosting.md). In dit geval moeten Hallo IP-adresbereiken dat wordt vertegenwoordigd door een zone voor reverse lookup Hallo worden toegewezen tooyour organisatie, doorgaans door uw Internetprovider.

Voordat u dit artikel leest, moet u bekend bent met dit [overzicht van de reverse DNS- en biedt ondersteuning in Azure](dns-reverse-dns-overview.md).

Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../azure-resource-manager/resource-manager-deployment-model.md).
* Hallo Resource Manager-implementatiemodel, compute-bronnen (zoals virtuele machines, virtuele-machineschaalsets of Service Fabric-clusters) beschikbaar worden gemaakt via een PublicIpAddress-resource. Omgekeerde DNS-zoekacties zijn geconfigureerd met Hallo 'ReverseFqdn'-eigenschap van Hallo PublicIpAddress.
* In de klassieke implementatiemodel Hallo rekenresources zichtbaar cloudservices gebruikt. Omgekeerde DNS-zoekacties zijn geconfigureerd met Hallo 'ReverseDnsFqdn'-eigenschap van Hallo Service in de Cloud.

Omgekeerde DNS is momenteel niet ondersteund voor hello Azure App Service.

## <a name="validation-of-reverse-dns-records"></a>Validatie van de reverse DNS-records

Een derde partij mag geen kunnen toocreate omgekeerde DNS-records voor de Azure-service toewijzing tooyour DNS-domeinen. tooprevent, Azure kunt alleen Hallo maken van een omgekeerde DNS-record waar domeinnaam in Hallo omgekeerde DNS-record is Hallo gelijk zijn aan of wordt omgezet in DNS-naam of IP-adres van een PublicIpAddress of Cloud Hallo-Service in Hallo dezelfde Azure-abonnement.

Deze validatie wordt alleen uitgevoerd wanneer Hallo omgekeerde DNS-record wordt ingesteld of gewijzigd. Periodieke opnieuw validatie is niet uitgevoerd.

Voorbeeld: Stel Hallo PublicIpAddress resource Hallo DNS-naam contosoapp1.northus.cloudapp.azure.com en IP-adres 23.96.52.53 heeft. Hallo ReverseFqdn voor Hallo die publicipaddress kan worden opgegeven als:
* Hallo DNS-naam voor Hallo PublicIpAddress, contosoapp1.northus.cloudapp.azure.com
* Hallo DNS-naam voor een andere PublicIpAddress in Hallo hetzelfde abonnement, zoals contosoapp2.westus.cloudapp.azure.com
* Een vanity DNS-naam, zoals app1.contoso.com, zolang deze naam *eerste* geconfigureerd als een CNAME-toocontosoapp1.northus.cloudapp.azure.com of tooa verschillende PublicIpAddress in Hallo hetzelfde abonnement.
* Een vanity DNS-naam, zoals app1.contoso.com, zolang deze naam *eerste* is geconfigureerd als een IP-adres van een record toohello 23.96.52.53 of toohello IP-adres van een andere PublicIpAddress in Hallo hetzelfde abonnement.

Hallo dezelfde beperkingen gelden tooreverse DNS voor Cloud-Services.


## <a name="reverse-dns-for-publicipaddress-resources"></a>Omgekeerde DNS voor PublicIpAddress resources

Deze sectie bevat gedetailleerde instructies voor hoe tooconfigure reverse DNS-PublicIpAddress resources Hallo Resource Manager-implementatiemodel, met Azure PowerShell, Azure CLI 1.0 of 2.0 voor Azure CLI. Configureren van omgekeerde DNS voor PublicIpAddress bronnen is momenteel niet ondersteund via hello Azure-portal.

Azure momenteel ondersteunt reverse DNS alleen voor IPv4 PublicIpAddress resources. Dit wordt niet ondersteund voor IPv6.

### <a name="add-reverse-dns-tooan-existing-publicipaddresses"></a>Omgekeerde DNS-tooan bestaande PublicIpAddresses toevoegen

#### <a name="powershell"></a>PowerShell

tooadd omgekeerde DNS-tooan PublicIpAddress bestaande:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

tooadd reverse DNS-tooan bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings = New-Object -TypeName "Microsoft.Azure.Commands.Network.Models.PSPublicIpAddressDnsSettings"
$pip.DnsSettings.DomainNameLabel = "contosoapp1"
$pip.DnsSettings.ReverseFqdn = "contosoapp1.westus.cloudapp.azure.com."
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

tooadd omgekeerde DNS-tooan PublicIpAddress bestaande:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -f contosoapp1.westus.cloudapp.azure.com.
```

tooadd reverse DNS-tooan bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup -d contosoapp1 -f contosoapp1.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

tooadd omgekeerde DNS-tooan PublicIpAddress bestaande:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com.
```

tooadd reverse DNS-tooan bestaande PublicIpAddress die nog niet over een DNS-naam, moet u ook een DNS-naam opgeven:

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn contosoapp1.westus.cloudapp.azure.com --dns-name contosoapp1
```

### <a name="create-a-public-ip-address-with-reverse-dns"></a>Maken van een openbaar IP-adres met de reverse DNS

een nieuwe PublicIpAddress met Hallo omgekeerde DNS-eigenschap is al opgegeven toocreate:

#### <a name="powershell"></a>PowerShell

```powershell
New-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup" -Location "WestUS" -AllocationMethod Dynamic -DomainNameLabel "contosoapp2" -ReverseFqdn "contosoapp2.westus.cloudapp.azure.com."
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip create -n PublicIp -g MyResourceGroup -l westus -d contosoapp3 -f contosoapp3.westus.cloudapp.azure.com.
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip create --name PublicIp --resource-group MyResourceGroup --location westcentralus --dns-name contosoapp1 --reverse-fqdn contosoapp1.westcentralus.cloudapp.azure.com
```

### <a name="view-reverse-dns-for-an-existing-publicipaddress"></a>Weergave omgekeerde DNS voor een bestaande PublicIpAddress

tooview hello geconfigureerde waarde voor een bestaande PublicIpAddress:

#### <a name="powershell"></a>PowerShell

```powershell
Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip show -n PublicIp -g MyResourceGroup
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip show --name PublicIp --resource-group MyResourceGroup
```

### <a name="remove-reverse-dns-from-existing-public-ip-addresses"></a>Omgekeerde DNS verwijderen uit bestaande openbare IP-adressen

een omgekeerde DNS-eigenschap van een bestaande PublicIpAddress tooremove:

#### <a name="powershell"></a>PowerShell

```powershell
$pip = Get-AzureRmPublicIpAddress -Name "PublicIp" -ResourceGroupName "MyResourceGroup"
$pip.DnsSettings.ReverseFqdn = ""
Set-AzureRmPublicIpAddress -PublicIpAddress $pip
```

#### <a name="azure-cli-10"></a>Azure CLI 1.0

```azurecli
azure network public-ip set -n PublicIp -g MyResourceGroup –f ""
```

#### <a name="azure-cli-20"></a>Azure CLI 2.0

```azurecli
az network public-ip update --resource-group MyResourceGroup --name PublicIp --reverse-fqdn ""
```


## <a name="configure-reverse-dns-for-cloud-services"></a>Omgekeerde DNS configureren voor Cloud-Services

Deze sectie bevat gedetailleerde instructies voor hoe tooconfigure DNS reverse voor Cloudservices in Hallo klassieke implementatiemodel met Azure PowerShell. Omgekeerde DNS configureren voor Cloud-Services wordt niet ondersteund via hello Azure-portal, Azure CLI 1.0 of 2.0 voor Azure CLI.

### <a name="add-reverse-dns-tooexisting-cloud-services"></a>Omgekeerde DNS-tooexisting Cloud Services toevoegen

tooadd een omgekeerde DNS-record tooan bestaande Cloudservice:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="create-a-cloud-service-with-reverse-dns"></a>Maak een Cloudservice met omgekeerde DNS

een nieuwe Cloudservice met de Hallo omgekeerde DNS-eigenschap is al opgegeven toocreate:

```powershell
New-AzureService –ServiceName "contosoapp1" –Location "West US" –Description "App1 with Reverse DNS" –ReverseDnsFqdn "contosoapp1.cloudapp.net."
```

### <a name="view-reverse-dns-for-existing-cloud-services"></a>Weergave omgekeerde DNS voor bestaande Cloud-Services

tooview hello omgekeerde DNS-eigenschap voor een bestaande Cloudservice:

```powershell
Get-AzureService "contosoapp1"
```

### <a name="remove-reverse-dns-from-existing-cloud-services"></a>Omgekeerde DNS verwijderen uit bestaande Cloud-Services

een omgekeerde DNS-eigenschap van een bestaande Cloudservice tooremove:

```powershell
Set-AzureService –ServiceName "contosoapp1" –Description "App1 with Reverse DNS" –ReverseDnsFqdn ""
```

## <a name="faq"></a>Veelgestelde vragen

### <a name="how-much-do-reverse-dns-records-cost"></a>Hoeveel reverse DNS-records kosten?

Ze zijn gratis!  Er is geen extra kosten voor omgekeerde DNS-records en query's.

### <a name="will-my-reverse-dns-records-resolve-from-hello-internet"></a>Wordt mijn omgekeerde DNS-records omzetten vanuit internet Hallo?

Ja. Als u Hallo omgekeerde DNS-eigenschap ingesteld voor uw Azure-service, Azure beheert alle Hallo DNS-delegeringen en DNS-zones vereist tooensure die reverse DNS-record wordt omgezet voor alle gebruikers van het Internet.

### <a name="are-default-reverse-dns-records-created-for-my-azure-services"></a>Worden standaard omgekeerde DNS-records gemaakt voor mijn Azure-services?

Nee. Omgekeerde DNS is een opt-in-functie. Er is geen standaard omgekeerde DNS-records worden gemaakt als u ervoor geen tooconfigure kiest ze.

### <a name="what-is-hello-format-for-hello-fully-qualified-domain-name-fqdn"></a>Wat is Hallo-indeling voor Hallo volledig gekwalificeerde domeinnaam (FQDN)?

FQDN-namen zijn opgegeven in oplopende volgorde en moeten worden afgesloten met een punt (bijvoorbeeld ' app1.contoso.com.').

### <a name="what-happens-if-hello-validation-check-for-hello-reverse-dns-ive-specified-fails"></a>Wat gebeurt er als de validatiecontrole Hallo op Hallo omgekeerde DNS ik hebt opgegeven mislukt?

Indien hello omgekeerde DNS-validatie van controle is mislukt, mislukt de Hallo bewerking tooconfigure Hallo omgekeerde DNS-record. Juiste Hallo omgekeerde DNS-waarde als vereist, en probeer het opnieuw.

### <a name="can-i-configure-reverse-dns-for-azure-app-service"></a>Kan ik omgekeerde DNS configureren voor Azure App Service?

Nee. Omgekeerde DNS wordt niet ondersteund voor hello Azure App Service.

### <a name="can-i-configure-multiple-reverse-dns-records-for-my-azure-service"></a>Kan ik meerdere omgekeerde DNS-records configureren voor mijn Azure-service?

Nee. Azure biedt ondersteuning voor één omgekeerde DNS-record voor elk Azure Cloud Service of PublicIpAddress.

### <a name="can-i-configure-reverse-dns-for-ipv6-publicipaddress-resources"></a>Kan ik omgekeerde DNS voor IPv6-PublicIpAddress-resources configureren?

Nee. Azure momenteel ondersteunt reverse DNS alleen voor IPv4 PublicIpAddress resources en Cloudservices.

### <a name="can-i-send-emails-tooexternal-domains-from-my-azure-compute-services"></a>Kan ik verzenden e-mailberichten tooexternal domeinen uit mijn Azure Compute-services?

Nee. [Azure Compute-services bieden geen ondersteuning voor verzenden e-mailberichten tooexternal domeinen](https://blogs.msdn.microsoft.com/mast/2016/04/04/sending-e-mail-from-azure-compute-resource-to-external-domains/)

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over omgekeerde DNS [achterwaartse DNS-zoekopdracht op Wikipedia](http://en.wikipedia.org/wiki/Reverse_DNS_lookup).
<br>
Meer informatie over hoe te[host Hallo-zone voor reverse lookup voor uw Internetprovider toegewezen IP-adresbereik in Azure DNS](dns-reverse-dns-for-azure-services.md).

