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
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Web application firewall configureren op een nieuwe of bestaande toepassingsgateway met Azure CLI

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [Azure-CLI](application-gateway-web-application-firewall-cli.md)

Informatie over het maken van een toepassingsgateway web application firewall is ingeschakeld of web application firewall toevoegen aan een bestaande toepassingsgateway.

De web application firewall (WAF) in Azure Application Gateway beveiligt webtoepassingen van algemene web gebaseerde aanvallen, zoals SQL-injectie, cross-site scripting aanvallen en sessie hijacks.

Azure Application Gateway is een load balancer in laag 7. De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud). Toepassingsgateway biedt veel levering controller (ADC) toepassingsfuncties zoals HTTP taakverdeling, cookies gebaseerde affiniteit van de sessie laden, secure sockets layer (SSL)-offload, aangepaste statuscontroles, ondersteuning voor meerdere locaties en vele andere. Ga voor een volledige lijst met ondersteunde functies naar: [overzicht van toepassingsgateway](application-gateway-introduction.md).

Het volgende artikel toont hoe [web application firewall toevoegen aan een bestaande toepassingsgateway](#add-web-application-firewall-to-an-existing-application-gateway) en [maken van een toepassingsgateway die gebruikmaakt van web application firewall](#create-an-application-gateway-with-web-application-firewall).

![afbeelding van scenario][scenario]

## <a name="prerequisite-install-the-azure-cli-20"></a>Voorwaarde: Installeer de Azure CLI 2.0

Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>WAF configuratie verschillen

Als u hebt gelezen [een toepassingsgateway maken met Azure CLI](application-gateway-create-gateway-cli.md), u inzicht in de SKU-instellingen bij het maken van een toepassingsgateway configureren. WAF biedt aanvullende instellingen op te geven bij het configureren van de SKU voor een toepassingsgateway. Er zijn geen aanvullende wijzigingen die u in de toepassingsgateway zelf aanbrengt.

| **Instelling** | **Details**
|---|---|
|**SKU** |Een normale toepassingsgateway zonder WAF ondersteunt **standaard\_kleine**, **standaard\_gemiddeld**, en **standaard\_grote**grootten. Dankzij de introductie van WAF, er zijn twee extra SKU's **WAF\_gemiddeld** en **WAF\_grote**. WAF wordt niet ondersteund op kleine Toepassingsgateways.|
|**Modus** | Deze instelling wordt de modus van WAF. toegestane waarden zijn **detectie** en **preventie**. Wanneer WAF is ingesteld in de modus voor detectie, worden alle bedreigingen opgeslagen in een logboekbestand. Gebeurtenissen worden nog wel geregistreerd in de modus te voorkomen, maar de aanvaller ontvangt een niet-geautoriseerde 403-antwoord van de toepassingsgateway.|

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a>Web application firewall toevoegen aan een bestaande application gateway

De volgende opdracht verandert een bestaande standaard application gateway met een ingeschakelde toepassing WAF gateway.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Deze opdracht werkt u de toepassingsgateway met web application firewall. Ga naar [Application Gateway Diagnostics](application-gateway-diagnostics.md) om te begrijpen hoe de logboeken voor uw toepassingsgateway bekijken. Vanwege de aard van de beveiliging van WAF moeten Logboeken regelmatig worden gecontroleerd om te begrijpen van de beveiligingsstatus van uw webtoepassingen.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Een toepassingsgateway maken met web application firewall

De volgende opdracht maakt een toepassingsgateway met web application firewall.

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
> Toepassingsgateways gemaakt met de basic web application firewall-configuratie zijn geconfigureerd met CRS 3.0 voor beveiliging.

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). Voor het configureren van een CNAME-record ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway. De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst. Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.

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

## <a name="next-steps"></a>Volgende stappen

Informatie over het aanpassen van WAF regels in via: [web application firewall-regels via de Azure CLI 2.0 aanpassen](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
