---
title: Maken van een Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs
description: Informatie over het maken van een toepassingsgateway met behulp van de Azure CLI 2.0 in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 052410db8c7619c7990dc319951a55663f2c2ba1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a>Een toepassingsgateway maken met behulp van de Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager-sjabloon](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

Application Gateway is een toegewezen virtueel apparaat waarmee de toepassing levering controller (ADC) als een service biedt verschillende laag 7 load balancing mogelijkheden voor uw toepassing.

## <a name="cli-versions-to-complete-the-task"></a>CLI-versies om de taak uit te voeren

U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel

## <a name="prerequisite-install-the-azure-cli-20"></a>Voorwaarde: Installeer de Azure CLI 2.0

Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Als u geen Azure-account hebt, moet u een. U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenario

In dit scenario wordt informatie over het maken van een toepassingsgateway met Azure portal.

Dit scenario wordt:

* Een middelgrote toepassingsgateway maken met twee exemplaren.
* Maak een virtueel netwerk met de naam AdatumAppGatewayVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.
* Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.

> [!NOTE]
> Aanvullende configuratie van de toepassingsgateway, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway is geconfigureerd en niet tijdens de eerste installatie.

## <a name="before-you-begin"></a>Voordat u begint

Azure Application Gateway vereist een eigen subnet. Zorg ervoor dat u onvoldoende adresruimte voor meerdere subnetten hebben laten bij het maken van een virtueel netwerk. Wanneer u een toepassingsgateway met een subnet implementeert, kunnen alleen andere Toepassingsgateways worden toegevoegd aan het subnet.

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.

Open de **Microsoft Azure-opdrachtprompt**, en zich aanmelden. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> U kunt ook `az login` zonder dat de switch voor apparaat aanmelding waarvoor een code op aka.ms/devicelogin invoert.

Wanneer u in het voorgaande voorbeeld typt, wordt een code opgegeven. Ga naar https://aka.ms/devicelogin in een browser om terug te gaan met de aanmelding.

![cmd tonen apparaat aanmelding][1]

Voer de code die u hebt ontvangen in de browser. U wordt omgeleid naar een aanmeldingspagina.

![browser-code invoeren][2]

Zodra de code is ingevoerd. u bent aangemeld, sluit de browser om door te gaan op met het scenario.

![aangemeld][3]

## <a name="create-the-resource-group"></a>De resourcegroep maken

Voordat u de toepassingsgateway maakt, wordt een resourcegroep gemaakt voor de toepassingsgateway. Hieronder ziet u de opdracht.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a>De toepassingsgateway maken

De IP-adressen gebruikt voor de back-end zijn de IP-adressen voor uw back-endserver. Deze waarden kunnen worden persoonlijke IP-adressen in het virtuele netwerk, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers. Het volgende voorbeeld maakt een toepassingsgateway met extra configuratie-instellingen voor HTTP-instellingen, poorten en regels.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Het vorige voorbeeld ziet u veel eigenschappen die niet vereist zijn tijdens het maken van een toepassingsgateway. Het volgende codevoorbeeld maakt een toepassingsgateway met de vereiste informatie.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Voor een lijst met parameters die kan worden opgegeven tijdens het maken van de volgende opdracht uitvoeren: `az network application-gateway create --help`.

In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor de listener, back-endpool, back-end-http-instellingen en -regels. U kunt deze instellingen aanpassen aan uw implementatie wanneer het inrichten voltooid is, kunt wijzigen.
Als u al uw webtoepassing gedefinieerd met behulp van de back endpool in de voorgaande stappen hebt uitgevoerd, eenmaal is gemaakt, begint taakverdeling.

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway. [Een aangepaste domeinnaam configureren voor in Azure](../dns/dns-custom-domain.md). Voor het configureren van een alias ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway. De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst. Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
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

## <a name="delete-all-resources"></a>Alle resources verwijderen

Als u alle resources wilt verwijderen die u in dit artikel hebt gemaakt, voert u de volgende stappen uit:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Volgende stappen

Informatie over het maken van aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)

Informatie over het configureren van SSL-Offloading en nemen de kostbare SSL-ontsleuteling uit uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
