---
title: een toepassingsgateway met URL-routering regels - aaaCreate Azure CLI 2.0 | Microsoft Docs
description: Deze pagina vindt u instructies toocreate, een Azure-toepassingsgateway met behulp van regels voor URL-routering configureren
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
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a><span data-ttu-id="8b3ca-103">Een toepassingsgateway met pad gebaseerde routering met Azure CLI 2.0 maken</span><span class="sxs-lookup"><span data-stu-id="8b3ca-103">Create an application gateway using Path-based routing with Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b3ca-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="8b3ca-104">Azure portal</span></span>](application-gateway-create-url-route-portal.md)
> * [<span data-ttu-id="8b3ca-105">Azure Resource Manager PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b3ca-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-url-route-arm-ps.md)
> * [<span data-ttu-id="8b3ca-106">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8b3ca-106">Azure CLI 2.0</span></span>](application-gateway-create-url-route-cli.md)

<span data-ttu-id="8b3ca-107">URL-pad gebaseerde routering, kunt u tooassociate routes op basis van Hallo URL-pad van een Http-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-107">URL Path-based routing enables you tooassociate routes based on hello URL path of an Http request.</span></span> <span data-ttu-id="8b3ca-108">Het wordt gecontroleerd of er een route tooa back-end-adresgroep geconfigureerd voor Hallo-URL die zijn gepresenteerd in Hallo Application Gateway is en verzendt Hallo netwerkverkeer toohello gedefinieerd back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-108">It checks if there is a route tooa back-end pool configured for hello URL presented in hello Application Gateway and sends hello network traffic toohello defined back-end pool.</span></span> <span data-ttu-id="8b3ca-109">Vaak gebruikt voor het doorsturen van op basis van een URL is tooload van aanvragen verdelen over voor andere typen inhoud toodifferent back-end-servergroepen.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-109">A common use for URL-based routing is tooload balance requests for different content types toodifferent back-end server pools.</span></span>

<span data-ttu-id="8b3ca-110">URL gebaseerde routering introduceert een nieuwe regel type tooapplication gateway.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-110">URL-based routing introduces a new rule type tooapplication gateway.</span></span> <span data-ttu-id="8b3ca-111">Toepassingsgateway heeft twee regeltypen: basic en PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-111">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="8b3ca-112">Basic regeltype biedt round robin-service voor Hallo back-end opslaggroepen tijdens PathBasedRouting bovendien tooround robin distributie, ook rekening wordt gehouden pad patroon van de aanvraag-URL Hallo daarbij Hallo back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-112">Basic rule type provides round-robin service for hello back-end pools while PathBasedRouting in addition tooround robin distribution, also takes path pattern of hello request URL into account while choosing hello back-end pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="8b3ca-113">Scenario</span><span class="sxs-lookup"><span data-stu-id="8b3ca-113">Scenario</span></span>

<span data-ttu-id="8b3ca-114">In Hallo voorbeeld te volgen, Application Gateway verkeer voor contoso.com bedient met twee back-endserver van toepassingen: een servergroep standaard en een installatiekopie-servergroep.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-114">In hello following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: a default server pool and an image server pool.</span></span>

<span data-ttu-id="8b3ca-115">Aanvragen voor http://contoso.com/image * worden gerouteerd servergroep tooimage (imagesBackendPool), als hello komt niet overeen met het pad, een server standaardgroep (appGatewayBackendPool) is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-115">Requests for http://contoso.com/image* are routed tooimage server pool (imagesBackendPool), if hello path pattern does not match, a default server pool (appGatewayBackendPool) is selected.</span></span>

![URL-route](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a><span data-ttu-id="8b3ca-117">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="8b3ca-117">Log in tooAzure</span></span>

<span data-ttu-id="8b3ca-118">Open Hallo **Microsoft Azure-opdrachtprompt**, en zich aanmelden.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-118">Open hello **Microsoft Azure Command Prompt**, and log in.</span></span> 

```azurecli
az login -u "username"
```

> [!NOTE]
> <span data-ttu-id="8b3ca-119">U kunt ook `az login` zonder Hallo switch voor apparaat aanmelding waarvoor een code op aka.ms/devicelogin invoert.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-119">You can also use `az login` without hello switch for device login that requires entering a code at aka.ms/devicelogin.</span></span>

<span data-ttu-id="8b3ca-120">Wanneer u Hallo voorgaande voorbeeld typt, wordt een code opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-120">Once you type hello preceding example, a code is provided.</span></span> <span data-ttu-id="8b3ca-121">Navigeer toohttps://aka.ms/devicelogin in een browser toocontinue Hallo aanmeldingsproces.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-121">Navigate toohttps://aka.ms/devicelogin in a browser toocontinue hello login process.</span></span>

![cmd tonen apparaat aanmelding][1]

<span data-ttu-id="8b3ca-123">Voer in de browser Hallo Hallo-code die u hebt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-123">In hello browser, enter hello code you received.</span></span> <span data-ttu-id="8b3ca-124">U staat op de aanmeldingspagina omgeleide tooa.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-124">You are redirected tooa sign-in page.</span></span>

![browser tooenter code][2]

<span data-ttu-id="8b3ca-126">Zodra het Hallo-code is ingevoerd u bent aangemeld, sluiten Hallo browser toocontinue op met de Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-126">Once hello code has been entered you are signed in, close hello browser toocontinue on with hello scenario.</span></span>

![aangemeld][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a><span data-ttu-id="8b3ca-128">Een regel op basis van het pad tooan bestaande toepassingsgateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="8b3ca-128">Add a path-based rule tooan existing application gateway</span></span>

<span data-ttu-id="8b3ca-129">Een toepassingsgateway maken met een padregel gedefinieerd</span><span class="sxs-lookup"><span data-stu-id="8b3ca-129">Create an application gateway with a path rule defined</span></span>

### <a name="create-a-new-back-end-pool"></a><span data-ttu-id="8b3ca-130">Een nieuwe back-end-pool maken</span><span class="sxs-lookup"><span data-stu-id="8b3ca-130">Create a new back-end pool</span></span>

<span data-ttu-id="8b3ca-131">Configureren van de instelling voor application gateway **imagesBackendPool** voor Hallo taakverdeling netwerkverkeer in Hallo back-endpool.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-131">Configure application gateway setting **imagesBackendPool** for hello load-balanced network traffic in hello back-end pool.</span></span> <span data-ttu-id="8b3ca-132">In dit voorbeeld kunt u instellingen van de andere back-end-adresgroep voor de nieuwe back-end-pool Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-132">In this example, you configure different back-end pool settings for hello new back-end pool.</span></span> <span data-ttu-id="8b3ca-133">Elke back-endpool kan een eigen instelling van de back-endpool hebben.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-133">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="8b3ca-134">Back-end-HTTP-instellingen worden gebruikt door regels tooroute verkeer toohello juiste back-end-groepsleden.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-134">Backend HTTP settings are used by rules tooroute traffic toohello correct backend pool members.</span></span> <span data-ttu-id="8b3ca-135">Hiermee bepaalt u het Hallo-protocol en poort die wordt gebruikt bij het verzenden van verkeer toohello back-end-groepsleden.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-135">This determines hello protocol and port that is used when sending traffic toohello backend pool members.</span></span> <span data-ttu-id="8b3ca-136">Op basis van het cookie sessies worden ook bepaald door Hallo back-end-HTTP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-136">Cookie-based sessions are also determined by hello backend HTTP settings.</span></span>  <span data-ttu-id="8b3ca-137">Bij inschakeling sessie cookies gebaseerde affiniteit verkeer toohello verzendt dezelfde back-end als de vorige aanvragen voor elk pakket.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-137">If enabled, cookie-based session affinity sends traffic toohello same backend as previous requests for each packet.</span></span>

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a><span data-ttu-id="8b3ca-138">Maak een nieuwe front-endpoort</span><span class="sxs-lookup"><span data-stu-id="8b3ca-138">Create a new front-end port</span></span>

<span data-ttu-id="8b3ca-139">Hallo front-endpoort voor een toepassingsgateway configureren.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-139">Configure hello front-end port for an application gateway.</span></span> <span data-ttu-id="8b3ca-140">Hallo front-endpoort configuration-object wordt gebruikt door een listener toodefine wat Hallo Application Gateway luistert naar verkeer op Hallo listener-poort.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-140">hello front-end port configuration object is used by a listener toodefine what port hello Application Gateway listens for traffic on hello listener.</span></span>

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a><span data-ttu-id="8b3ca-141">Maak een nieuwe listener</span><span class="sxs-lookup"><span data-stu-id="8b3ca-141">Create a new listener</span></span>

<span data-ttu-id="8b3ca-142">Hallo-listener configureren.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-142">Configure hello listener.</span></span> <span data-ttu-id="8b3ca-143">Deze stap configureert u Hallo-listener voor Hallo openbaar IP-adres en poort gebruikt tooreceive binnenkomend netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-143">This step configures hello listener for hello public IP address and port used tooreceive incoming network traffic.</span></span> <span data-ttu-id="8b3ca-144">Hallo volgt duurt Hallo eerder geconfigureerde front-end-IP-configuratie, front-endpoort configuratie en een protocol (http of https) en Hallo listener configureert.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-144">hello following example takes hello previously configured front-end IP configuration,  front-end port configuration, and a protocol (http or https) and configures hello listener.</span></span> <span data-ttu-id="8b3ca-145">Hallo-listener luistert in dit voorbeeld tooHTTP verkeer op poort 82 van het openbare IP-adres hello, dat eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-145">In this example, hello listener listens tooHTTP traffic on port 82 on hello public IP address that was created earlier.</span></span>

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a><span data-ttu-id="8b3ca-146">Overzicht van Hallo Url-pad maken</span><span class="sxs-lookup"><span data-stu-id="8b3ca-146">Create hello Url path map</span></span>

<span data-ttu-id="8b3ca-147">URL-regel paden voor back-end-adresgroepen Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-147">Configure URL rule paths for hello back-end pools.</span></span> <span data-ttu-id="8b3ca-148">Deze stap configureert u Hallo relatieve pad dat wordt gebruikt door application gateway toodefine Hallo toewijzing tussen URL-pad en welke back-end-pool toohandle Hallo binnenkomend verkeer is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-148">This step configures hello relative path used by application gateway toodefine hello mapping between URL path and which back-end pool is assigned toohandle hello incoming traffic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b3ca-149">Elk pad moet beginnen met / en Hallo enige plaats waar een '\*' is toegestaan, Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-149">Each path must start with / and hello only place a "\*" is allowed, is at hello end.</span></span> <span data-ttu-id="8b3ca-150">Voorbeelden van geldige zijn/xyz, /xyz* of xyz / *.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-150">Valid examples are /xyz, /xyz* or /xyz/*.</span></span> <span data-ttu-id="8b3ca-151">Hallo tekenreeks ingevoerd toohello pad matcher heeft geen tekst bevatten na Hallo eerst '? ' of '#' en deze tekens zijn niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-151">hello string fed toohello path matcher does not include any text after hello first "?" or "#", and those characters are not allowed.</span></span> 

<span data-ttu-id="8b3ca-152">Hallo volgende voorbeeld maakt u één regel voor ' / installatiekopieën / * ' pad routering verkeer tooback-end 'imagesBackendPool'.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-152">hello following example creates one rule for "/images/*" path routing traffic tooback-end "imagesBackendPool."</span></span> <span data-ttu-id="8b3ca-153">Deze regel zorgt ervoor dat verkeer voor elke set van URL's gerouteerde toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-153">This rule ensures that traffic for each set of urls is routed toohello backend.</span></span> <span data-ttu-id="8b3ca-154">Bijvoorbeeld: http://adatum.com/images/figure1.jpg gaat te 'imagesBackendPool'.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-154">For example, http://adatum.com/images/figure1.jpg goes too"imagesBackendPool."</span></span> <span data-ttu-id="8b3ca-155">Als het pad Hallo komt niet overeen met de vooraf gedefinieerde padregels hello, configureert pad Hallo-kaart regelconfiguratie ook een standaard back-end-adresgroep.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-155">If hello path doesn't match any of hello pre-defined path rules, hello rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="8b3ca-156">Http://adatum.com/shoppingcart/test.html geldt bijvoorbeeld toopool1 zoals deze is gedefinieerd als de standaardgroep Hallo voor niet-overeenkomende verkeer.</span><span class="sxs-lookup"><span data-stu-id="8b3ca-156">For example, http://adatum.com/shoppingcart/test.html goes toopool1 as it is defined as hello default pool for unmatched traffic.</span></span>

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a><span data-ttu-id="8b3ca-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b3ca-157">Next steps</span></span>

<span data-ttu-id="8b3ca-158">Als u toolearn over Secure Sockets Layer (SSL)-offload wilt, Zie [een toepassingsgateway voor SSL-offload configureren](application-gateway-ssl-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8b3ca-158">If you want toolearn about Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-cli.md).</span></span>


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
