---
title: aaaHosting meerdere sites op Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway-ondersteuning voor meerdere locaties.
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
ms.openlocfilehash: 4ab6faa97f1891d7525affdaa36463681bf99e9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-multiple-site-hosting"></a><span data-ttu-id="a74dd-103">Meerdere sites in Application Gateway hosten</span><span class="sxs-lookup"><span data-stu-id="a74dd-103">Application Gateway multiple site hosting</span></span>

<span data-ttu-id="a74dd-104">Kunt u meerdere hosting-site tooconfigure meer dan één webtoepassing op Hallo hetzelfde exemplaar van de gateway.</span><span class="sxs-lookup"><span data-stu-id="a74dd-104">Multiple site hosting enables you tooconfigure more than one web application on hello same application gateway instance.</span></span> <span data-ttu-id="a74dd-105">Deze functie kunt u een efficiëntere topologie voor uw implementaties tooconfigure door too20 websites tooone toepassingsgateway toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="a74dd-105">This feature allows you tooconfigure a more efficient topology for your deployments by adding up too20 websites tooone application gateway.</span></span> <span data-ttu-id="a74dd-106">Elke website kan worden omgeleid tooits eigenaar van de back-endpool.</span><span class="sxs-lookup"><span data-stu-id="a74dd-106">Each website can be directed tooits own backend pool.</span></span> <span data-ttu-id="a74dd-107">In de Hallo voorbeeld te volgen, bedient toepassingsgateway verkeer voor contoso.com en fabrikam.com van twee back-end servergroepen ContosoServerPool en FabrikamServerPool genoemd.</span><span class="sxs-lookup"><span data-stu-id="a74dd-107">In hello following example, application gateway is serving traffic for contoso.com and fabrikam.com from two back-end server pools called ContosoServerPool and FabrikamServerPool.</span></span>

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> <span data-ttu-id="a74dd-109">Regels worden verwerkt in Hallo volgorde waarin die ze worden weergegeven in de portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="a74dd-109">Rules are processed in hello order they are listed in hello portal.</span></span> <span data-ttu-id="a74dd-110">Het wordt sterk aanbevolen tooconfigure listeners multi-site eerste voorafgaande tooconfiguring een basic-listener.</span><span class="sxs-lookup"><span data-stu-id="a74dd-110">It is highly recommended tooconfigure multi-site listeners first prior tooconfiguring a basic listener.</span></span>  <span data-ttu-id="a74dd-111">Dit zorgt ervoor dat verkeer opgehaald terugkeren gerouteerde toohello eindigen.</span><span class="sxs-lookup"><span data-stu-id="a74dd-111">This will ensure that traffic gets routed toohello right back end.</span></span> <span data-ttu-id="a74dd-112">Als een basislistener als eerste wordt weergegeven en overeenkomt met een inkomende aanvraag, wordt deze door die listener verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a74dd-112">If a basic listener is listed first and matches an incoming request, it gets processed by that listener.</span></span>

<span data-ttu-id="a74dd-113">Aanvragen voor http://contoso.com gerouteerde tooContosoServerPool en http://fabrikam.com gerouteerde tooFabrikamServerPool zijn.</span><span class="sxs-lookup"><span data-stu-id="a74dd-113">Requests for http://contoso.com are routed tooContosoServerPool, and http://fabrikam.com are routed tooFabrikamServerPool.</span></span>

<span data-ttu-id="a74dd-114">Op dezelfde manier Hallo twee subdomeinen Hallo dezelfde bovenliggende domein kan worden gehost op dezelfde gateway toepassingsimplementatie.</span><span class="sxs-lookup"><span data-stu-id="a74dd-114">Similarly two subdomains of hello same parent domain can be hosted on hello same application gateway deployment.</span></span> <span data-ttu-id="a74dd-115">Voorbeelden van subdomeinen die worden gehost op één toepassingsgateway-implementatie, zijn http://blog.contoso.com en http://app.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a74dd-115">Examples of using subdomains could include http://blog.contoso.com and http://app.contoso.com hosted on a single application gateway deployment.</span></span>

## <a name="host-headers-and-server-name-indication-sni"></a><span data-ttu-id="a74dd-116">Hostheaders en Servernaamindicatie (SNI)</span><span class="sxs-lookup"><span data-stu-id="a74dd-116">Host headers and Server Name Indication (SNI)</span></span>

<span data-ttu-id="a74dd-117">Er zijn drie algemene methoden voor het inschakelen van meerdere site hosten op Hallo van dezelfde infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="a74dd-117">There are three common mechanisms for enabling multiple site hosting on hello same infrastructure.</span></span>

