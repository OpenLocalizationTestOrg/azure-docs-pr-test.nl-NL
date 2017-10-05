---
title: Maken van een Azure Application Gateway - Azure CLI 1.0 | Microsoft Docs
description: Informatie over het maken van een toepassingsgateway met behulp van de Azure CLI 1.0 in Resource Manager
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
ms.openlocfilehash: e7b16e789e0f241aa8ca2292aacb2bccde8777ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-cli"></a><span data-ttu-id="03406-103">Een toepassingsgateway maken met behulp van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="03406-103">Create an application gateway by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="03406-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="03406-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="03406-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="03406-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="03406-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="03406-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="03406-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="03406-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="03406-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="03406-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="03406-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="03406-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="03406-110">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="03406-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="03406-111">De gateway biedt opties voor failovers en het routeren van HTTP-aanvragen tussen servers (on-premises en in de cloud).</span><span class="sxs-lookup"><span data-stu-id="03406-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="03406-112">Toepassingsgateway bevat de volgende functies van de toepassing-levering: HTTP load balancing, sessie cookies gebaseerde affiniteit en Secure Sockets Layer (SSL)-offload, aangepaste statuscontroles en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="03406-112">Application gateway has the following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-the-azure-cli"></a><span data-ttu-id="03406-113">Voorwaarde: Installeer de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="03406-113">Prerequisite: Install the Azure CLI</span></span>

