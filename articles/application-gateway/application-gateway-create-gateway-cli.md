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
# <a name="create-an-application-gateway-by-using-the-azure-cli-20"></a><span data-ttu-id="cd8f8-103">Een toepassingsgateway maken met behulp van de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd8f8-103">Create an application gateway by using the Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd8f8-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="cd8f8-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="cd8f8-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd8f8-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="cd8f8-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd8f8-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="cd8f8-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="cd8f8-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="cd8f8-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="cd8f8-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="cd8f8-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd8f8-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="cd8f8-110">Application Gateway is een toegewezen virtueel apparaat waarmee de toepassing levering controller (ADC) als een service biedt verschillende laag 7 load balancing mogelijkheden voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-110">Application Gateway is a dedicated virtual appliance that provides application delivery controller (ADC) as a service, offering various layer 7 load balancing capabilities for your application.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="cd8f8-111">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="cd8f8-111">CLI versions to complete the task</span></span>

<span data-ttu-id="cd8f8-112">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="cd8f8-112">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="cd8f8-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md): onze CLI voor het klassieke implementatiemodel en het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-113">[Azure CLI 1.0](application-gateway-create-gateway-cli-nodejs.md) - our CLI for the classic and resource management deployment models.</span></span>
* <span data-ttu-id="cd8f8-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md): onze CLI van de volgende generatie voor het Resource Manager-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="cd8f8-114">[Azure CLI 2.0](application-gateway-create-gateway-cli.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisite-install-the-azure-cli-20"></a><span data-ttu-id="cd8f8-115">Voorwaarde: Installeer de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd8f8-115">Prerequisite: Install the Azure CLI 2.0</span></span>

<span data-ttu-id="cd8f8-116">Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="cd8f8-116">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

> [!NOTE]
> <span data-ttu-id="cd8f8-117">Als u geen Azure-account hebt, moet u een.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-117">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="cd8f8-118">U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="cd8f8-118">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="cd8f8-119">Scenario</span><span class="sxs-lookup"><span data-stu-id="cd8f8-119">Scenario</span></span>

<span data-ttu-id="cd8f8-120">In dit scenario wordt informatie over het maken van een toepassingsgateway met Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-120">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="cd8f8-121">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="cd8f8-121">This scenario will:</span></span>

* <span data-ttu-id="cd8f8-122">Een middelgrote toepassingsgateway maken met twee exemplaren.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-122">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="cd8f8-123">Maak een virtueel netwerk met de naam AdatumAppGatewayVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-123">Create a virtual network named AdatumAppGatewayVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="cd8f8-124">Maakt u een subnet met de naam Appgatewaysubnet dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-124">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="cd8f8-125">Aanvullende configuratie van de toepassingsgateway, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway is geconfigureerd en niet tijdens de eerste installatie.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-125">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cd8f8-126">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="cd8f8-126">Before you begin</span></span>

<span data-ttu-id="cd8f8-127">Azure Application Gateway vereist een eigen subnet.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-127">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="cd8f8-128">Zorg ervoor dat u onvoldoende adresruimte voor meerdere subnetten hebben laten bij het maken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-128">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="cd8f8-129">Wanneer u een toepassingsgateway met een subnet implementeert, kunnen alleen andere Toepassingsgateways worden toegevoegd aan het subnet.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-129">Once you deploy an application gateway to a subnet, only additional application gateways can be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="cd8f8-130">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-130">Log in to Azure</span></span>

<span data-ttu-id="cd8f8-131">Open de **Microsoft Azure-opdrachtprompt**, en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-131">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="cd8f8-132">U kunt ook `az login` zonder dat de switch voor apparaat aanmelding waarvoor een code op aka.ms/devicelogin invoert.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-132">You can also use `az login` without the switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="cd8f8-133">Wanneer u in het voorgaande voorbeeld typt, wordt een code opgegeven.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-133">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="cd8f8-134">Ga naar https://aka.ms/devicelogin in een browser om terug te gaan met de aanmelding.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-134">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd tonen apparaat aanmelding][1]

<span data-ttu-id="cd8f8-136">Voer de code die u hebt ontvangen in de browser.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-136">In the browser, enter the code you received.</span></span> <span data-ttu-id="cd8f8-137">U wordt omgeleid naar een aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-137">You are redirected to a sign-in page.</span></span>

![browser-code invoeren][2]

<span data-ttu-id="cd8f8-139">Zodra de code is ingevoerd. u bent aangemeld, sluit de browser om door te gaan op met het scenario.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-139">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![aangemeld][3]

