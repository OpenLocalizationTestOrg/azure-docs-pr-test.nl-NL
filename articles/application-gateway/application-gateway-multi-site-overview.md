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
# <a name="application-gateway-multiple-site-hosting"></a>Meerdere sites in Application Gateway hosten

Kunt u meerdere hosting-site tooconfigure meer dan één webtoepassing op Hallo hetzelfde exemplaar van de gateway. Deze functie kunt u een efficiëntere topologie voor uw implementaties tooconfigure door too20 websites tooone toepassingsgateway toe te voegen. Elke website kan worden omgeleid tooits eigenaar van de back-endpool. In de Hallo voorbeeld te volgen, bedient toepassingsgateway verkeer voor contoso.com en fabrikam.com van twee back-end servergroepen ContosoServerPool en FabrikamServerPool genoemd.

![imageURLroute](./media/application-gateway-multi-site-overview/multisite.png)

> [!IMPORTANT]
> Regels worden verwerkt in Hallo volgorde waarin die ze worden weergegeven in de portal Hallo. Het wordt sterk aanbevolen tooconfigure listeners multi-site eerste voorafgaande tooconfiguring een basic-listener.  Dit zorgt ervoor dat verkeer opgehaald terugkeren gerouteerde toohello eindigen. Als een basislistener als eerste wordt weergegeven en overeenkomt met een inkomende aanvraag, wordt deze door die listener verwerkt.

Aanvragen voor http://contoso.com gerouteerde tooContosoServerPool en http://fabrikam.com gerouteerde tooFabrikamServerPool zijn.

Op dezelfde manier Hallo twee subdomeinen Hallo dezelfde bovenliggende domein kan worden gehost op dezelfde gateway toepassingsimplementatie. Voorbeelden van subdomeinen die worden gehost op één toepassingsgateway-implementatie, zijn http://blog.contoso.com en http://app.contoso.com.

## <a name="host-headers-and-server-name-indication-sni"></a>Hostheaders en Servernaamindicatie (SNI)

Er zijn drie algemene methoden voor het inschakelen van meerdere site hosten op Hallo van dezelfde infrastructuur.

1. Het is mogelijk meerdere webtoepassingen te hosten, elk op een uniek IP-adres.
2. Gebruik hostnaam toohost meerdere webtoepassingen op Hallo hetzelfde IP-adres.
3. Gebruik verschillende poorten toohost meerdere webtoepassingen op Hallo hetzelfde IP-adres.

Op dit ogenblik krijgt een toepassingsgateway één openbaar IP-adres waarop deze luistert naar verkeer. Daarom wordt de ondersteuning van meerdere toepassingen, elk met een eigen IP-adres, momenteel niet ondersteund. Toepassingsgateway ondersteunt die als host fungeert voor meerdere toepassingen elke luistert op verschillende poorten, maar in dit scenario zou moeten Hallo toepassingen tooaccept verkeer op niet-standaardpoorten en is vaak niet een gewenste configuratie. Application Gateway is afhankelijk van HTTP 1.1 host headers toohost meer dan één website op Hallo hetzelfde openbare IP-adres en poort. Hallo sites die worden gehost in toepassingsgateway kunnen ook ondersteuning voor SSL-offload met de Server de naam van vermelding (SNI) TLS-extensie. Dit scenario betekent dat Hallo client browser en back-end-webfarm HTTP/1.1 en TLS-extensie, zoals gedefinieerd in RFC 6066 moet ondersteunen.

## <a name="listener-configuration-element"></a>Configuratie-element Listener

Bestaande HTTPListener configuratie-element is verbeterd toosupport host en de server de naam van vermelding elementen, die wordt gebruikt door de gateway tooroute verkeer tooappropriate back-end van toepassingen. Hallo is volgende codevoorbeeld Hallo codefragment HttpListeners-element van de sjabloon.

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

U kunt ook bezoeken [Resource Manager-sjabloon met gebruik van meerdere hosting-site](https://github.com/Azure/azure-quickstart-templates/blob/master/201-application-gateway-multihosting) voor een implementatie end tooend op basis van een sjabloon.

## <a name="routing-rule"></a>Routeringsregel

Er is geen wijziging in de regel voor het doorsturen van Hallo vereist. Hallo routeringsregel 'Basic' moet blijven toobe gekozen tootie Hallo geschikte site listener toohello overeenkomende back-end-adresgroep.

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

## <a name="next-steps"></a>Volgende stappen

Nadat u hebt leren over het hosten van meerdere site gaat te[een toepassingsgateway met meerdere hosting-site maken](application-gateway-create-multisite-azureresourcemanager-powershell.md) toocreate een toepassingsgateway met mogelijkheid toosupport meer dan één webtoepassing.