<span data-ttu-id="03406-114">Als u wilt de stappen in dit artikel uitvoert, moet u [installeren van de Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI)](../xplat-cli-install.md) en u moet [Meld u aan bij Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="03406-114">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need to [log on to Azure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="03406-115">Als u geen Azure-account hebt, moet u een.</span><span class="sxs-lookup"><span data-stu-id="03406-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="03406-116">U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="03406-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="03406-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="03406-117">Scenario</span></span>

<span data-ttu-id="03406-118">In dit scenario wordt informatie over het maken van een toepassingsgateway met Azure portal.</span><span class="sxs-lookup"><span data-stu-id="03406-118">In this scenario, you learn how to create an application gateway using the Azure portal.</span></span>

<span data-ttu-id="03406-119">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="03406-119">This scenario will:</span></span>

* <span data-ttu-id="03406-120">Een middelgrote toepassingsgateway maken met twee exemplaren.</span><span class="sxs-lookup"><span data-stu-id="03406-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="03406-121">Maak een virtueel netwerk met de naam ContosoVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="03406-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="03406-122">Maak een subnet met de naam subnet01 dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="03406-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="03406-123">Aanvullende configuratie van de toepassingsgateway, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway is geconfigureerd en niet tijdens de eerste installatie.</span><span class="sxs-lookup"><span data-stu-id="03406-123">Additional configuration of the application gateway, including custom health probes, backend pool addresses, and additional rules are configured after the application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="03406-124">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="03406-124">Before you begin</span></span>

<span data-ttu-id="03406-125">Azure Application Gateway vereist een eigen subnet.</span><span class="sxs-lookup"><span data-stu-id="03406-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="03406-126">Zorg ervoor dat u onvoldoende adresruimte voor meerdere subnetten hebben laten bij het maken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="03406-126">When creating a virtual network, ensure that you leave enough address space to have multiple subnets.</span></span> <span data-ttu-id="03406-127">Wanneer u een toepassingsgateway met een subnet implementeert, kunnen alleen andere Toepassingsgateways worden toegevoegd aan het subnet.</span><span class="sxs-lookup"><span data-stu-id="03406-127">Once you deploy an application gateway to a subnet, only additional application gateways are able to be added to the subnet.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="03406-128">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="03406-128">Log in to Azure</span></span>

<span data-ttu-id="03406-129">Open de **Microsoft Azure-opdrachtprompt**, en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="03406-129">Open the **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="03406-130">Wanneer u in het voorgaande voorbeeld typt, wordt een code opgegeven.</span><span class="sxs-lookup"><span data-stu-id="03406-130">Once you type the preceding example, a code is provided.</span></span> <span data-ttu-id="03406-131">Ga naar https://aka.ms/devicelogin in een browser om terug te gaan met de aanmelding.</span><span class="sxs-lookup"><span data-stu-id="03406-131">Navigate to https://aka.ms/devicelogin in a browser to continue the login process.</span></span>

![cmd tonen apparaat aanmelding][1]

<span data-ttu-id="03406-133">Voer de code die u hebt ontvangen in de browser.</span><span class="sxs-lookup"><span data-stu-id="03406-133">In the browser, enter the code you received.</span></span> <span data-ttu-id="03406-134">U wordt omgeleid naar een aanmeldingspagina.</span><span class="sxs-lookup"><span data-stu-id="03406-134">You are redirected to a sign-in page.</span></span>

![browser-code invoeren][2]

<span data-ttu-id="03406-136">Zodra de code is ingevoerd. u bent aangemeld, sluit de browser om door te gaan op met het scenario.</span><span class="sxs-lookup"><span data-stu-id="03406-136">Once the code has been entered you are signed in, close the browser to continue on with the scenario.</span></span>

![aangemeld][3]

## <a name="switch-to-resource-manager-mode"></a><span data-ttu-id="03406-138">Overschakelen naar de modus Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03406-138">Switch to Resource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-the-resource-group"></a><span data-ttu-id="03406-139">De resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="03406-139">Create the resource group</span></span>

<span data-ttu-id="03406-140">Voordat u de toepassingsgateway maakt, wordt een resourcegroep gemaakt voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="03406-140">Before creating the application gateway, a resource group is created to contain the application gateway.</span></span> <span data-ttu-id="03406-141">Hieronder ziet u de opdracht.</span><span class="sxs-lookup"><span data-stu-id="03406-141">The following shows the command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="03406-142">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="03406-142">Create a virtual network</span></span>

<span data-ttu-id="03406-143">Zodra de resourcegroep is gemaakt, wordt een virtueel netwerk gemaakt voor de toepassingsgateway.</span><span class="sxs-lookup"><span data-stu-id="03406-143">Once the resource group is created, a virtual network is created for the application gateway.</span></span>  <span data-ttu-id="03406-144">In het volgende voorbeeld is de adresruimte als 10.0.0.0/16 zoals gedefinieerd in de notities bij de voorgaande scenario.</span><span class="sxs-lookup"><span data-stu-id="03406-144">In the following example, the address space was as 10.0.0.0/16 as defined in the preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="03406-145">Een subnet maken</span><span class="sxs-lookup"><span data-stu-id="03406-145">Create a subnet</span></span>

<span data-ttu-id="03406-146">Nadat het virtuele netwerk is gemaakt, wordt een subnet voor de toepassingsgateway toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="03406-146">After the virtual network is created, a subnet is added for the application gateway.</span></span>  <span data-ttu-id="03406-147">Als u van plan bent gebruik toepassingsgateway met een web-app gehost in hetzelfde virtuele netwerk als de toepassingsgateway, zorg er dan voor dat onvoldoende ruimte is voor een ander subnet.</span><span class="sxs-lookup"><span data-stu-id="03406-147">If you plan to use application gateway with a web app hosted in the same virtual network as the application gateway, be sure to leave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="03406-148">De toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="03406-148">Create the application gateway</span></span>

<span data-ttu-id="03406-149">Als het virtuele netwerk en het subnet zijn gemaakt, zijn de vereisten voor de toepassingsgateway zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="03406-149">Once the virtual network and subnet are created, the pre-requisites for the application gateway are complete.</span></span> <span data-ttu-id="03406-150">Bovendien een eerder geëxporteerde pfx-certificaat en het wachtwoord voor het certificaat zijn vereist voor de volgende stap: het IP-adressen gebruikt voor de back-end zijn de IP-adressen voor uw back-endserver.</span><span class="sxs-lookup"><span data-stu-id="03406-150">Additionally a previously exported .pfx certificate and the password for the certificate are required for the following step: The IP addresses used for the backend are the IP addresses for your backend server.</span></span> <span data-ttu-id="03406-151">Deze waarden kunnen worden persoonlijke IP-adressen in het virtuele netwerk, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers.</span><span class="sxs-lookup"><span data-stu-id="03406-151">These values can be either private IPs in the virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="03406-152">Voor een lijst met parameters die kan worden opgegeven tijdens het maken van de volgende opdracht uitvoeren: **netwerk van azure-toepassingsgateway maken--help**.</span><span class="sxs-lookup"><span data-stu-id="03406-152">For a list of parameters that can be provided during creation run the following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="03406-153">In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor de listener, back-endpool, back-end-http-instellingen en -regels.</span><span class="sxs-lookup"><span data-stu-id="03406-153">This example creates a basic application gateway with default settings for the listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="03406-154">U kunt deze instellingen aanpassen aan uw implementatie wanneer het inrichten voltooid is, kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="03406-154">You can modify these settings to suit your deployment once the provisioning is successful.</span></span>
<span data-ttu-id="03406-155">Als u al uw webtoepassing gedefinieerd met behulp van de back endpool in de voorgaande stappen hebt uitgevoerd, eenmaal is gemaakt, begint taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="03406-155">If you already have your web application defined with the backend pool in the preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03406-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03406-156">Next steps</span></span>

<span data-ttu-id="03406-157">Informatie over het maken van aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="03406-157">Learn how to create custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="03406-158">Informatie over het configureren van SSL-Offloading en nemen de kostbare SSL-ontsleuteling uit uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="03406-158">Learn how to configure SSL Offloading and take the costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
