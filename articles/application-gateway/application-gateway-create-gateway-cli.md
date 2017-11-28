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
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a><span data-ttu-id="9d418-103">Een toepassingsgateway maken met behulp van hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d418-103">Create an application gateway by using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d418-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9d418-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="9d418-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d418-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="9d418-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d418-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="9d418-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="9d418-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="9d418-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9d418-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="9d418-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d418-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="9d418-110">Application Gateway is een toegewezen virtueel apparaat waarmee de toepassing levering controller (ADC) als een service biedt verschillende laag 7 load balancing mogelijkheden voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9d418-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9d418-111">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="9d418-111">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="9d418-112">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d418-112">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="9d418-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) -onze CLI voor Hallo klassieke en resource management implementatiemodellen.</span><span class="sxs-lookup"><span data-stu-id="9d418-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for hello classic and resource management deployment models.</span></span>
* <span data-ttu-id="9d418-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="9d418-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisite-install-hello-azure-cli-20"></a><span data-ttu-id="9d418-115">Voorwaarde: Installeer hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9d418-115">Prerequisite: Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="9d418-116">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9d418-116">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="9d418-117">Als u geen Azure-account hebt, moet u een.</span><span class="sxs-lookup"><span data-stu-id="9d418-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="9d418-118">U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="9d418-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="9d418-119">Scenario</span><span class="sxs-lookup"><span data-stu-id="9d418-119">Scenario</span></span>

<span data-ttu-id="9d418-120">In dit scenario leert u hoe een application gateway met toocreate hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9d418-120">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="9d418-121">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="9d418-121">This scenario will:</span></span>

* <span data-ttu-id="9d418-122">Een middelgrote toepassingsgateway maken met twee exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9d418-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="9d418-123">Maak een virtueel netwerk met de naam AdatumAppGatewayVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="9d418-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="9d418-124">Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="9d418-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="9d418-125">Aanvullende configuratie van de toepassingsgateway hello, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway Hallo is geconfigureerd en niet tijdens de eerste installatie.</span><span class="sxs-lookup"><span data-stu-id="9d418-125">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9d418-126">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9d418-126">Before you begin</span></span>

<span data-ttu-id="9d418-127">Azure Application Gateway vereist een eigen subnet.</span><span class="sxs-lookup"><span data-stu-id="9d418-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="9d418-128">Zorg ervoor dat u laat u genoeg ruimte adres toohave meerdere subnetten bij het maken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="9d418-128">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="9d418-129">Wanneer u een subnet toepassingsgateway tooa implementeert, kunnen alleen andere Toepassingsgateways toohello subnet worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9d418-129">Once you deploy an application gateway tooa subnet, only additional application gateways can be added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="9d418-130">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="9d418-130">Log in tooAzure</span></span>

<span data-ttu-id="9d418-131">Open Hallo **Microsoft Azure-opdrachtprompt**, en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="9d418-131">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="9d418-132">U kunt ook `az login` zonder Hallo switch voor apparaat aanmelding waarvoor een code op aka.ms/devicelogin invoert.</span><span class="sxs-lookup"><span data-stu-id="9d418-132">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="9d418-133">Wanneer u Hallo voorgaande voorbeeld typt, wordt een code opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9d418-133">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="9d418-134">Navigeer toohttps://aka.ms/devicelogin in een browser toocontinue Hallo aanmeldingsproces.</span><span class="sxs-lookup"><span data-stu-id="9d418-134">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd tonen apparaat aanmelding][1]

<span data-ttu-id="9d418-136">Voer in de browser Hallo Hallo-code die u hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="9d418-136">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="9d418-137">U staat op de aanmeldingspagina omgeleide tooa.</span><span class="sxs-lookup"><span data-stu-id="9d418-137">You are redirected tooa sign-in page.</span></span>

![browser tooenter code][2]

<span data-ttu-id="9d418-139">Zodra het Hallo-code is ingevoerd u bent aangemeld, sluiten Hallo browser toocontinue op met de Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="9d418-139">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![aangemeld][3]

## <a name="create-hello-resource-group"></a><span data-ttu-id="9d418-141">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="9d418-141">Create hello resource group</span></span>

<span data-ttu-id="9d418-142">Voordat u de toepassingsgateway Hallo maakt, wordt een resourcegroep toocontain Hallo toepassingsgateway gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d418-142">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="9d418-143">Hallo hieronder vindt u Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="9d418-143">hello following shows hello command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="9d418-144">Hallo toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="9d418-144">Create hello application gateway</span></span>