1. <span data-ttu-id="a74dd-118">Het is mogelijk meerdere webtoepassingen te hosten, elk op een uniek IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a74dd-118">Host multiple web applications each on a unique IP address.</span></span>
2. <span data-ttu-id="a74dd-119">Gebruik hostnaam toohost meerdere webtoepassingen op Hallo hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a74dd-119">Use host name toohost multiple web applications on hello same IP address.</span></span>
3. <span data-ttu-id="a74dd-120">Gebruik verschillende poorten toohost meerdere webtoepassingen op Hallo hetzelfde IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a74dd-120">Use different ports toohost multiple web applications on hello same IP address.</span></span>

<span data-ttu-id="a74dd-121">Op dit ogenblik krijgt een toepassingsgateway één openbaar IP-adres waarop deze luistert naar verkeer.</span><span class="sxs-lookup"><span data-stu-id="a74dd-121">Currently an application gateway gets a single public IP address on which it listens for traffic.</span></span> <span data-ttu-id="a74dd-122">Daarom wordt de ondersteuning van meerdere toepassingen, elk met een eigen IP-adres, momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a74dd-122">Therefore supporting multiple applications, each with its own IP address, is currently not supported.</span></span> <span data-ttu-id="a74dd-123">Toepassingsgateway ondersteunt die als host fungeert voor meerdere toepassingen elke luistert op verschillende poorten, maar in dit scenario zou moeten Hallo toepassingen tooaccept verkeer op niet-standaardpoorten en is vaak niet een gewenste configuratie.</span><span class="sxs-lookup"><span data-stu-id="a74dd-123">Application Gateway supports hosting multiple applications each listening on different ports but this scenario would require hello applications tooaccept traffic on non-standard ports and is often not a desired configuration.</span></span> <span data-ttu-id="a74dd-124">Application Gateway is afhankelijk van HTTP 1.1 host headers toohost meer dan één website op Hallo hetzelfde openbare IP-adres en poort.</span><span class="sxs-lookup"><span data-stu-id="a74dd-124">Application Gateway relies on HTTP 1.1 host headers toohost more than one website on hello same public IP address and port.</span></span> <span data-ttu-id="a74dd-125">Hallo sites die worden gehost in toepassingsgateway kunnen ook ondersteuning voor SSL-offload met de Server de naam van vermelding (SNI) TLS-extensie.</span><span class="sxs-lookup"><span data-stu-id="a74dd-125">hello sites hosted on application gateway can also support SSL offload with Server Name Indication (SNI) TLS extension.</span></span> <span data-ttu-id="a74dd-126">Dit scenario betekent dat Hallo client browser en back-end-webfarm HTTP/1.1 en TLS-extensie, zoals gedefinieerd in RFC 6066 moet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="a74dd-126">This scenario means that hello client browser and backend web farm must support HTTP/1.1 and TLS extension as defined in RFC 6066.</span></span>

## <a name="listener-configuration-element"></a><span data-ttu-id="a74dd-127">Configuratie-element Listener</span><span class="sxs-lookup"><span data-stu-id="a74dd-127">Listener configuration element</span></span>

<span data-ttu-id="a74dd-128">Bestaande HTTPListener configuratie-element is verbeterd toosupport host en de server de naam van vermelding elementen, die wordt gebruikt door de gateway tooroute verkeer tooappropriate back-end van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a74dd-128">Existing HTTPListener configuration element is enhanced toosupport host name and server name indication elements, which is used by application gateway tooroute traffic tooappropriate backend pool.</span></span> <span data-ttu-id="a74dd-129">Hallo is volgende codevoorbeeld Hallo codefragment HttpListeners-element van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a74dd-129">hello following code example is hello snippet of HttpListeners element from template file.</span></span>

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

<span data-ttu-id="a74dd-130">U kunt ook bezoeken [Resource Manager-sjabloon met gebruik van meerdere hosting-site](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) voor een implementatie end tooend op basis van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a74dd-130">You can visit [Resource Manager template using multiple site hosting](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) for an end tooend template-based deployment.</span></span>

## <a name="routing-rule"></a><span data-ttu-id="a74dd-131">Routeringsregel</span><span class="sxs-lookup"><span data-stu-id="a74dd-131">Routing rule</span></span>

<span data-ttu-id="a74dd-132">Er is geen wijziging in de regel voor het doorsturen van Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="a74dd-132">There is no change required in hello routing rule.</span></span> <span data-ttu-id="a74dd-133">Hallo routeringsregel 'Basic' moet blijven toobe gekozen tootie Hallo geschikte site listener toohello overeenkomende back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="a74dd-133">hello routing rule 'Basic' should continue toobe chosen tootie hello appropriate site listener toohello corresponding backend address pool.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a74dd-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a74dd-134">Next steps</span></span>

<span data-ttu-id="a74dd-135">Nadat u hebt leren over het hosten van meerdere site gaat te[een toepassingsgateway met meerdere hosting-site maken](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate een toepassingsgateway met mogelijkheid toosupport meer dan één webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="a74dd-135">After learning about multiple site hosting, go too[create an application gateway using multiple site hosting](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate an application gateway with ability toosupport more than one web application.</span></span>

