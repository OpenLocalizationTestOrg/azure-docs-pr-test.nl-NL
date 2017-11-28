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
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a><span data-ttu-id="9fdb0-103">Een toepassingsgateway maken met behulp van hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9fdb0-103">Create an application gateway by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9fdb0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9fdb0-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="9fdb0-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fdb0-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="9fdb0-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fdb0-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="9fdb0-107">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="9fdb0-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="9fdb0-108">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9fdb0-108">Azure CLI 1.0</span></span>](application-gateway-create-gateway-cli.md)
> * [<span data-ttu-id="9fdb0-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9fdb0-109">Azure CLI 2.0</span></span>](application-gateway-create-gateway-cli.md)
> 
> 

<span data-ttu-id="9fdb0-110">Azure Application Gateway is een load balancer in laag 7.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-110">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="9fdb0-111">Het biedt failover, HTTP-aanvragen routeren tussen verschillende servers, ongeacht of deze op Hallo cloud of on-premises.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-111">It provides failover, performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="9fdb0-112">Toepassingsgateway heeft Hallo levering toepassingsfuncties te volgen: HTTP load balancing, sessie cookies gebaseerde affiniteit en Secure Sockets Layer (SSL)-offload, aangepaste statuscontroles en ondersteuning voor meerdere locaties.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-112">Application gateway has hello following application delivery features: HTTP load balancing, cookie-based session affinity, and Secure Sockets Layer (SSL) offload, custom health probes, and support for multi-site.</span></span>

## <a name="prerequisite-install-hello-azure-cli"></a><span data-ttu-id="9fdb0-113">Voorwaarde: Installeer hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9fdb0-113">Prerequisite: Install hello Azure CLI</span></span>