## <a name="create-the-resource-group"></a><span data-ttu-id="cd8f8-141">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="cd8f8-141">Create the resource group</span></span>

<span data-ttu-id="cd8f8-142">Voordat u de toepassingsgateway maakt, wordt een resourcegroep gemaakt voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-142">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="cd8f8-143">Hieronder ziet u de opdracht.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-143">The following shows the command.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="cd8f8-144">De toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="cd8f8-144">Create the application gateway</span></span>

<span data-ttu-id="cd8f8-145">De IP-adressen gebruikt voor de back-end zijn de IP-adressen voor uw back-endserver.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-145">The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="cd8f8-146">Deze waarden kunnen worden persoonlijke IP-adressen in het virtuele netwerk, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-146">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span> <span data-ttu-id="cd8f8-147">Het volgende voorbeeld maakt een toepassingsgateway met extra configuratie-instellingen voor HTTP-instellingen, poorten en regels.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-147">The following example creates an application gateway with additional configuration settings for http settings, ports, and rules.</span></span>

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

<span data-ttu-id="cd8f8-148">Het vorige voorbeeld ziet u veel eigenschappen die niet vereist zijn tijdens het maken van een toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-148">The preceding example shows many properties that are not required during the creation of an application gateway.</span></span> <span data-ttu-id="cd8f8-149">Het volgende codevoorbeeld maakt een toepassingsgateway met de vereiste informatie.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-149">The following code example creates an application gateway with the required information.</span></span>

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
> <span data-ttu-id="cd8f8-150">Voor een lijst met parameters die kan worden opgegeven tijdens het maken van de volgende opdracht uitvoeren: `az network application-gateway create --help`.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-150">For a list of parameters that can be provided during creation run the following command: `az network application-gateway create --help`.</span></span>

<span data-ttu-id="cd8f8-151">In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor de listener, back-endpool, back-end-http-instellingen en -regels.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-151">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="cd8f8-152">U kunt deze instellingen aanpassen aan uw implementatie wanneer het inrichten voltooid is, kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-152">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="cd8f8-153">Als u al uw webtoepassing gedefinieerd met behulp van de back endpool in de voorgaande stappen hebt uitgevoerd, eenmaal is gemaakt, begint taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-153">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="cd8f8-154">DNS-naam van toepassingsgateway verkrijgen</span><span class="sxs-lookup"><span data-stu-id="cd8f8-154">Get application gateway DNS name</span></span>

<span data-ttu-id="cd8f8-155">Wanneer de gateway is gemaakt, gaat u in de volgende stap de front-end voor communicatie configureren.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-155">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="cd8f8-156">Wanneer u een openbare IP gebruikt, heeft de toepassingsgateway een dynamisch toegewezen DNS-naam nodig. Dit is niet gebruiksvriendelijk.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-156">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="cd8f8-157">Om ervoor te zorgen dat eindgebruikers de toepassingsgateway kunnen bereiken, kan een CNAME-record worden gebruikt die verwijst naar het openbare eindpunt van de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-157">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="cd8f8-158">[Een aangepaste domeinnaam configureren voor in Azure](../dns/dns-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="cd8f8-158">[Configuring a custom domain name for in Azure](../dns/dns-custom-domain.md).</span></span> <span data-ttu-id="cd8f8-159">Voor het configureren van een alias ophalen van gegevens van de toepassingsgateway en de bijbehorende IP-en DNS-naam met behulp van de PublicIPAddress-element dat is gekoppeld aan de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-159">To configure an alias, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="cd8f8-160">De DNS-naam van de toepassingsgateway moet worden gebruikt om een CNAME-record te maken die de twee webtoepassingen naar deze DNS-naam wijst.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-160">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="cd8f8-161">Het gebruik van A-records wordt niet aanbevolen, omdat het VIP kan veranderen wanneer de toepassingsgateway opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="cd8f8-161">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="delete-all-resources"></a><span data-ttu-id="cd8f8-162">Alle resources verwijderen</span><span class="sxs-lookup"><span data-stu-id="cd8f8-162">Delete all resources</span></span>

<span data-ttu-id="cd8f8-163">Als u alle resources wilt verwijderen die u in dit artikel hebt gemaakt, voert u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="cd8f8-163">To delete all resources created in this article, complete the following steps:</span></span>

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a><span data-ttu-id="cd8f8-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd8f8-164">Next steps</span></span>

<span data-ttu-id="cd8f8-165">Informatie over het maken van aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cd8f8-165">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="cd8f8-166">Informatie over het configureren van SSL-Offloading en nemen de kostbare SSL-ontsleuteling uit uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="cd8f8-166">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
