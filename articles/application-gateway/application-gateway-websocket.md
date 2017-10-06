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
# <a name="overview-of-websocket-support-in-application-gateway"></a>Overzicht van WebSocket-ondersteuning in Application Gateway

Toepassingsgateway biedt systeemeigen ondersteuning voor WebSocket over alle gateway-grootte. Er is geen gebruiker configureerbare instelling tooselectively inschakelen of uitschakelen WebSocket-ondersteuning. 

WebSocket-protocol in gestandaardiseerd [RFC6455](https://tools.ietf.org/html/rfc6455) een full-duplex communicatie tussen een server en een client via een langdurige TCP-verbinding worden ingeschakeld. Deze functie kunt u een nieuwe interactieve communicatie tussen webserver Hallo en Hallo-client, die bidirectionele zonder Hallo nodig voor polling als vereiste in implementaties op basis van HTTP worden kan. WebSocket heeft weinig overhead in tegenstelling tot HTTP en hergebruik kunt Hallo dezelfde TCP-verbinding voor meerdere aanvragen/antwoorden, wat resulteert in een efficiënter gebruik van bronnen. WebSocket-protocollen zijn ontworpen toowork via traditionele HTTP-poorten 80 en 443.

U kunt doorgaan met behulp van standaard HTTP-listener op poort 80 of 443 tooreceive WebSocket-verkeer. WebSocket-verkeer wordt gerichte toohello WebSocket back-endserver Hallo juiste back-endpool zoals opgegeven in de regels voor application gateway is ingeschakeld. Hallo back-endserver moet reageren toohello application gateway tests die worden beschreven in Hallo [health test overzicht](application-gateway-probe-overview.md) sectie. Statuscontroles van Application gateway zijn alleen HTTP/HTTPS. Elke back-endserver moet tooHTTP tests voor application gateway tooroute WebSocket verkeer toohello server reageren.

## <a name="listener-configuration-element"></a>Configuratie-element Listener

Een bestaande HTTP-listener kan worden gebruikt toosupport WebSocket-verkeer. Hallo hieronder is een fragment van een element vanuit een voorbeeldbestand van de sjabloon een httpListeners. U moet zowel HTTP als HTTPS-listeners toosupport WebSocket en beveiliging van WebSocket-verkeer. Op dezelfde manier kunt u Hallo [portal](application-gateway-create-gateway-portal.md) of [PowerShell](application-gateway-create-gateway-arm.md) toocreate een toepassingsgateway met listeners op poort 80/443 toosupport WebSocket-verkeer.

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

## <a name="backendaddresspool-backendhttpsetting-and-routing-rule-configuration"></a>Regelconfiguratie BackendAddressPool BackendHttpSetting en routering

Een BackendAddressPool is gebruikte toodefine een back-endpool met servers van WebSocket is ingeschakeld. Hallo backendHttpSetting wordt gedefinieerd met een back endpoort 80 en 443. Hallo-eigenschappen voor cookies gebaseerde affiniteit en requestTimeouts zijn niet relevant tooWebSocket verkeer. Er is geen wijziging vereist in de regel voor het doorsturen van hello, 'Basic' gebruikte tootie Hallo juiste listener toohello back-endadresgroep overeenkomt. 

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

## <a name="websocket-enabled-backend"></a>Back-end van WebSocket is ingeschakeld

Uw back-end moet een HTTP/HTTPS-webserver uitgevoerd op Hallo geconfigureerd hebben poort (meestal 80/443) voor WebSocket toowork. Deze vereiste is omdat WebSocket-protocol Hallo initiële handshake toobe HTTP met upgrade tooWebSocket-protocol als een headerveld is vereist. Hallo Hieronder volgt een voorbeeld van een koptekst:

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

Een andere reden hiervoor is dat back-end de statuscontrole van application gateway biedt ondersteuning voor HTTP en HTTPS-protocollen. Als back-endserver Hallo tooHTTP of HTTPS-tests niet reageert, wordt het opgevat buiten het back-endpool.

## <a name="next-steps"></a>Volgende stappen

Nadat u hebt leren over de WebSocket-ondersteuning gaat te[een toepassingsgateway maken](application-gateway-create-gateway.md) tooget gestart met een WebSocket-webtoepassing ingeschakeld.

