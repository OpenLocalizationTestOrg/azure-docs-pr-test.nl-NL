---
title: overzicht van routering voor inhoud op basis van aaaURL | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway URL gebaseerde inhoud routering, UrlPathMap-configuratie en PathBasedRouting regel.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.assetid: 4409159b-e22d-4c9a-a103-f5d32465d163
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: gwallace
ms.openlocfilehash: 5094b42625baffeb395beace68db0d269e46080c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="url-path-based-routing-overview"></a>Overzicht van op URL-pad gebaseerde routering

URL-pad op basis van routering, kunt u tooroute verkeer tooback-end servergroepen op basis van de URL-paden van Hallo-aanvraag. 

Een van de Hallo scenario's is tooroute aanvragen voor andere typen inhoud toodifferent back-end-servergroepen.

In de Hallo voorbeeld te volgen, Application Gateway fungeert verkeer voor contoso.com van drie back-endserver pools van bijvoorbeeld: VideoServerPool ImageServerPool en DefaultServerPool.

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

Aanvragen voor http://contoso.com/video * gerouteerde tooVideoServerPool en http://contoso.com/images * gerouteerde tooImageServerPool zijn. DefaultServerPool is geselecteerd als geen Hallo pad patronen overeenkomt met.

> [!IMPORTANT]
> Regels worden verwerkt in Hallo volgorde waarin die ze worden weergegeven in de portal Hallo. Het wordt sterk aanbevolen tooconfigure listeners multi-site eerste voorafgaande tooconfiguring een basic-listener.  Dit zorgt ervoor dat verkeer opgehaald terugkeren gerouteerde toohello eindigen. Als een basislistener als eerste wordt weergegeven en overeenkomt met een inkomende aanvraag, wordt deze door die listener verwerkt.

## <a name="urlpathmap-configuration-element"></a>Configuratie-element UrlPathMap

Hallo urlPathMap element heeft de gebruikte toospecify pad patronen tooback-end server groep toewijzingen. Hallo is volgende codevoorbeeld Hallo codefragment urlPathMap-element van de sjabloon.

```json
"urlPathMaps": [{
    "name": "{urlpathMapName}",
    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/urlPathMaps/{urlpathMapName}",
    "properties": {
        "defaultBackendAddressPool": {
            "id": "/subscriptions/    {subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName1}"
        },
        "defaultBackendHttpSettings": {
            "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpSettingsList/{settingname1}"
        },
        "pathRules": [{
            "name": "{pathRuleName}",
            "properties": {
                "paths": [
                    "{pathPattern}"
                ],
                "backendAddressPool": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendAddressPools/{poolName2}"
                },
                "backendHttpsettings": {
                    "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/backendHttpsettingsList/{settingName2}"
                }
            }
        }]
    }
}]
```

> [!NOTE]
> PathPattern: Deze instelling is een lijst met pad patronen toomatch. Elk moet beginnen met / en Hallo enige plaats waar een ' * ' is toegestaan op Hallo end volgt een '/'. Hallo-tekenreeks ingevoerd toohello pad matcher heeft geen tekst bevatten na Hallo eerst? of # en deze tekens worden hier niet toegestaan.

U kunt een [Resource Manager-sjabloon met op URL gebaseerde routering](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) bekijken voor meer informatie.

## <a name="pathbasedrouting-rule"></a>PathBasedRouting-regel

RequestRoutingRule van het type PathBasedRouting is gebruikte toobind een listener tooa urlPathMap. Alle aanvragen die zijn ontvangen voor deze listener, worden gerouteerd op basis van een beleid dat is opgegeven in urlPathMap.
Fragment van PathBasedRouting-regel:

```json
"requestRoutingRules": [
    {

"name": "{ruleName}",
"id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/requestRoutingRules/{ruleName}",
"properties": {
    "ruleType": "PathBasedRouting",
    "httpListener": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/httpListeners/<listenerName>"
    },
    "urlPathMap": {
        "id": "/subscriptions/{subscriptionId}/../microsoft.network/applicationGateways/{gatewayName}/ urlPathMaps/{urlpathMapName}"
    },

}
    }
]
```

## <a name="next-steps"></a>Volgende stappen

Nadat u hebt meer informatie over inhoud routering op basis van een URL, gaat te[maken van een toepassingsgateway met URL gebaseerde routering](application-gateway-create-url-route-portal.md) toocreate een toepassingsgateway met regels voor URL-routering.
