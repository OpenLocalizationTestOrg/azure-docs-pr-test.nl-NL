---
title: aaaConfigure SSL-offload - Azure Application Gateway - Azure CLI 2.0 | Microsoft Docs
description: Deze pagina vindt u instructies toocreate een toepassingsgateway met SSL-offload met Azure CLI 2.0
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: f8d50e0c6ffef17c807938d816410e6d85321c9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-cli-20"></a>Een toepassingsgateway voor SSL-offload configureren met behulp van Azure CLI 2.0

> [!div class="op_single_selector"]
> * [Azure Portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

Azure Application Gateway kan worden geconfigureerd tooterminate Hallo Secure Sockets Layer (SSL)-sessie op Hallo gateway tooavoid kostbare SSL ontsleuteling taken toohappen op Hallo-webfarm. SSL-offload vereenvoudigt ook Certificaatbeheer op Hallo front-endserver.

## <a name="prerequisite-install-hello-azure-cli-20"></a>Voorwaarde: Installeer hello Azure CLI 2.0

tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="required-components"></a>Vereiste onderdelen

* **Back-endserverpool:** Hallo lijst met IP-adressen van Hallo back-endservers. Hallo IP-adressen moeten ofwel deel uitmaken toohello virtueel netwerksubnet ofwel moeten een openbare IP-/ VIP.
* **Back-endserverpoolinstellingen:** elke pool heeft instellingen, zoals voor de poort, het protocol en de op cookies gebaseerde affiniteit. Deze instellingen zijn gebonden tooa servergroep en toegepaste tooall servers binnen de pool Hallo zijn.
* **Front-endpoort:** deze is Hallo openbare poort die in Hallo toepassingsgateway wordt geopend. Verkeer komt binnen via deze poort en vervolgens wordt omgeleid tooone van Hallo back-endservers.
* **Listener:** Hallo listener beschikt over een front-endpoort, een protocol (Http of Https; deze instellingen zijn hoofdlettergevoelig), en Hallo SSL-certificaatnaam (als u SSL-offloading configureert).
* **Regel:** Hallo regel verbindt Hallo listener Hallo back-endserverpool en definieert welk verkeer van back-endserver groep Hallo moet gerichte toowhen dit bij een bepaalde listener aankomt. Op dit moment alleen Hallo *basic* regel wordt ondersteund. Hallo *basic* regel is round-robinbelastingverdeling.

**Aanvullende configuratieopmerkingen**

Hallo-protocol in voor de configuratie van SSL-certificaten, **HttpListener** moet ook wijzigen*Https* (hoofdlettergevoelig). Hallo **SslCertificate** element te toegevoegd**HttpListener** met Hallo variabele waarde die is geconfigureerd voor SSL-certificaat Hallo. Hallo front-endpoort moet bijgewerkte too443.

**tooenable cookies gebaseerde affiniteit**: een application gateway kan worden geconfigureerd tooensure is een aanvraag van een clientsessie altijd gerichte toohello dezelfde virtuele machine in de webfarm Hallo. Dit scenario wordt gedaan door het injecteren van een sessiecookie waarmee Hallo gateway toodirect verkeer op de juiste wijze. tooenable cookies gebaseerde affiniteit ingesteld **CookieBasedAffinity** te*ingeschakeld* in Hallo **BackendHttpSettings** element.

## <a name="configure-ssl-offload-on-an-existing-application-gateway"></a>SSL-offload configureren op een bestaande application gateway

```azurecli-interactive
#!/bin/bash

# Create a new front end port toobe used for SSL
az network application-gateway frontend-port create \
  --name sslport \
  --port 443 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Upload hello .pfx certificate for SSL offload
az network application-gateway ssl-cert create \
  --name "newcert" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new listener referencing hello port and certificate created earlier
az network application-gateway http-listener create \
  --frontend-ip "appGatewayFrontendIP" \
  --frontend-port sslport  \
  --name sslListener \
  --ssl-cert newcert \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new back-end pool toobe used
az network application-gateway address-pool create \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG" \
  --name "appGatewayBackendPool2" \
  --servers 10.0.0.7 10.0.0.8

# Create a new back-end HTTP settings using hello new probe
az network application-gateway http-settings create \
  --name "settings2" \
  --port 80 \
  --cookie-based-affinity Enabled \
  --protocol "Http" \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

# Create a new rule linking hello listener toohello back-end pool
az network application-gateway rule create \
  --name "rule2" \
  --rule-type Basic \
  --http-settings settings2 \
  --http-listener ssllistener \
  --address-pool temp1 \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"

```

## <a name="create-an-application-gateway-with-ssl-offload"></a>Een toepassingsgateway maken met de SSL-Offload

Hallo volgende voorbeeld maakt een toepassingsgateway met SSL-offload.  Hallo-certificaat en het wachtwoord voor certificaat moeten bijgewerkte tooa geldige persoonlijke sleutel.

```azurecli-interactive
#!/bin/bash

# Creates an application gateway with SSL offload
az network application-gateway create \
  --name "AdatumAppGateway3" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG2" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --cert-file /home/azureuser/self-signed/AdatumAppGatewayCert.pfx \
  --cert-password P@ssw0rd \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet" \
  --subnet-address-prefix "10.0.0.0/28" \
  --frontend-port 443 \
  --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 \
  --sku "Standard_Small" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip" \
  --public-ip-address-allocation "dynamic"
```

## <a name="get-application-gateway-dns-name"></a>DNS-naam van toepassingsgateway verkrijgen

Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie. Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk. eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo. [Een aangepaste domeinnaam configureren voor in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure een alias ophalen van gegevens van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met. Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam. Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.


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

## <a name="next-steps"></a>Volgende stappen

Als u wilt tooconfigure een toouse application gateway met een interne load balancer (ILB), Zie [een toepassingsgateway maken met een interne load balancer (ILB)](application-gateway-ilb.md).

Als u meer informatie wilt over de algemene opties voor load balancing, raadpleegt u:

* [Azure Load Balancer](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)
