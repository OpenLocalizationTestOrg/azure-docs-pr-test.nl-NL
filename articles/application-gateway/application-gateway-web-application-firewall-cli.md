---
title: aaaConfigure web application firewall - Azure Application Gateway | Microsoft Docs
description: In dit artikel biedt richtlijnen voor hoe toostart met behulp van web application firewall op een bestaande of nieuwe application gateway.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="ec397-103">Web application firewall configureren op een nieuwe of bestaande toepassingsgateway met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ec397-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec397-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ec397-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="ec397-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec397-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="ec397-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="ec397-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="ec397-107">Meer informatie over hoe toocreate web application firewall ingeschakeld voor toepassingsgateway of web application firewall tooan bestaande toepassingsgateway toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ec397-107">Learn how toocreate a web application firewall enabled application gateway or add web application firewall tooan existing application gateway.</span></span>

<span data-ttu-id="ec397-108">Hallo web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.</span><span class="sxs-lookup"><span data-stu-id="ec397-108">hello web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="ec397-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="ec397-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="ec397-110">Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="ec397-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="ec397-111">Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere.</span><span class="sxs-lookup"><span data-stu-id="ec397-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="ec397-112">toofind een volledige lijst van ondersteunde functies, gaat u naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec397-112">toofind a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="ec397-113">Hallo volgende artikel laat zien hoe te[web application firewall tooan bestaande toepassingsgateway toevoegen](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="ec397-113">hello following article shows how too[add web application firewall tooan existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![afbeelding van scenario][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="ec397-115">Voorwaarde: Installeer hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ec397-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="ec397-116">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="ec397-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="ec397-117">WAF configuratie verschillen</span><span class="sxs-lookup"><span data-stu-id="ec397-117">WAF configuration differences</span></span>

<span data-ttu-id="ec397-118">Als u hebt gelezen [een toepassingsgateway maken met Azure CLI](application-gateway-create-gateway-cli.md), u begrijpt Hallo SKU instellingen tooconfigure bij het maken van een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="ec397-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand hello SKU settings tooconfigure when creating an application gateway.</span></span> <span data-ttu-id="ec397-119">WAF biedt extra instellingen toodefine bij het configureren van Hallo SKU voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="ec397-119">WAF provides additional settings toodefine when configuring hello SKU on an application gateway.</span></span> <span data-ttu-id="ec397-120">Er zijn geen aanvullende wijzigingen die u op Hallo application gateway zelf aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="ec397-120">There are no additional changes that you make on hello application gateway itself.</span></span>

| <span data-ttu-id="ec397-121">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="ec397-121">**Setting**</span></span> | <span data-ttu-id="ec397-122">**Details**</span><span class="sxs-lookup"><span data-stu-id="ec397-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="ec397-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="ec397-123">**SKU**</span></span> |<span data-ttu-id="ec397-124">Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**grootten.</span><span class="sxs-lookup"><span data-stu-id="ec397-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="ec397-125">Dankzij de introductie van de Hallo van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**.</span><span class="sxs-lookup"><span data-stu-id="ec397-125">With hello introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="ec397-126">WAF wordt niet ondersteund op kleine Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="ec397-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="ec397-127">**Modus**</span><span class="sxs-lookup"><span data-stu-id="ec397-127">**Mode**</span></span> | <span data-ttu-id="ec397-128">Deze instelling is Hallo-modus van WAF.</span><span class="sxs-lookup"><span data-stu-id="ec397-128">This setting is hello mode of WAF.</span></span> <span data-ttu-id="ec397-129">toegestane waarden zijn **detectie** en **preventie**.</span><span class="sxs-lookup"><span data-stu-id="ec397-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="ec397-130">Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="ec397-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="ec397-131">Gebeurtenissen worden nog wel geregistreerd in '-modus, maar Hallo aanvaller een 403 onbevoegde reactie van de toepassingsgateway Hallo krijgt.</span><span class="sxs-lookup"><span data-stu-id="ec397-131">In prevention mode, events are still logged but hello attacker receives a 403 unauthorized response from hello application gateway.</span></span>|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a><span data-ttu-id="ec397-132">Web application firewall tooan bestaande toepassingsgateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="ec397-132">Add web application firewall tooan existing application gateway</span></span>

<span data-ttu-id="ec397-133">Hallo volgt wijzigingen van de scriptopdracht een bestaande standaard application gateway tooa WAF ingeschakelde application gateway.</span><span class="sxs-lookup"><span data-stu-id="ec397-133">hello follow command changes an existing standard application gateway tooa WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="ec397-134">Met deze opdracht werkt Hallo toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="ec397-134">This command updates hello application gateway with web application firewall.</span></span> <span data-ttu-id="ec397-135">Ga naar [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand hoe tooview voor uw toepassingsgateway registreert.</span><span class="sxs-lookup"><span data-stu-id="ec397-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand how tooview logs for your application gateway.</span></span> <span data-ttu-id="ec397-136">Vervaldatum toohello aard van de beveiliging van WAF beoordeeld logboeken moeten toobe regelmatig toounderstand Hallo-beveiligingsstatus van uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="ec397-136">Due toohello security nature of WAF, logs need toobe reviewed regularly toounderstand hello security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="ec397-137">Een toepassingsgateway maken met web application firewall</span><span class="sxs-lookup"><span data-stu-id="ec397-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="ec397-138">Hallo volgende opdracht maakt een toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="ec397-138">hello following command creates an Application Gateway with web application firewall.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> <span data-ttu-id="ec397-139">Toepassingsgateways gemaakt met de Hallo basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="ec397-139">Application gateways created with hello basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="ec397-140">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="ec397-140">Get application gateway DNS name</span></span>

<span data-ttu-id="ec397-141">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="ec397-141">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="ec397-142">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="ec397-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="ec397-143">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec397-143">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="ec397-144">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ec397-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="ec397-145">tooconfigure een CNAME-record ophalen van gegevens van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="ec397-145">tooconfigure a CNAME record, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="ec397-146">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="ec397-146">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="ec397-147">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ec397-147">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="next-steps"></a><span data-ttu-id="ec397-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec397-148">Next steps</span></span>

<span data-ttu-id="ec397-149">Meer informatie over hoe toocustomize WAF in via regels: [web application firewall-regels via hello Azure CLI 2.0 aanpassen](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ec397-149">Learn how toocustomize WAF rules by visiting: [Customize web application firewall rules through hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
