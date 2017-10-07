---
title: aaaCreate een Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs
description: Meer informatie over hoe toocreate een toepassingsgateway met behulp van Azure CLI 2.0 in Resource Manager Hallo
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
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Een toepassingsgateway maken met behulp van hello Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager-sjabloon](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)

Application Gateway is een toegewezen virtueel apparaat waarmee de toepassing levering controller (ADC) als een service biedt verschillende laag 7 load balancing mogelijkheden voor uw toepassing.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak

U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

* [Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.
* [Azure CLI 2.0](application-gateway-create-gateway-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="prerequisite-install-hello-azure-cli-20"></a>Voorwaarde: Installeer hello Azure CLI 2.0

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Als u geen Azure-account hebt, moet u een. U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenario

In dit scenario leert u hoe een application gateway met toocreate hello Azure-portal.

Dit scenario wordt:

* Een middelgrote toepassingsgateway maken met twee exemplaren.
* Maak een virtueel netwerk met de naam AdatumAppGatewayVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.
* Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.

> [!NOTE]
> Aanvullende configuratie van de toepassingsgateway hello, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway Hallo is geconfigureerd en niet tijdens de eerste installatie.

## <a name="before-you-begin"></a>Voordat u begint

Azure Application Gateway vereist een eigen subnet. Zorg ervoor dat u laat u genoeg ruimte adres toohave meerdere subnetten bij het maken van een virtueel netwerk. Wanneer u een subnet toepassingsgateway tooa implementeert, kunnen alleen andere Toepassingsgateways toohello subnet worden toegevoegd.

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Open Hallo **Microsoft Azure-opdrachtprompt**, en zich aanmelden. 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> U kunt ook `az login` zonder Hallo switch voor apparaat aanmelding waarvoor een code op aka.ms/devicelogin invoert.

Wanneer u Hallo voorgaande voorbeeld typt, wordt een code opgegeven. Navigeer toohttps://aka.ms/devicelogin in een browser toocontinue Hallo aanmeldingsproces.

![cmd tonen apparaat aanmelding][1]

Voer in de browser Hallo Hallo-code die u hebt ontvangen. U staat op de aanmeldingspagina omgeleide tooa.

![browser tooenter code][2]

Zodra het Hallo-code is ingevoerd u bent aangemeld, sluiten Hallo browser toocontinue op met de Hallo scenario.

![aangemeld][3]

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Voordat u de toepassingsgateway Hallo maakt, wordt een resourcegroep toocontain Hallo toepassingsgateway gemaakt. Hallo hieronder vindt u Hallo-opdracht.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Hallo toepassingsgateway maken

Hallo IP-adressen gebruikt voor back-end voor Hallo zijn Hallo IP-adressen voor uw back-endserver. Deze waarden mag ofwel persoonlijke IP-adressen in het virtuele netwerk hello, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers. Hallo volgende voorbeeld wordt een toepassingsgateway met extra configuratie-instellingen voor HTTP-instellingen, poorten en regels.

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

Hallo voorgaande voorbeeld ziet u veel eigenschappen die niet vereist zijn tijdens het maken van een toepassingsgateway Hallo. Hallo volgende codevoorbeeld maakt een toepassingsgateway met Hallo vereiste informatie.

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
> Voor een lijst met parameters die kan worden opgegeven tijdens maken uitvoeren Hallo volgende opdracht: `az network application-gateway create --help`.

In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor het Hallo-listener, back-endpool, back-end-http-instellingen en -regels. U kunt deze instellingen toosuit uw implementatie wijzigen wanneer Hallo inrichten voltooid is.
Als u al uw webtoepassing gedefinieerd met behulp van back-endpool in de vorige stappen, eenmaal is gemaakt, Hallo Hallo begint taakverdeling.

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo. [Een aangepaste domeinnaam configureren voor in Azure](../dns/dns-custom-domain.md). tooconfigure een alias ophalen van gegevens van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met. Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.


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

toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stappen te volgen:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toocreate aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)

Meer informatie over hoe tooconfigure SSL-Offloading en los het Hallo kostbare SSL ontsleuteling uitgeschakeld in uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