<span data-ttu-id="9d418-145">Hallo IP-adressen gebruikt voor back-end voor Hallo zijn Hallo IP-adressen voor uw back-endserver.</span><span class="sxs-lookup"><span data-stu-id="9d418-145">hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="9d418-146">Deze waarden mag ofwel persoonlijke IP-adressen in het virtuele netwerk hello, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers.</span><span class="sxs-lookup"><span data-stu-id="9d418-146">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="9d418-147">Hallo volgende voorbeeld wordt een toepassingsgateway met extra configuratie-instellingen voor HTTP-instellingen, poorten en regels.</span><span class="sxs-lookup"><span data-stu-id="9d418-147">hello following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="9d418-148">Hallo voorgaande voorbeeld ziet u veel eigenschappen die niet vereist zijn tijdens het maken van een toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d418-148">hello preceding example shows many properties that are not required during hello creation of an application gateway.</span></span> <span data-ttu-id="9d418-149">Hallo volgende codevoorbeeld maakt een toepassingsgateway met Hallo vereiste informatie.</span><span class="sxs-lookup"><span data-stu-id="9d418-149">hello following code example creates an application gateway with hello required information.</span></span>

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
> <span data-ttu-id="9d418-150">Voor een lijst met parameters die kan worden opgegeven tijdens maken uitvoeren Hallo volgende opdracht: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="9d418-150">For a list of parameters that can be provided during creation run hello following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="9d418-151">In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor het Hallo-listener, back-endpool, back-end-http-instellingen en -regels.</span><span class="sxs-lookup"><span data-stu-id="9d418-151">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="9d418-152">U kunt deze instellingen toosuit uw implementatie wijzigen wanneer Hallo inrichten voltooid is.</span><span class="sxs-lookup"><span data-stu-id="9d418-152">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="9d418-153">Als u al uw webtoepassing gedefinieerd met behulp van back-endpool in de vorige stappen, eenmaal is gemaakt, Hallo Hallo begint taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="9d418-153">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="9d418-154">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="9d418-154">Get application gateway DNS name</span></span>

<span data-ttu-id="9d418-155">Zodra Hallo gateway is gemaakt, is de volgende stap Hallo tooconfigure Hallo front-end voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="9d418-155">Once hello gateway is created, hello next step is tooconfigure hello front end for communication.</span></span> <span data-ttu-id="9d418-156">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="9d418-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="9d418-157">eindgebruikers tooensure kunt Hallo toepassingsgateway bereikt, een CNAME-record kan gebruikte toopoint toohello openbaar eindpunt van de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d418-157">tooensure end users can hit hello application gateway, a CNAME record can be used toopoint toohello public endpoint of hello application gateway.</span></span> <span data-ttu-id="9d418-158">[Een aangepaste domeinnaam configureren voor in Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9d418-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="9d418-159">tooconfigure een alias ophalen van gegevens van de toepassingsgateway Hallo en de bijbehorende IP-en DNS-naam op Hallo PublicIPAddress element gekoppelde toohello application gateway met.</span><span class="sxs-lookup"><span data-stu-id="9d418-159">tooconfigure an alias, retrieve details of hello application gateway and its associated IP/DNS name using hello PublicIPAddress element attached toohello application gateway.</span></span> <span data-ttu-id="9d418-160">Hallo application gateway DNS-naam moet gebruikte toocreate een CNAME-record punten Hallo twee web applications toothis DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="9d418-160">hello application gateway's DNS name should be used toocreate a CNAME record, which points hello two web applications toothis DNS name.</span></span> <span data-ttu-id="9d418-161">Hallo-gebruik van A-records wordt niet aanbevolen omdat Hallo VIP bij opnieuw opstarten van toepassingsgateway mag wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9d418-161">hello use of A-records is not recommended since hello VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="9d418-162">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="9d418-162">Delete all resources</span></span>

<span data-ttu-id="9d418-163">toodelete alle resources die worden gemaakt in dit artikel wordt voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d418-163">toodelete all resources created in this article, complete hello following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="9d418-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d418-164">Next steps</span></span>

<span data-ttu-id="9d418-165">Meer informatie over hoe toocreate aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9d418-165">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="9d418-166">Meer informatie over hoe tooconfigure SSL-Offloading en los het Hallo kostbare SSL ontsleuteling uitgeschakeld in uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="9d418-166">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
