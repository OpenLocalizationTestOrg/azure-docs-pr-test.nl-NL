---
title: ondersteuning voor aaaWebSocket in Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway WebSocket-ondersteuning.
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
ms.openlocfilehash: 3776117803e8559ad243c2d4c3dd661199c1e48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-websocket-support-in-application-gateway"></a><span data-ttu-id="5f03c-103">Overzicht van WebSocket-ondersteuning in Application Gateway</span><span class="sxs-lookup"><span data-stu-id="5f03c-103">Overview of WebSocket support in Application Gateway</span></span>

<span data-ttu-id="5f03c-104">Toepassingsgateway biedt systeemeigen ondersteuning voor WebSocket over alle gateway-grootte.</span><span class="sxs-lookup"><span data-stu-id="5f03c-104">Application Gateway provides native support for WebSocket across all gateway sizes.</span></span> <span data-ttu-id="5f03c-105">Er is geen gebruiker configureerbare instelling tooselectively inschakelen of uitschakelen WebSocket-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="5f03c-105">There is no user-configurable setting tooselectively enable or disable WebSocket support.</span></span> 

<span data-ttu-id="5f03c-106">WebSocket-protocol in gestandaardiseerd [RFC6455](https://tools.ietf.org/html/rfc6455) een full-duplex communicatie tussen een server en een client via een langdurige TCP-verbinding worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5f03c-106">WebSocket protocol standardized in [RFC6455](https://tools.ietf.org/html/rfc6455) enables a full duplex communication between a server and a client over a long running TCP connection.</span></span> <span data-ttu-id="5f03c-107">Deze functie kunt u een nieuwe interactieve communicatie tussen webserver Hallo en Hallo-client, die bidirectionele zonder Hallo nodig voor polling als vereiste in implementaties op basis van HTTP worden kan.</span><span class="sxs-lookup"><span data-stu-id="5f03c-107">This feature allows for a more interactive communication between hello web server and hello client, which can be bidirectional without hello need for polling as required in HTTP-based implementations.</span></span> <span data-ttu-id="5f03c-108">WebSocket heeft weinig overhead in tegenstelling tot HTTP en hergebruik kunt Hallo dezelfde TCP-verbinding voor meerdere aanvragen/antwoorden, wat resulteert in een efficiënter gebruik van bronnen.</span><span class="sxs-lookup"><span data-stu-id="5f03c-108">WebSocket has low overhead unlike HTTP and can reuse hello same TCP connection for multiple request/responses resulting in a more efficient utilization of resources.</span></span> <span data-ttu-id="5f03c-109">WebSocket-protocollen zijn ontworpen toowork via traditionele HTTP-poorten 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="5f03c-109">WebSocket protocols are designed toowork over traditional HTTP ports of 80 and 443.</span></span>

<span data-ttu-id="5f03c-110">U kunt doorgaan met behulp van standaard HTTP-listener op poort 80 of 443 tooreceive WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="5f03c-110">You can continue using a standard HTTP listener on port 80 or 443 tooreceive WebSocket traffic.</span></span> <span data-ttu-id="5f03c-111">WebSocket-verkeer wordt gerichte toohello WebSocket back-endserver Hallo juiste back-endpool zoals opgegeven in de regels voor application gateway is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5f03c-111">WebSocket traffic is then directed toohello WebSocket enabled backend server using hello appropriate backend pool as specified in application gateway rules.</span></span> <span data-ttu-id="5f03c-112">Hallo back-endserver moet reageren toohello application gateway tests die worden beschreven in Hallo [health test overzicht](application-gateway-probe-overview.md) sectie.</span><span class="sxs-lookup"><span data-stu-id="5f03c-112">hello backend server must respond toohello application gateway probes, which are described in hello [health probe overview](application-gateway-probe-overview.md) section.</span></span> <span data-ttu-id="5f03c-113">Statuscontroles van Application gateway zijn alleen HTTP/HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5f03c-113">Application gateway health probes are HTTP/HTTPS only.</span></span> <span data-ttu-id="5f03c-114">Elke back-endserver moet tooHTTP tests voor application gateway tooroute WebSocket verkeer toohello server reageren.</span><span class="sxs-lookup"><span data-stu-id="5f03c-114">Each backend server must respond tooHTTP probes for application gateway tooroute WebSocket traffic toohello server.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="5f03c-115">Configuratie-element Listener</span><span class="sxs-lookup"><span data-stu-id="5f03c-115">Listener configuration element</span></span>

<span data-ttu-id="5f03c-116">Een bestaande HTTP-listener kan worden gebruikt toosupport WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="5f03c-116">An existing HTTP listener can be used toosupport WebSocket traffic.</span></span> <span data-ttu-id="5f03c-117">Hallo hieronder is een fragment van een element vanuit een voorbeeldbestand van de sjabloon een httpListeners.</span><span class="sxs-lookup"><span data-stu-id="5f03c-117">hello following is a snippet of an httpListeners element from a sample template file.</span></span> <span data-ttu-id="5f03c-118">U moet zowel HTTP als HTTPS-listeners toosupport WebSocket en beveiliging van WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="5f03c-118">You would need both HTTP and HTTPS listeners toosupport WebSocket and secure WebSocket traffic.</span></span> <span data-ttu-id="5f03c-119">Op dezelfde manier kunt u Hallo [portal](application-gateway-create-gateway-portal.md) of [PowerShell](application-gateway-create-gateway-arm.md) toocreate een toepassingsgateway met listeners op poort 80/443 toosupport WebSocket-verkeer.</span><span class="sxs-lookup"><span data-stu-id="5f03c-119">Similarly you can use hello [portal](application-gateway-create-gateway-portal.md) or [PowerShell](application-gateway-create-gateway-arm.md) toocreate an application gateway with listeners on port 80/443 toosupport WebSocket traffic.</span></span>

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a><span data-ttu-id="5f03c-120">Regelconfiguratie BackendAddressPool BackendHttpSetting en routering</span><span class="sxs-lookup"><span data-stu-id="5f03c-120">BackendAddressPool, BackendHttpSetting, and Routing rule configuration</span></span>

<span data-ttu-id="5f03c-121">Een BackendAddressPool is gebruikte toodefine een back-endpool met servers van WebSocket is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5f03c-121">A BackendAddressPool is used toodefine a backend pool with WebSocket enabled servers.</span></span> <span data-ttu-id="5f03c-122">Hallo backendHttpSetting wordt gedefinieerd met een back endpoort 80 en 443.</span><span class="sxs-lookup"><span data-stu-id="5f03c-122">hello backendHttpSetting is defined with a backend port 80 and 443.</span></span> <span data-ttu-id="5f03c-123">Hallo-eigenschappen voor cookies gebaseerde affiniteit en requestTimeouts zijn niet relevant tooWebSocket verkeer.</span><span class="sxs-lookup"><span data-stu-id="5f03c-123">hello properties for cookie-based affinity and requestTimeouts are not relevant tooWebSocket traffic.</span></span> <span data-ttu-id="5f03c-124">Er is geen wijziging vereist in de regel voor het doorsturen van hello, 'Basic' gebruikte tootie Hallo juiste listener toohello back-endadresgroep overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="5f03c-124">There is no change required in hello routing rule, 'Basic' is used tootie hello appropriate listener toohello corresponding backend address pool.</span></span> 

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

## <a name="websocket-enabled-backend"></a><span data-ttu-id="5f03c-125">Back-end van WebSocket is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="5f03c-125">WebSocket enabled backend</span></span>

<span data-ttu-id="5f03c-126">Uw back-end moet een HTTP/HTTPS-webserver uitgevoerd op Hallo geconfigureerd hebben poort (meestal 80/443) voor WebSocket toowork.</span><span class="sxs-lookup"><span data-stu-id="5f03c-126">Your backend must have a HTTP/HTTPS web server running on hello configured port (usually 80/443) for WebSocket toowork.</span></span> <span data-ttu-id="5f03c-127">Deze vereiste is omdat WebSocket-protocol Hallo initiële handshake toobe HTTP met upgrade tooWebSocket-protocol als een headerveld is vereist.</span><span class="sxs-lookup"><span data-stu-id="5f03c-127">This requirement is because WebSocket protocol requires hello initial handshake toobe HTTP with upgrade tooWebSocket protocol as a header field.</span></span> <span data-ttu-id="5f03c-128">Hallo Hieronder volgt een voorbeeld van een koptekst:</span><span class="sxs-lookup"><span data-stu-id="5f03c-128">hello following is an example of a header:</span></span>

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

<span data-ttu-id="5f03c-129">Een andere reden hiervoor is dat back-end de statuscontrole van application gateway biedt ondersteuning voor HTTP en HTTPS-protocollen.</span><span class="sxs-lookup"><span data-stu-id="5f03c-129">Another reason for this is that application gateway backend health probe supports HTTP and HTTPS protocols only.</span></span> <span data-ttu-id="5f03c-130">Als back-endserver Hallo tooHTTP of HTTPS-tests niet reageert, wordt het opgevat buiten het back-endpool.</span><span class="sxs-lookup"><span data-stu-id="5f03c-130">If hello backend server does not respond tooHTTP or HTTPS probes, it is taken out of backend pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f03c-131">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f03c-131">Next steps</span></span>

<span data-ttu-id="5f03c-132">Nadat u hebt leren over de WebSocket-ondersteuning gaat te[een toepassingsgateway maken](application-gateway-create-gateway.md) tooget gestart met een WebSocket-webtoepassing ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5f03c-132">After learning about WebSocket support, go too[create an application gateway](application-gateway-create-gateway.md) tooget started with a WebSocket enabled web application.</span></span>

