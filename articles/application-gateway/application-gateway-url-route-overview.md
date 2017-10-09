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
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="faf28-103">Overzicht van op URL-pad gebaseerde routering</span><span class="sxs-lookup"><span data-stu-id="faf28-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="faf28-104">URL-pad op basis van routering, kunt u tooroute verkeer tooback-end servergroepen op basis van de URL-paden van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="faf28-104">URL Path Based Routing allows you tooroute traffic tooback-end server pools based on URL Paths of hello request.</span></span> 

<span data-ttu-id="faf28-105">Een van de Hallo scenario's is tooroute aanvragen voor andere typen inhoud toodifferent back-end-servergroepen.</span><span class="sxs-lookup"><span data-stu-id="faf28-105">One of hello scenarios is tooroute requests for different content types toodifferent backend server pools.</span></span>

<span data-ttu-id="faf28-106">In de Hallo voorbeeld te volgen, Application Gateway fungeert verkeer voor contoso.com van drie back-endserver pools van bijvoorbeeld: VideoServerPool ImageServerPool en DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="faf28-106">In hello following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="faf28-108">Aanvragen voor http://contoso.com/video * gerouteerde tooVideoServerPool en http://contoso.com/images * gerouteerde tooImageServerPool zijn.</span><span class="sxs-lookup"><span data-stu-id="faf28-108">Requests for http://contoso.com/video* are routed tooVideoServerPool, and http://contoso.com/images* are routed tooImageServerPool.</span></span> <span data-ttu-id="faf28-109">DefaultServerPool is geselecteerd als geen Hallo pad patronen overeenkomt met.</span><span class="sxs-lookup"><span data-stu-id="faf28-109">DefaultServerPool is selected if none of hello path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="faf28-110">Regels worden verwerkt in Hallo volgorde waarin die ze worden weergegeven in de portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="faf28-110">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="faf28-111">Het wordt sterk aanbevolen tooconfigure listeners multi-site eerste voorafgaande tooconfiguring een basic-listener.</span><span class="sxs-lookup"><span data-stu-id="faf28-111">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="faf28-112">Dit zorgt ervoor dat verkeer opgehaald terugkeren gerouteerde toohello eindigen.</span><span class="sxs-lookup"><span data-stu-id="faf28-112">This ensures that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="faf28-113">Als een basislistener als eerste wordt weergegeven en overeenkomt met een inkomende aanvraag, wordt deze door die listener verwerkt.</span><span class="sxs-lookup"><span data-stu-id="faf28-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="faf28-114">Configuratie-element UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="faf28-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="faf28-115">Hallo urlPathMap element heeft de gebruikte toospecify pad patronen tooback-end server groep toewijzingen.</span><span class="sxs-lookup"><span data-stu-id="faf28-115">hello urlPathMap element is used toospecify Path patterns tooback-end server pool mappings.</span></span> <span data-ttu-id="faf28-116">Hallo is volgende codevoorbeeld Hallo codefragment urlPathMap-element van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="faf28-116">hello following code example is hello snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="faf28-117">PathPattern: Deze instelling is een lijst met pad patronen toomatch.</span><span class="sxs-lookup"><span data-stu-id="faf28-117">PathPattern: This setting is a list of path patterns toomatch.</span></span> <span data-ttu-id="faf28-118">Elk moet beginnen met / en Hallo enige plaats waar een ' * ' is toegestaan op Hallo end volgt een '/'.</span><span class="sxs-lookup"><span data-stu-id="faf28-118">Each must start with / and hello only place a "*" is allowed is at hello end following a "/."</span></span> <span data-ttu-id="faf28-119">Hallo-tekenreeks ingevoerd toohello pad matcher heeft geen tekst bevatten na Hallo eerst? of # en deze tekens worden hier niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="faf28-119">hello string fed toohello path matcher does not include any text after hello first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="faf28-120">U kunt een [Resource Manager-sjabloon met op URL gebaseerde routering](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) bekijken voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="faf28-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="faf28-121">PathBasedRouting-regel</span><span class="sxs-lookup"><span data-stu-id="faf28-121">PathBasedRouting rule</span></span>

<span data-ttu-id="faf28-122">RequestRoutingRule van het type PathBasedRouting is gebruikte toobind een listener tooa urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="faf28-122">RequestRoutingRule of type PathBasedRouting is used toobind a listener tooa urlPathMap.</span></span> <span data-ttu-id="faf28-123">Alle aanvragen die zijn ontvangen voor deze listener, worden gerouteerd op basis van een beleid dat is opgegeven in urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="faf28-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="faf28-124">Fragment van PathBasedRouting-regel:</span><span class="sxs-lookup"><span data-stu-id="faf28-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="faf28-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="faf28-125">Next steps</span></span>

<span data-ttu-id="faf28-126">Nadat u hebt meer informatie over inhoud routering op basis van een URL, gaat te[maken van een toepassingsgateway met URL gebaseerde routering](application-gateway-create-url-route-portal.md) toocreate een toepassingsgateway met regels voor URL-routering.</span><span class="sxs-lookup"><span data-stu-id="faf28-126">After learning about URL-based content routing, go too[create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) toocreate an application gateway with URL routing rules.</span></span>
