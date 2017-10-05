---
title: Overzicht routering van op URL gebaseerde inhoud | Microsoft Docs
description: Deze pagina biedt een overzicht van de routering van op URL gebaseerde inhoud van de toepassingsgateway, de UrlPathMap-configuratie en de PathBasedRouting-regel.
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
ms.openlocfilehash: 75c3279d2d02cb3c6e949d191c88a1eb18b58a27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="url-path-based-routing-overview"></a><span data-ttu-id="e4cc1-103">Overzicht van op URL-pad gebaseerde routering</span><span class="sxs-lookup"><span data-stu-id="e4cc1-103">URL Path Based Routing overview</span></span>

<span data-ttu-id="e4cc1-104">Met op URL-pad gebaseerde routering kunt u verkeer routeren naar back-endserverpools die zijn gebaseerd op de URL-paden van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-104">URL Path Based Routing allows you to route traffic to back-end server pools based on URL Paths of the request.</span></span> 

<span data-ttu-id="e4cc1-105">Een van de scenario's is het routeren van aanvragen voor verschillende inhoudstypen naar verschillende back-endserverpools.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-105">One of the scenarios is to route requests for different content types to different backend server pools.</span></span>

<span data-ttu-id="e4cc1-106">In het volgende voorbeeld verzorgt de toepassingsgateway het verkeer voor contoso.com van drie back-endserverpools: VideoServerPool, ImageServerPool en DefaultServerPool.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-106">In the following example, Application Gateway is serving traffic for contoso.com from three back-end server pools for example: VideoServerPool, ImageServerPool, and DefaultServerPool.</span></span>

![imageURLroute](./media/application-gateway-url-route-overview/figure1.png)

<span data-ttu-id="e4cc1-108">Aanvragen voor http://contoso.com/video* worden gerouteerd naar VideoServerPool en http://contoso.com/images* naar ImageServerPool.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-108">Requests for http://contoso.com/video* are routed to VideoServerPool, and http://contoso.com/images* are routed to ImageServerPool.</span></span> <span data-ttu-id="e4cc1-109">Als geen van de padpatronen overeenkomen, wordt DefaultServerPool geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-109">DefaultServerPool is selected if none of the path patterns match.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4cc1-110">Regels worden verwerkt in de volgorde die wordt weergegeven in de portal.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-110">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="e4cc1-111">Het is raadzaam om eerst listeners voor meerdere locaties te configureren voordat u een basislistener configureert.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-111">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="e4cc1-112">Dit zorgt ervoor dat verkeer naar de juiste back-end wordt geleid.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-112">This ensures that traffic gets routed to the right back end.</span></span> <span data-ttu-id="e4cc1-113">Als een basislistener als eerste wordt weergegeven en overeenkomt met een inkomende aanvraag, wordt deze door die listener verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-113">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

## <a name="urlpathmap-configuration-element"></a><span data-ttu-id="e4cc1-114">Configuratie-element UrlPathMap</span><span class="sxs-lookup"><span data-stu-id="e4cc1-114">UrlPathMap configuration element</span></span>

<span data-ttu-id="e4cc1-115">Het element UrlPathMap wordt gebruikt om padpatronen op te geven voor back-endservergroepstoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-115">The urlPathMap element is used to specify Path patterns to back-end server pool mappings.</span></span> <span data-ttu-id="e4cc1-116">Het volgende codevoorbeeld is het fragment van het urlPathMap-element van het sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-116">The following code example is the snippet of urlPathMap element from template file.</span></span>

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
> <span data-ttu-id="e4cc1-117">PathPattern: deze instelling is een lijst van padpatronen voor aanpassing.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-117">PathPattern: This setting is a list of path patterns to match.</span></span> <span data-ttu-id="e4cc1-118">Elk hiervan moet beginnen met / en de enige plaats waar een * is toegestaan, is aan het einde na een /.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-118">Each must start with / and the only place a "*" is allowed is at the end following a "/."</span></span> <span data-ttu-id="e4cc1-119">De tekenreeks die is ingevoerd in de padvergelijking, bevat geen tekst na de eerste ? of # en die tekens zijn hier niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-119">The string fed to the path matcher does not include any text after the first? or #, and those chars are not allowed here.</span></span>

<span data-ttu-id="e4cc1-120">U kunt een [Resource Manager-sjabloon met op URL gebaseerde routering](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) bekijken voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-120">You can check out a [Resource Manager template using URL-based routing](https://azure.microsoft.com/documentation/templates/201-application-gateway-url-path-based-routing) for more information.</span></span>

## <a name="pathbasedrouting-rule"></a><span data-ttu-id="e4cc1-121">PathBasedRouting-regel</span><span class="sxs-lookup"><span data-stu-id="e4cc1-121">PathBasedRouting rule</span></span>

<span data-ttu-id="e4cc1-122">RequestRoutingRule van type PathBasedRouting wordt gebruikt voor het verbinden van een listener met een urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-122">RequestRoutingRule of type PathBasedRouting is used to bind a listener to a urlPathMap.</span></span> <span data-ttu-id="e4cc1-123">Alle aanvragen die zijn ontvangen voor deze listener, worden gerouteerd op basis van een beleid dat is opgegeven in urlPathMap.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-123">All requests that are received for this listener are routed based on policy specified in urlPathMap.</span></span>
<span data-ttu-id="e4cc1-124">Fragment van PathBasedRouting-regel:</span><span class="sxs-lookup"><span data-stu-id="e4cc1-124">Snippet of PathBasedRouting rule:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e4cc1-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4cc1-125">Next steps</span></span>

<span data-ttu-id="e4cc1-126">Nadat u meer hebt geleerd over routering van op URL gebaseerde inhoud, gaat u naar [Een toepassingsgateway maken met behulp van URL-gebaseerde routering](application-gateway-create-url-route-portal.md) om een toepassingsgateway te maken met URL-routeringsregels.</span><span class="sxs-lookup"><span data-stu-id="e4cc1-126">After learning about URL-based content routing, go to [create an application gateway using URL-based routing](application-gateway-create-url-route-portal.md) to create an application gateway with URL routing rules.</span></span>
