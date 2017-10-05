---
title: Meerdere sites op Azure Application Gateway hosten| Microsoft Docs
description: Op deze pagina wordt de ondersteuning voor meerdere sites in Application Gateway beschreven.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: 
ms.assetid: 49993fd2-87e5-4a66-b386-8d22056a616d
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: 645f68d836babf11f32fc391e6dacc9430f0070c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="5968a-103">Meerdere sites in Application Gateway hosten</span><span class="sxs-lookup"><span data-stu-id="5968a-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="5968a-104">Door meerdere sites te hosten, kunt u meer dan één webtoepassing configureren op dezelfde instantie van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="5968a-104">Multiple site hosting enables you to configure more than one web application on the same application gateway instance.</span></span> <span data-ttu-id="5968a-105">Met deze functie kunt u een efficiëntere topologie voor uw implementaties configureren door maximaal 20 websites toe te voegen aan één toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="5968a-105">This feature allows you to configure a more efficient topology for your deployments by adding up to 20 websites to one application gateway.</span></span> <span data-ttu-id="5968a-106">Elke website kan worden omgeleid naar een eigen back-endpool.</span><span class="sxs-lookup"><span data-stu-id="5968a-106">Each website can be directed to its own backend pool.</span></span> <span data-ttu-id="5968a-107">In het volgende voorbeeld verzorgt de toepassingsgateway het verkeer voor contoso.com en fabrikam.com van twee back-endservepools, ContosoServerPool en FabrikamServerPool genaamd.</span><span class="sxs-lookup"><span data-stu-id="5968a-107">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="5968a-109">Regels worden verwerkt in de volgorde die wordt weergegeven in de portal.</span><span class="sxs-lookup"><span data-stu-id="5968a-109">Rules are processed in the order they are listed in the portal.</span></span> <span data-ttu-id="5968a-110">Het is raadzaam om eerst listeners voor meerdere locaties te configureren voordat u een basislistener configureert.</span><span class="sxs-lookup"><span data-stu-id="5968a-110">It is highly recommended to configure multi-site listeners first prior to configuring a basic listener.</span></span>  <span data-ttu-id="5968a-111">Dit zorgt ervoor dat verkeer naar de juiste back-end wordt geleid.</span><span class="sxs-lookup"><span data-stu-id="5968a-111">This will ensure that traffic gets routed to the right back end.</span></span> <span data-ttu-id="5968a-112">Als een basislistener als eerste wordt weergegeven en overeenkomt met een inkomende aanvraag, wordt deze door die listener verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5968a-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="5968a-113">Aanvragen voor http://contoso.com worden naar ContosoServerPool gerouteerd en aanvragen voor http://fabrikam.com naar FabrikamServerPool.</span><span class="sxs-lookup"><span data-stu-id="5968a-113">Requests for http://contoso.com are routed to ContosoServerPool, and http://fabrikam.com are routed to FabrikamServerPool.</span></span>

<span data-ttu-id="5968a-114">Op dezelfde manier kunnen twee subdomeinen van hetzelfde bovenliggende domein worden gehost op dezelfde gateway-implementatie.</span><span class="sxs-lookup"><span data-stu-id="5968a-114">Similarly two subdomains of the same parent domain can be hosted on the same application gateway deployment.</span></span> <span data-ttu-id="5968a-115">Voorbeelden van subdomeinen die worden gehost op één toepassingsgateway-implementatie, zijn http://blog.contoso.com en http://app.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="5968a-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="5968a-116">Hostheaders en Servernaamindicatie (SNI)</span><span class="sxs-lookup"><span data-stu-id="5968a-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="5968a-117">Er zijn drie algemene mechanismen om het hosten van meerdere sites in te schakelen op dezelfde infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="5968a-117">There are three common mechanisms for enabling multiple site hosting on the same infrastructure.</span></span>

1. <span data-ttu-id="5968a-118">Het is mogelijk meerdere webtoepassingen te hosten, elk op een uniek IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5968a-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="5968a-119">Gebruik de hostnaam voor het hosten van meerdere webtoepassingen op hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5968a-119">Use host name to host multiple web applications on the same IP address.</span></span>
3. <span data-ttu-id="5968a-120">Gebruik verschillende poorten voor het hosten van meerdere webtoepassingen op hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5968a-120">Use different ports to host multiple web applications on the same IP address.</span></span>

