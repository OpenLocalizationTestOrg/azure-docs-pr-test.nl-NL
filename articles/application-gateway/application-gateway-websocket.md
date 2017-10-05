---
title: Ondersteuning voor WebSocket in Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van de toepassing Gateway WebSocket-ondersteuning.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 8968dac1-e9bc-4fa1-8415-96decacab83f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: amsriva
ms.openlocfilehash: 75b06ddd02da231b7813c609c848c75e42116da5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="e7d04-103">Overzicht van WebSocket-ondersteuning in Application Gateway</span><span class="sxs-lookup"><span data-stu-id="e7d04-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="e7d04-104">Toepassingsgateway biedt systeemeigen ondersteuning voor WebSocket over alle gateway-grootte.</span><span class="sxs-lookup"><span data-stu-id="e7d04-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="e7d04-105">Er is geen gebruiker configureerbare instelling selectief of WebSocket ondersteuning uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="e7d04-105">There is no user-configurable setting to selectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="e7d04-106">WebSocket-protocol in gestandaardiseerd [RFC6455](https://tools.ietf.org/html/rfc6455) een full-duplex communicatie tussen een server en een client via een langdurige TCP-verbinding worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e7d04-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="e7d04-107">Deze functie kunt u een nieuwe interactieve communicatie tussen de webserver en de client, die bidirectionele zonder de noodzaak voor polling als vereiste in implementaties op basis van HTTP worden kan.</span><span class="sxs-lookup"><span data-stu-id="e7d04-107">This feature allows for a more interactive communication between the web server and the client, which can be bidirectional without the need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="e7d04-108">WebSocket heeft weinig overhead in tegenstelling tot HTTP en dezelfde TCP-verbinding voor meerdere aanvragen/antwoorden, wat resulteert in een efficiënter gebruik van bronnen kan gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e7d04-108">WebSocket has low overhead unlike HTTP and can reuse the same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="e7d04-109">WebSocket-protocollen zijn ontworpen om te werken via traditionele HTTP-poorten 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="e7d04-109">WebSocket protocols are designed to work over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="e7d04-110">U kunt doorgaan met behulp van standaard HTTP-listener op poort 80 of 443 WebSocket-verkeer ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e7d04-110">You can continue using a standard HTTP listener on port 80 or 443 to receive WebSocket traffic.</span></span> <span data-ttu-id="e7d04-111">WebSocket-verkeer wordt vervolgens omgeleid naar de WebSocket-ingeschakelde back-endserver met de juiste back-endpool is opgegeven in de regels voor application gateway.</span><span class="sxs-lookup"><span data-stu-id="e7d04-111">WebSocket traffic is then directed to the WebSocket enabled backend server using the appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="e7d04-112">De back-endserver moet reageren op de application gateway tests die worden beschreven in de [health test overzicht](application-gateway-probe-overview.md) sectie.</span><span class="sxs-lookup"><span data-stu-id="e7d04-112">The backend server must respond to the application gateway probes, which are described in the [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="e7d04-113">Statuscontroles van Application gateway zijn alleen HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e7d04-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="e7d04-114">Elke back-endserver moet reageren op HTTP-tests voor de toepassingsgateway WebSocket om gegevensverkeer te routeren naar de server.</span><span class="sxs-lookup"><span data-stu-id="e7d04-114">Each backend server must respond to HTTP probes for application gateway to route WebSocket traffic to the server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="e7d04-115">Configuratie-element Listener</span><span class="sxs-lookup"><span data-stu-id="e7d04-115">Listener configuration element</span></span>

<span data-ttu-id="e7d04-116">Een bestaande HTTP-listener kan worden gebruikt ter ondersteuning van WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="e7d04-116">An existing HTTP listener can be used to support WebSocket traffic.</span></span> <span data-ttu-id="e7d04-117">Hier volgt een fragment van een element vanuit een voorbeeldbestand van de sjabloon een httpListeners.</span><span class="sxs-lookup"><span data-stu-id="e7d04-117">The following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="e7d04-118">U moet zowel HTTP als HTTPS-listeners ter ondersteuning van WebSocket en beveiliging van WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="e7d04-118">You would need both HTTP and HTTPS listeners to support WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="e7d04-119">Op dezelfde manier kunt u de [portal](application-gateway-create-gateway-portal.md) of [PowerShell](application-gateway-create-gateway-arm.md) een toepassingsgateway maken met listeners op poort 80/443 ter ondersteuning van WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="e7d04-119">Similarly you can use the [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) to create an application gateway with listeners on port 80/443 to support WebSocket traffic.</span></span>

```json
"httpListeners": [
        {
            "name": "appGatewayHttpsListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/DefaultFrontendPublicIP"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort443'"
                },
                "Protocol": "Https",
                "SslCertificate": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/sslCertificates/appGatewaySslCert1'"
                },
            }
        },
        {
            "name": "appGatewayHttpListener",
            "properties": {
                "FrontendIPConfiguration": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendIPConfigurations/appGatewayFrontendIP'"
                },
                "FrontendPort": {
                    "Id": "/subscriptions/{subscriptionId/resourceGroups/{resourceGroupName/providers/Microsoft.Network/applicationGateways/{applicationGatewayName/frontendPorts/appGatewayFrontendPort80'"
                },
                "Protocol": "Http",
            }
        }
    ],
```

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="e7d04-120">Regelconfiguratie BackendAddressPool BackendHttpSetting en routering</span><span class="sxs-lookup"><span data-stu-id="e7d04-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="e7d04-121">Een BackendAddressPool wordt gebruikt voor het definiëren van een back-endpool met servers van WebSocket is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e7d04-121">A BackendAddressPool is used to define a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="e7d04-122">De backendHttpSetting wordt gedefinieerd met een back endpoort 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="e7d04-122">The backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="e7d04-123">De eigenschappen voor cookies gebaseerde affiniteit en requestTimeouts zijn niet relevant zijn voor WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="e7d04-123">The properties for cookie-based affinity and requestTimeouts are not relevant to WebSocket traffic.</span></span> <span data-ttu-id="e7d04-124">Er is geen wijziging vereist in de regel voor het doorsturen, 'Basic' wordt gebruikt voor het koppelen van de juiste listener aan de bijbehorende back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="e7d04-124">There is no change required in the routing rule, 'Basic' is used to tie the appropriate listener to the corresponding backend address pool.</span></span> 

```json
"requestRoutingRules": [{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpsListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}, {
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/httpListeners/appGatewayHttpListener')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/applicationGateways/{applicationGatewayName}/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }

    }
}]
```

## <a name="websocket-enabled-backend"></a><span data-ttu-id="e7d04-125">Back-end van WebSocket is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="e7d04-125">WebSocket enabled backend</span></span>

<span data-ttu-id="e7d04-126">Uw back-end moet een HTTP/HTTPS-webserver uitgevoerd op de geconfigureerde poort (meestal 80/443) voor WebSocket om te werken.</span><span class="sxs-lookup"><span data-stu-id="e7d04-126">Your backend must have a HTTP/HTTPS web server running on the configured port (usually 80/443) for WebSocket to work.</span></span> <span data-ttu-id="e7d04-127">Deze vereiste is omdat de initiële handshake moet HTTP met een upgrade uit naar de WebSocket-protocol als een headerveld WebSocket-protocol is vereist.</span><span class="sxs-lookup"><span data-stu-id="e7d04-127">This requirement is because WebSocket protocol requires the initial handshake to be HTTP with upgrade to WebSocket protocol as a header field.</span></span> <span data-ttu-id="e7d04-128">Hier volgt een voorbeeld van een koptekst:</span><span class="sxs-lookup"><span data-stu-id="e7d04-128">The following is an example of a header:</span></span>

```
    GET /chat HTTP/1.1
    Host: server.example.com
    Upgrade: websocket
    Connection: Upgrade
    Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
    Origin: http://example.com
    Sec-WebSocket-Protocol: chat, superchat
    Sec-WebSocket-Version: 13
```

<span data-ttu-id="e7d04-129">Een andere reden hiervoor is dat back-end de statuscontrole van application gateway biedt ondersteuning voor HTTP en HTTPS-protocollen.</span><span class="sxs-lookup"><span data-stu-id="e7d04-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="e7d04-130">Als de back-endserver niet op HTTP of HTTPS tests reageert, is deze buiten het back-endpool nodig.</span><span class="sxs-lookup"><span data-stu-id="e7d04-130">If the backend server does not respond to HTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7d04-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e7d04-131">Next steps</span></span>

<span data-ttu-id="e7d04-132">Na het leren over de WebSocket-ondersteuning gaat u naar [een toepassingsgateway maken](application-gateway-create-gateway.md) ingeschakeld om te beginnen met een WebSocket-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="e7d04-132">After learning about WebSocket support, go to [create an application gateway](application-gateway-create-gateway.md) to get started with a WebSocket enabled web application.</span></span>