<span data-ttu-id="9fdb0-114">tooperform hello stappen in dit artikel, moet u te[hello Azure-opdrachtregelinterface voor Mac, Linux en Windows (Azure CLI) installeren](../xplat-cli-install.md) en u moet te[tooAzure aanmelden](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="9fdb0-114">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](../xplat-cli-install.md) and you need too[log on tooAzure](../xplat-cli-connect.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="9fdb0-115">Als u geen Azure-account hebt, moet u een.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-115">If you don't have an Azure account, you need one.</span></span> <span data-ttu-id="9fdb0-116">U kunt zich [hier aanmelden voor een gratis proefversie](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="9fdb0-116">Go sign up for a [free trial here](../active-directory/sign-up-organization.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="9fdb0-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="9fdb0-117">Scenario</span></span>

<span data-ttu-id="9fdb0-118">In dit scenario leert u hoe een application gateway met toocreate hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-118">In this scenario, you learn how toocreate an application gateway using hello Azure portal.</span></span>

<span data-ttu-id="9fdb0-119">Dit scenario wordt:</span><span class="sxs-lookup"><span data-stu-id="9fdb0-119">This scenario will:</span></span>

* <span data-ttu-id="9fdb0-120">Een middelgrote toepassingsgateway maken met twee exemplaren.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-120">Create a medium application gateway with two instances.</span></span>
* <span data-ttu-id="9fdb0-121">Maak een virtueel netwerk met de naam ContosoVNET met een gereserveerd CIDR-blok van 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-121">Create a virtual network named ContosoVNET with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="9fdb0-122">Maak een subnet met de naam subnet01 dat gebruikmaakt van 10.0.0.0/28 als CIDR-blok.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-122">Create a subnet called subnet01 that uses 10.0.0.0/28 as its CIDR block.</span></span>

> [!NOTE]
> <span data-ttu-id="9fdb0-123">Aanvullende configuratie van de toepassingsgateway hello, met inbegrip van aangepaste health tests, adressen van de groep back-end en extra regels worden geconfigureerd nadat de toepassingsgateway Hallo is geconfigureerd en niet tijdens de eerste installatie.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-123">Additional configuration of hello application gateway, including custom health probes, backend pool addresses, and additional rules are configured after hello application gateway is configured and not during initial deployment.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9fdb0-124">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9fdb0-124">Before you begin</span></span>

<span data-ttu-id="9fdb0-125">Azure Application Gateway vereist een eigen subnet.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-125">Azure Application Gateway requires its own subnet.</span></span> <span data-ttu-id="9fdb0-126">Zorg ervoor dat u laat u genoeg ruimte adres toohave meerdere subnetten bij het maken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-126">When creating a virtual network, ensure that you leave enough address space toohave multiple subnets.</span></span> <span data-ttu-id="9fdb0-127">Wanneer u een subnet toepassingsgateway tooa implementeert, enige extra toepassingsgateways kunnen toobe toegevoegd worden toohello subnet.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-127">Once you deploy an application gateway tooa subnet, only additional application gateways are able toobe added toohello subnet.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="9fdb0-128">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="9fdb0-128">Log in tooAzure</span></span>

<span data-ttu-id="9fdb0-129">Open Hallo **Microsoft Azure-opdrachtprompt**, en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-129">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli-interactive
azure login
```

<span data-ttu-id="9fdb0-130">Wanneer u Hallo voorgaande voorbeeld typt, wordt een code opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-130">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="9fdb0-131">Navigeer toohttps://aka.ms/devicelogin in een browser toocontinue Hallo aanmeldingsproces.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-131">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd tonen apparaat aanmelding][1]

<span data-ttu-id="9fdb0-133">Voer in de browser Hallo Hallo-code die u hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-133">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="9fdb0-134">U staat op de aanmeldingspagina omgeleide tooa.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-134">You are redirected tooa sign-in page.</span></span>

![browser tooenter code][2]

<span data-ttu-id="9fdb0-136">Zodra het Hallo-code is ingevoerd u bent aangemeld, sluiten Hallo browser toocontinue op met de Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-136">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![aangemeld][3]

## <a name="switch-tooresource-manager-mode"></a><span data-ttu-id="9fdb0-138">TooResource Manager-modus schakelen</span><span class="sxs-lookup"><span data-stu-id="9fdb0-138">Switch tooResource Manager Mode</span></span>

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a><span data-ttu-id="9fdb0-139">Hallo resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="9fdb0-139">Create hello resource group</span></span>

<span data-ttu-id="9fdb0-140">Voordat u de toepassingsgateway Hallo maakt, wordt een resourcegroep toocontain Hallo toepassingsgateway gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-140">Before creating hello application gateway, a resource group is created toocontain hello application gateway.</span></span> <span data-ttu-id="9fdb0-141">Hallo hieronder vindt u Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-141">hello following shows hello command.</span></span>

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="9fdb0-142">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="9fdb0-142">Create a virtual network</span></span>

<span data-ttu-id="9fdb0-143">Zodra de resourcegroep Hallo is gemaakt, wordt een virtueel netwerk gemaakt voor de toepassingsgateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-143">Once hello resource group is created, a virtual network is created for hello application gateway.</span></span>  <span data-ttu-id="9fdb0-144">Hallo-adresruimte is Hallo voorbeeld te volgen, als 10.0.0.0/16 zoals gedefinieerd in het voorgaande scenario notities Hallo.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-144">In hello following example, hello address space was as 10.0.0.0/16 as defined in hello preceding scenario notes.</span></span>

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a><span data-ttu-id="9fdb0-145">Een subnet maken</span><span class="sxs-lookup"><span data-stu-id="9fdb0-145">Create a subnet</span></span>

<span data-ttu-id="9fdb0-146">Nadat het virtuele netwerk Hallo is gemaakt, wordt een subnet voor de toepassingsgateway Hallo toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-146">After hello virtual network is created, a subnet is added for hello application gateway.</span></span>  <span data-ttu-id="9fdb0-147">Als u van plan bent toouse toepassingsgateway met een web-app gehost in Hallo hetzelfde virtuele netwerk als de toepassingsgateway hello, tooleave ervoor dat voldoende ruimte heeft voor een ander subnet worden.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-147">If you plan toouse application gateway with a web app hosted in hello same virtual network as hello application gateway, be sure tooleave enough room for another subnet.</span></span>

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a><span data-ttu-id="9fdb0-148">Hallo toepassingsgateway maken</span><span class="sxs-lookup"><span data-stu-id="9fdb0-148">Create hello application gateway</span></span>

<span data-ttu-id="9fdb0-149">Zodra Hallo virtueel netwerk en subnet worden gemaakt, zijn vereisten voor de toepassingsgateway Hallo Hallo voltooid.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-149">Once hello virtual network and subnet are created, hello pre-requisites for hello application gateway are complete.</span></span> <span data-ttu-id="9fdb0-150">Bovendien een eerder geëxporteerde .pfx-bestand certificaat en het Hallo-wachtwoord voor Hallo certificaat zijn vereist voor stap Hallo: Hallo IP-adressen gebruikt voor back-end voor Hallo zijn Hallo IP-adressen voor uw back-endserver.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-150">Additionally a previously exported .pfx certificate and hello password for hello certificate are required for hello following step: hello IP addresses used for hello backend are hello IP addresses for your backend server.</span></span> <span data-ttu-id="9fdb0-151">Deze waarden mag ofwel persoonlijke IP-adressen in het virtuele netwerk hello, openbare IP-adressen of volledig gekwalificeerde domeinnamen voor uw back-endservers.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-151">These values can be either private IPs in hello virtual network, public ips, or fully qualified domain names for your backend servers.</span></span>

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
> <span data-ttu-id="9fdb0-152">Voor een lijst met parameters die kan worden opgegeven tijdens het maken van Hallo volgende opdracht uitvoeren: **netwerk van azure-toepassingsgateway maken--help**.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-152">For a list of parameters that can be provided during creation run hello following command: **azure network application-gateway create --help**.</span></span>

<span data-ttu-id="9fdb0-153">In dit voorbeeld maakt een basic-toepassingsgateway met standaardinstellingen voor het Hallo-listener, back-endpool, back-end-http-instellingen en -regels.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-153">This example creates a basic application gateway with default settings for hello listener, backend pool, backend http settings, and rules.</span></span> <span data-ttu-id="9fdb0-154">U kunt deze instellingen toosuit uw implementatie wijzigen wanneer Hallo inrichten voltooid is.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-154">You can modify these settings toosuit your deployment once hello provisioning is successful.</span></span>
<span data-ttu-id="9fdb0-155">Als u al uw webtoepassing gedefinieerd met behulp van back-endpool in de vorige stappen, eenmaal is gemaakt, Hallo Hallo begint taakverdeling.</span><span class="sxs-lookup"><span data-stu-id="9fdb0-155">If you already have your web application defined with hello backend pool in hello preceding steps, once created, load balancing begins.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fdb0-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9fdb0-156">Next steps</span></span>

<span data-ttu-id="9fdb0-157">Meer informatie over hoe toocreate aangepaste statuscontroles in via [een aangepaste health test maken](application-gateway-create-probe-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9fdb0-157">Learn how toocreate custom health probes by visiting [Create a custom health probe](application-gateway-create-probe-portal.md)</span></span>

<span data-ttu-id="9fdb0-158">Meer informatie over hoe tooconfigure SSL-Offloading en los het Hallo kostbare SSL ontsleuteling uitgeschakeld in uw webservers in via [SSL-Offload configureren](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="9fdb0-158">Learn how tooconfigure SSL Offloading and take hello costly SSL decryption off your web servers by visiting [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
