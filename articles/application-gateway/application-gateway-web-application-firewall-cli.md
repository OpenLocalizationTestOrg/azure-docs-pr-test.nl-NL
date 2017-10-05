---
title: Web application firewall - Azure Application Gateway configureren | Microsoft Docs
description: In dit artikel biedt richtlijnen voor het gebruik van web application firewall op een bestaande of nieuwe application gateway.
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
ms.openlocfilehash: ac6c629ceaf1a8036643f593ce3d7ef9ea096ef8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a><span data-ttu-id="39aba-103">Web application firewall configureren op een nieuwe of bestaande toepassingsgateway met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="39aba-103">Configure web application firewall on a new or existing Application Gateway with Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="39aba-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="39aba-104">Azure portal</span></span>](application-gateway-web-application-firewall-portal.md)
> * [<span data-ttu-id="39aba-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="39aba-105">PowerShell</span></span>](application-gateway-web-application-firewall-powershell.md)
> * [<span data-ttu-id="39aba-106">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="39aba-106">Azure CLI</span></span>](application-gateway-web-application-firewall-cli.md)

<span data-ttu-id="39aba-107">Informatie over het maken van een toepassingsgateway web application firewall is ingeschakeld of web application firewall toevoegen aan een bestaande toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="39aba-107">Learn how to create a web application firewall enabled application gateway or add web application firewall to an existing application gateway.</span></span>

<span data-ttu-id="39aba-108">De web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.</span><span class="sxs-lookup"><span data-stu-id="39aba-108">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="39aba-109">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="39aba-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="39aba-110">De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud).</span><span class="sxs-lookup"><span data-stu-id="39aba-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="39aba-111">Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere.</span><span class="sxs-lookup"><span data-stu-id="39aba-111">Application gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, secure sockets layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="39aba-112">Ga voor een volledige lijst met ondersteunde functies naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="39aba-112">To find a complete list of supported features, visit: [Overview of Application Gateway](application-gateway-introduction.md).</span></span>

<span data-ttu-id="39aba-113">Het volgende artikel toont hoe [web application firewall toevoegen aan een bestaande toepassingsgateway](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="39aba-113">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![afbeelding van scenario][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="39aba-115">Voorwaarde: Installeer de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="39aba-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="39aba-116">Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="39aba-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="waf-configuration-differences"></a><span data-ttu-id="39aba-117">WAF configuratie verschillen</span><span class="sxs-lookup"><span data-stu-id="39aba-117">WAF configuration differences</span></span>

<span data-ttu-id="39aba-118">Als u hebt gelezen [een toepassingsgateway maken met Azure CLI](application-gateway-create-gateway-cli.md), u inzicht in de SKU-instellingen bij het maken van een toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="39aba-118">If you have read [Create an Application Gateway with Azure CLI](application-gateway-create-gateway-cli.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="39aba-119">WAF biedt aanvullende instellingen op te geven bij het configureren van de SKU voor een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="39aba-119">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="39aba-120">Er zijn geen aanvullende wijzigingen die u in de toepassingsgateway zelf aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="39aba-120">There are no additional changes that you make on the application gateway itself.</span></span>

| <span data-ttu-id="39aba-121">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="39aba-121">**Setting**</span></span> | <span data-ttu-id="39aba-122">**Details**</span><span class="sxs-lookup"><span data-stu-id="39aba-122">**Details**</span></span>
|---|---|
|<span data-ttu-id="39aba-123">**SKU**</span><span class="sxs-lookup"><span data-stu-id="39aba-123">**SKU**</span></span> |<span data-ttu-id="39aba-124">Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**grootten.</span><span class="sxs-lookup"><span data-stu-id="39aba-124">A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="39aba-125">Dankzij de introductie van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**.</span><span class="sxs-lookup"><span data-stu-id="39aba-125">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="39aba-126">WAF wordt niet ondersteund op kleine Toepassingsgateways.</span><span class="sxs-lookup"><span data-stu-id="39aba-126">WAF is not supported on small application gateways.</span></span>|
|<span data-ttu-id="39aba-127">**Modus**</span><span class="sxs-lookup"><span data-stu-id="39aba-127">**Mode**</span></span> | <span data-ttu-id="39aba-128">Deze instelling wordt de modus van WAF.</span><span class="sxs-lookup"><span data-stu-id="39aba-128">This setting is the mode of WAF.</span></span> <span data-ttu-id="39aba-129">toegestane waarden zijn **detectie** en **preventie**.</span><span class="sxs-lookup"><span data-stu-id="39aba-129">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="39aba-130">Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="39aba-130">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="39aba-131">Gebeurtenissen worden nog wel geregistreerd in de modus te voorkomen, maar de aanvaller ontvangt een niet-geautoriseerde 403-antwoord van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="39aba-131">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="39aba-132">Web application firewall toevoegen aan een bestaande application gateway</span><span class="sxs-lookup"><span data-stu-id="39aba-132">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="39aba-133">De volgende opdracht verandert een bestaande standaard application gateway met een ingeschakelde toepassing WAF gateway.</span><span class="sxs-lookup"><span data-stu-id="39aba-133">The follow command changes an existing standard application gateway to a WAF enabled application gateway.</span></span>

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

<span data-ttu-id="39aba-134">Deze opdracht werkt u de toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="39aba-134">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="39aba-135">Ga naar [Application Gateway Diagnostics](application-gateway-diagnostics.md) om te begrijpen hoe de logboeken voor uw toepassingsgateway bekijken.</span><span class="sxs-lookup"><span data-stu-id="39aba-135">Visit [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="39aba-136">Vanwege de aard van de beveiliging van WAF moeten Logboeken regelmatig worden gecontroleerd om te begrijpen van de beveiligingsstatus van uw webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="39aba-136">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="39aba-137">Een toepassingsgateway maken met web application firewall</span><span class="sxs-lookup"><span data-stu-id="39aba-137">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="39aba-138">De volgende opdracht maakt een toepassingsgateway met web application firewall.</span><span class="sxs-lookup"><span data-stu-id="39aba-138">The following command creates an Application Gateway with web application firewall.</span></span>

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
> <span data-ttu-id="39aba-139">Toepassingsgateways gemaakt met de basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="39aba-139">Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="39aba-140">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="39aba-140">Get application gateway DNS name</span></span>

<span data-ttu-id="39aba-141">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="39aba-141">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="39aba-142">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="39aba-142">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="39aba-143">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="39aba-143">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="39aba-144">[Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39aba-144">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="39aba-145">Voor het configureren van een CNAME-record ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="39aba-145">To configure a CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="39aba-146">De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="39aba-146">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="39aba-147">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="39aba-147">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="39aba-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="39aba-148">Next steps</span></span>

<span data-ttu-id="39aba-149">Informatie over het aanpassen van WAF regels in via: [web application firewall-regels via de Azure CLI 2.0 aanpassen](application-gateway-customize-waf-rules-cli.md).</span><span class="sxs-lookup"><span data-stu-id="39aba-149">Learn how to customize WAF rules by visiting: [Customize web application firewall rules through the Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).</span></span>

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