<span data-ttu-id="5968a-121">Op dit ogenblik krijgt een toepassingsgateway één openbaar IP-adres waarop deze luistert naar verkeer.</span><span class="sxs-lookup"><span data-stu-id="5968a-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="5968a-122">Daarom wordt de ondersteuning van meerdere toepassingen, elk met een eigen IP-adres, momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5968a-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="5968a-123">Application Gateway ondersteunt het hosten van meerdere toepassingen die elk luisteren op verschillende poorten. Dit scenario zou echter vereisen dat de toepassingen verkeer accepteren op niet-standaardpoorten en dat is vaak geen gewenste configuratie.</span><span class="sxs-lookup"><span data-stu-id="5968a-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require the applications to accept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="5968a-124">Application Gateway maakt gebruik van HTTP 1.1-hostheaders voor het hosten van meer dan één website op hetzelfde openbare IP-adres en dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="5968a-124">Application Gateway relies on HTTP 1.1 host headers to host more than one website on the same public IP address and port.</span></span> <span data-ttu-id="5968a-125">De sites die op de toepassingsgateway worden gehost, kunnen ook SSL-offload ondersteunen met de Servernaamindicatie (SNI) met TLS-extensie.</span><span class="sxs-lookup"><span data-stu-id="5968a-125">The sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="5968a-126">Dit scenario houdt in dat de clientbrowser en back-end-webfarm de HTTP/1.1- en TLS-extensie moeten ondersteunen zoals gedefinieerd in RFC 6066.</span><span class="sxs-lookup"><span data-stu-id="5968a-126">This scenario means that the client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="5968a-127">Configuratie-element Listener</span><span class="sxs-lookup"><span data-stu-id="5968a-127">Listener configuration element</span></span>

<span data-ttu-id="5968a-128">Configuratie-element HTTPListener is verbeterd voor het ondersteunen van indicatie-elementen van de hostnaam en servernaam die worden gebruikt door de toepassingsgateway om verkeer naar de back-endpool te routeren.</span><span class="sxs-lookup"><span data-stu-id="5968a-128">Existing HTTPListener configuration element is enhanced to support host name and server name indication elements, which is used by application gateway to route traffic to appropriate backend pool.</span></span> <span data-ttu-id="5968a-129">Het volgende codevoorbeeld is het fragment van het HttpListeners-element van het sjabloonbestand.</span><span class="sxs-lookup"><span data-stu-id="5968a-129">The following code example is the snippet of HttpListeners element from template file.</span></span>

```json
"httpListeners": [
    {
        "name": "appGatewayHttpsListener1",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/DefaultFrontendPublicIP"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort443'"
            },
            "Protocol": "Https",
            "SslCertificate": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/sslCertificates/appGatewaySslCert1'"
            },
            "HostName": "contoso.com",
            "RequireServerNameIndication": "true"
        }
    },
    {
        "name": "appGatewayHttpListener2",
        "properties": {
            "FrontendIPConfiguration": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendIPConfigurations/appGatewayFrontendIP'"
            },
            "FrontendPort": {
                "Id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/frontendPorts/appGatewayFrontendPort80'"
            },
            "Protocol": "Http",
            "HostName": "fabrikam.com",
            "RequireServerNameIndication": "false"
        }
    }
],
```

<span data-ttu-id="5968a-130">U kunt ook [Resource Manager-sjabloon met het hosten van meerdere sites](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) bezoeken voor een end-to-end implementatie op basis van sjablonen.</span><span class="sxs-lookup"><span data-stu-id="5968a-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end to end template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="5968a-131">Routeringsregel</span><span class="sxs-lookup"><span data-stu-id="5968a-131">Routing rule</span></span>

<span data-ttu-id="5968a-132">Er is geen wijziging vereist in de routeringsregel.</span><span class="sxs-lookup"><span data-stu-id="5968a-132">There is no change required in the routing rule.</span></span> <span data-ttu-id="5968a-133">De routeringsregel Basic moet nog steeds worden gekozen om de geschikte site-listener te binden aan de overeenkomende back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="5968a-133">The routing rule 'Basic' should continue to be chosen to tie the appropriate site listener to the corresponding backend address pool.</span></span>

```json
"requestRoutingRules": [
{
    "name": "<ruleName1>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpsListener1')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/ContosoServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

},
{
    "name": "<ruleName2>",
    "properties": {
        "RuleType": "Basic",
        "httpListener": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/httpListeners/appGatewayHttpListener2')]"
        },
        "backendAddressPool": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendAddressPools/FabrikamServerPool')]"
        },
        "backendHttpSettings": {
            "id": "/subscriptions/<subid>/resourceGroups/<rgName>/providers/Microsoft.Network/applicationGateways/applicationGateway1/backendHttpSettingsCollection/appGatewayBackendHttpSettings')]"
        }
    }

}
]
```

## <a name="next-steps"></a><span data-ttu-id="5968a-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5968a-134">Next steps</span></span>

<span data-ttu-id="5968a-135">Nadat u meer hebt geleerd over het hosten van meerdere sites, gaat u naar [Een toepassingsgateway maken met het hosten van meerdere sites](application-gateway-create-multisite-azureresourcemanager-powershell.md) om een toepassingsgateway te maken met de mogelijkheid om meer dan één webtoepassing te ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="5968a-135">After learning about multiple site hosting, go to [create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) to create an application gateway with ability to support more than one web application.</span></span>

