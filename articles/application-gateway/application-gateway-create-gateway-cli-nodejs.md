---
title: aaaCreate een Azure Application Gateway - Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe toocreate een toepassingsgateway met behulp van Azure CLI 1.0 in Resource Manager Hallo
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Een toepassingsgateway maken met behulp van hello Azure CLI

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager-sjabloon](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI 1.0](application-gateway-create-gateway-cli.md)
> * [Azure CLI 2.0](application-gateway-create-gateway-cli.md)
> 
> 

Azure Application Gateway is een load balancer in laag 7. Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises. Toepassingsgateway heeft Hallo levering toepassingsfuncties te volgen: HTTP load balancing, sessie cookies gebaseerde affiniteit en Secure Sockets Layer (SSL)-offload, aangepaste statuscontroles en ondersteuning voor meerdere locaties.

## <a name="prerequisite-install-hello-azure-cli"></a>Voorwaarde: Installeer hello Azure CLI

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](../xplat-cli-install.md) en u moet te[tooAzure aanmelden](../xplat-cli-connect.md). 

> [!NOTE]
> Als u geen Azure-account hebt, moet u een. U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Scenario

In dit scenario leert u hoe een application gateway met toocreate hello Azure-portal.

Dit scenario wordt:

* Een middelgrote toepassingsgateway maken met twee exemplaren.
* Maak een virtueel netwerk met de naam ContosoVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.
* Maak een subnet met de naam subnet01 dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.

> [!NOTE]
> Aanvullende configuratie van de toepassingsgateway hello, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway Hallo is geconfigureerd en niet tijdens de eerste installatie.

## <a name="before-you-begin"></a>Voordat u begint

Azure Application Gateway vereist een eigen subnet. Zorg ervoor dat u laat u genoeg ruimte adres toohave meerdere subnetten bij het maken van een virtueel netwerk. Wanneer u een subnet toepassingsgateway tooa implementeert, enige extra toepassingsgateways kunnen toobe toegevoegd worden toohello subnet.

## <a name="log-in-tooazure"></a>Meld u bij tooAzure

Open Hallo **Microsoft Azure-opdrachtprompt**, en zich aanmelden. 

```azurecli-interactive
azure login
```

Wanneer u Hallo voorgaande voorbeeld typt, wordt een code opgegeven. Navigeer toohttps://aka.ms/devicelogin in een browser toocontinue Hallo aanmeldingsproces.

![cmd tonen apparaat aanmelding][1]

Voer in de browser Hallo Hallo-code die u hebt ontvangen. U staat op de aanmeldingspagina omgeleide tooa.

![browser tooenter code][2]

Zodra het Hallo-code is ingevoerd u bent aangemeld, sluiten Hallo browser toocontinue op met de Hallo scenario.

![aangemeld][3]

## <a name="switch-tooresource-manager-mode"></a>TooResource Manager-modus schakelen

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Hallo resourcegroep maken

Voordat u de toepassingsgateway Hallo maakt, wordt een resourcegroep toocontain Hallo toepassingsgateway gemaakt. Hallo hieronder vindt u Hallo-opdracht.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Een virtueel netwerk maken

Zodra de resourcegroep Hallo is gemaakt, wordt een virtueel netwerk gemaakt voor de toepassingsgateway Hallo.  Hallo-adresruimte is Hallo voorbeeld te volgen, als 10.0.0.0/16 zoals gedefinieerd in het voorgaande scenario notities Hallo.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Een subnet maken

Nadat het virtuele netwerk Hallo is gemaakt, wordt een subnet voor de toepassingsgateway Hallo toegevoegd.  Als u van plan bent toouse toepassingsgateway met een web-app gehost in Hallo hetzelfde virtuele netwerk als de toepassingsgateway hello, tooleave ervoor dat voldoende ruimte heeft voor een ander subnet worden.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Hallo toepassingsgateway maken

Zodra Hallo virtueel netwerk en subnet worden gemaakt, zijn vereisten voor de toepassingsgateway Hallo Hallo voltooid. Bovendien een eerder geëxporteerde .pfx-bestand certificaat en het Hallo-wachtwoord voor Hallo certificaat zijn vereist voor stap Hallo: Hallo IP-adressen gebruikt voor back-end voor Hallo zijn Hallo IP-adressen voor uw back-endserver. Deze waarden mag ofwel persoonlijke IP-adressen in het virtuele netwerk hello, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Voor een lijst met parameters die kan worden opgegeven tijdens het maken van Hallo volgende opdracht uitvoeren: **netwerk van azure-toepassingsgateway maken--help**.

In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor het Hallo-listener, back-endpool, back-end-http-instellingen en -regels. U kunt deze instellingen toosuit uw implementatie wijzigen wanneer Hallo inrichten voltooid is.
Als u al uw webtoepassing gedefinieerd met behulp van back-endpool in de vorige stappen, eenmaal is gemaakt, Hallo Hallo begint taakverdeling.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toocreate aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)

Meer informatie over hoe tooconfigure SSL-Offloading en los het Hallo kostbare SSL ontsleuteling uitgeschakeld in uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
