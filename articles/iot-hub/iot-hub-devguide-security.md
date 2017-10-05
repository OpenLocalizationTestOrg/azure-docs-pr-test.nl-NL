---
title: Azure IoT Hub beveiliging begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - toegang met IoT Hub voor apparaat-apps en apps van de back-end beheren. Bevat informatie over beveiligingstokens en ondersteuning voor X.509-certificaten.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e4fe5400ffcf4446392015aada031dd4dfbf238a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="3d7ad-104">Toegang tot IoT Hub regelen</span><span class="sxs-lookup"><span data-stu-id="3d7ad-104">Control access to IoT Hub</span></span>

<span data-ttu-id="3d7ad-105">In dit artikel beschrijft de opties voor het beveiligen van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="3d7ad-106">IoT Hub gebruikt *machtigingen* toegang verlenen tot elk IoT hub-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="3d7ad-107">Machtigingen beperken de toegang tot een IoT-hub die op basis van functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="3d7ad-108">Dit artikel wordt beschreven:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-108">This article describes:</span></span>

* <span data-ttu-id="3d7ad-109">De andere machtigingen die u kunt verlenen aan een apparaat of back-end-app voor toegang tot uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="3d7ad-110">Het verificatieproces en de tokens die wordt gebruikt om machtigingen te controleren.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="3d7ad-111">Het bereik van referenties om toegang tot specifieke bronnen te beperken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="3d7ad-112">IoT Hub-ondersteuning voor het X.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="3d7ad-113">Aangepast apparaat verificatiemechanismen die gebruikmaken van bestaande apparaten identiteit registers of verificatieschema's.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="3d7ad-114">Wanneer gebruikt u dit?</span><span class="sxs-lookup"><span data-stu-id="3d7ad-114">When to use</span></span>

<span data-ttu-id="3d7ad-115">U moet de juiste machtigingen voor toegang tot een van de IoT Hub-eindpunten hebben.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-115">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="3d7ad-116">Een apparaat moet bijvoorbeeld een token met beveiligingsreferenties samen met elk bericht dat naar IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-116">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="3d7ad-117">Toegangsbeheer en machtigingen</span><span class="sxs-lookup"><span data-stu-id="3d7ad-117">Access control and permissions</span></span>

<span data-ttu-id="3d7ad-118">U kunt verlenen [machtigingen](#iot-hub-permissions) in de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-118">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="3d7ad-119">**IoT hub-niveau gedeelde toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="3d7ad-120">Beleid voor gedeelde toegang kunnen verlenen tot een combinatie van [machtigingen](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="3d7ad-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="3d7ad-121">U kunt beleid in definiëren de [Azure-portal][lnk-management-portal], of programmatisch met behulp van de [resourceprovider IoT Hub REST-API's][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-121">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="3d7ad-122">Een nieuwe iothub heeft de volgende standaardbeleidsregels:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-122">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="3d7ad-123">**iothubowner**: beleid met alle machtigingen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="3d7ad-124">**service**: beleid met **ServiceConnect** machtiging.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="3d7ad-125">**apparaat**: beleid met **DeviceConnect** machtiging.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="3d7ad-126">**registryRead**: beleid met **RegistryRead** machtiging.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="3d7ad-127">**registryReadWrite**: beleid met **RegistryRead** en RegistryWrite machtigingen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="3d7ad-128">**Beveiligingsreferenties per apparaat**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-128">**Per-device security credentials**.</span></span> <span data-ttu-id="3d7ad-129">Elke IoT-Hub bevat een [identiteitsregister][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="3d7ad-130">U kunt beveiligingsreferenties op die verlenen configureren voor elk apparaat in het identiteitenregister van deze **DeviceConnect** machtigingen binnen het bereik van de bijbehorende apparaat-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="3d7ad-131">Bijvoorbeeld in een typische IoT-oplossing:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="3d7ad-132">De apparaat-management-component gebruikt de *registryReadWrite* beleid.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-132">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="3d7ad-133">De gebeurtenis processor-component gebruikt de *service* beleid.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-133">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="3d7ad-134">De component runtime-apparaat zakelijke logica gebruikt de *service* beleid.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-134">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="3d7ad-135">Afzonderlijke apparaten verbinding maken met behulp van referenties opgeslagen in het identiteitsregister van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-135">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="3d7ad-136">Zie [machtigingen](#iot-hub-permissions) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="3d7ad-137">Authentication</span><span class="sxs-lookup"><span data-stu-id="3d7ad-137">Authentication</span></span>

<span data-ttu-id="3d7ad-138">Azure IoT Hub verleent toegang tot eindpunten door te controleren of een token tegen gedeeld toegangsbeleid en identiteit register beveiligingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-138">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="3d7ad-139">Beveiligingsreferenties zoals symmetrische sleutels worden nooit verzonden via de kabel.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-139">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="3d7ad-140">De resourceprovider van Azure IoT Hub is beveiligd via uw Azure-abonnement, omdat alle providers in het [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-140">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="3d7ad-141">Zie voor meer informatie over het maken en gebruiken van beveiligingstokens [IoT Hub beveiligingstokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-141">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="3d7ad-142">Protocol-specificaties</span><span class="sxs-lookup"><span data-stu-id="3d7ad-142">Protocol specifics</span></span>

<span data-ttu-id="3d7ad-143">Elke ondersteunde protocollen, zoals MQTT AMQP en HTTP, transporten tokens op verschillende manieren.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="3d7ad-144">Wanneer u MQTT, het pakket verbinding maken met de apparaat-id heeft als de ClientId, {iothubhostname} / {deviceId} in het veld Username en een SAS-token in het veld wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-144">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="3d7ad-145">{iothubhostname} moet de volledige CName van de IoT-hub (bijvoorbeeld contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="3d7ad-145">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="3d7ad-146">Wanneer u [AMQP][lnk-amqp], IoT-Hub ondersteunt [SASL zonder opmaak] [ lnk-sasl-plain] en [AMQP Claims-beveiliging op basis van-] [ lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="3d7ad-147">Als u AMQP claims-beveiliging op basis van-gebruikt, geeft de standaard geeft aan hoe deze tokens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-147">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="3d7ad-148">Voor SASL zonder opmaak, de **gebruikersnaam** kan zijn:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-148">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="3d7ad-149">`{policyName}@sas.root.{iothubName}`Als met IoT hub-niveau tokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="3d7ad-150">`{deviceId}@sas.{iothubname}`Als het gebruik van tokens binnen het bereik van apparaat.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="3d7ad-151">In beide gevallen wordt het wachtwoordveld bevat het token, zoals beschreven in [IoT Hub beveiligingstokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-151">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="3d7ad-152">HTTP wordt de verificatie geïmplementeerd door een geldig token in de **autorisatie** aanvraag-header.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-152">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="3d7ad-153">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="3d7ad-153">Example</span></span>

<span data-ttu-id="3d7ad-154">Gebruikersnaam (DeviceId is hoofdlettergevoelig):`iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="3d7ad-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="3d7ad-155">Wachtwoord (genereren van SAS-token met de [apparaat explorer] [ lnk-device-explorer] hulpprogramma):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="3d7ad-155">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="3d7ad-156">De [Azure IoT SDK's] [ lnk-sdks] automatisch genereren van tokens bij het verbinden met de service.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-156">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="3d7ad-157">In sommige gevallen worden de Azure IoT SDK's bieden geen ondersteuning alle protocollen of de verificatiemethoden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-157">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="3d7ad-158">Speciale overwegingen voor SASL zonder opmaak</span><span class="sxs-lookup"><span data-stu-id="3d7ad-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="3d7ad-159">Als u SASL zonder opmaak met AMQP, kunt een client die verbinding met een IoT-hub-token van een enkele gebruiken voor elke TCP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-159">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="3d7ad-160">Wanneer het token is verlopen, wordt de TCP-verbinding verbroken van de service en een reconnect activeert.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-160">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="3d7ad-161">Dit gedrag, raakt terwijl niet problematisch voor een back-endserver voor apps, voor een apparaat-app voor de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-161">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="3d7ad-162">Gateways verbinding meestal namens veel apparaten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="3d7ad-163">Wanneer u SASL zonder opmaak, hebben ze een afzonderlijke TCP-verbinding voor elk apparaat verbinding maakt met een IoT-hub te maken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-163">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="3d7ad-164">Dit scenario aanzienlijk verhoogd het verbruik van kracht en netwerkresources, en de latentie van elk apparaatverbinding.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-164">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="3d7ad-165">Resource beperkte apparaten nadelig worden beïnvloed door het toegenomen gebruik van bronnen te herstellen nadat elke token is verlopen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-165">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="3d7ad-166">Bereik IoT hub-niveau referenties</span><span class="sxs-lookup"><span data-stu-id="3d7ad-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="3d7ad-167">U kunt het beveiligingsbeleid van IoT hub-niveau bereik tokens met een beperkte resource-URI te maken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="3d7ad-168">Het eindpunt op apparaat-naar-cloud-berichten verzenden van een apparaat is bijvoorbeeld **/devices/ {deviceId} / berichten/gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-168">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="3d7ad-169">U kunt ook een IoT hub-niveau gedeeld toegangsbeleid met **DeviceConnect** machtigingen voor het ondertekenen van een token waarvan resourceURI wordt **/devices/ {deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="3d7ad-170">Deze methode maakt u een token die alleen kan worden gebruikt voor het verzenden van berichten namens apparaat **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-170">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="3d7ad-171">Deze methode is vergelijkbaar met de [Event Hubs uitgeversbeleid][lnk-event-hubs-publisher-policy], en kunt u aangepaste verificatiemethoden implementeren.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-171">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="3d7ad-172">Beveiligingstokens</span><span class="sxs-lookup"><span data-stu-id="3d7ad-172">Security tokens</span></span>

<span data-ttu-id="3d7ad-173">IoT Hub gebruikt de beveiligingstokens voor verificatie van apparaten en services om te voorkomen dat sleutels op de kabel verzonden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-173">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="3d7ad-174">Bovendien zijn beveiligingstokens beperkt in geldigheid en het bereik.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="3d7ad-175">[Azure IoT SDK's] [ lnk-sdks] automatisch genereren van tokens zonder speciale configuratie.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="3d7ad-176">Sommige scenario's hoeven te genereren en beveiligingstokens rechtstreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-176">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="3d7ad-177">Dergelijke scenario's omvatten:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-177">Such scenarios include:</span></span>

* <span data-ttu-id="3d7ad-178">Het direct gebruik van het oppervlak MQTT, AMQP of HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-178">The direct use of the MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="3d7ad-179">De implementatie van het patroon token service, zoals wordt beschreven in [aangepaste apparaatverificatie][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-179">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="3d7ad-180">IoT Hub kan ook apparaten te verifiëren met IoT Hub met [X.509-certificaten][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-180">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="3d7ad-181">Security token structuur</span><span class="sxs-lookup"><span data-stu-id="3d7ad-181">Security token structure</span></span>

<span data-ttu-id="3d7ad-182">U beveiligingstokens verlenen tijd begrensd toegang tot apparaten en services met specifieke functionaliteit van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-182">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="3d7ad-183">Als u toestemming om te verbinden met IoT Hub, moeten apparaten en services de beveiligingstokens die zijn ondertekend met een gedeelde toegang of de symmetrische sleutel verzenden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-183">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="3d7ad-184">Deze sleutels worden opgeslagen met een apparaat-id in het identiteitsregister.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-184">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="3d7ad-185">Een token dat is ondertekend met een gedeelde toegang sleutel verleent toegang tot alle functies die zijn gekoppeld aan de gedeelde beleid toegangsmachtigingen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-185">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="3d7ad-186">Een token die is ondertekend met een apparaat-id symmetrische sleutel alleen verleent de **DeviceConnect** machtiging voor het gekoppelde apparaat-id.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-186">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="3d7ad-187">Het beveiligingstoken heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-187">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="3d7ad-188">Hier volgen de verwachte waarden:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-188">Here are the expected values:</span></span>

| <span data-ttu-id="3d7ad-189">Waarde</span><span class="sxs-lookup"><span data-stu-id="3d7ad-189">Value</span></span> | <span data-ttu-id="3d7ad-190">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3d7ad-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3d7ad-191">{handtekening}</span><span class="sxs-lookup"><span data-stu-id="3d7ad-191">{signature}</span></span> |<span data-ttu-id="3d7ad-192">Een tekenreeks HMAC SHA256 handtekening van het formulier: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-192">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="3d7ad-193">**Belangrijke**: de sleutel is gedecodeerd van base64 en gebruikt als sleutel voor het uitvoeren van de berekening HMAC SHA256.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-193">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="3d7ad-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="3d7ad-194">{resourceURI}</span></span> |<span data-ttu-id="3d7ad-195">De voorvoegsels van URI (door het segment) van de eindpunten die toegankelijk zijn met dit token, beginnen met de hostnaam van de IoT-hub (geen protocol).</span><span class="sxs-lookup"><span data-stu-id="3d7ad-195">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="3d7ad-196">Bijvoorbeeld: `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="3d7ad-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="3d7ad-197">{verstrijken}</span><span class="sxs-lookup"><span data-stu-id="3d7ad-197">{expiry}</span></span> |<span data-ttu-id="3d7ad-198">UTF8-tekenreeksen voor het aantal seconden sinds de epoche 00:00:00 UTC op 1 januari 1970.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-198">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="3d7ad-199">{{URL-codering-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="3d7ad-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="3d7ad-200">Lagere case URL-codering van de resource-URI van kleine letters</span><span class="sxs-lookup"><span data-stu-id="3d7ad-200">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="3d7ad-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="3d7ad-201">{policyName}</span></span> |<span data-ttu-id="3d7ad-202">De naam van het beleid voor gedeelde toegang waarnaar dit token verwijst.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-202">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="3d7ad-203">Ontbrekende als verwijst het token naar apparaatregister referenties.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-203">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="3d7ad-204">**Opmerking van het voorvoegsel**: de URI-voorvoegsel wordt berekend door het segment en niet door teken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-204">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="3d7ad-205">Bijvoorbeeld `/a/b` is een voorvoegsel voor `/a/b/c` maar niet voor `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="3d7ad-206">De volgende Node.js-fragment toont een aangeroepen functie **generateSasToken** die het token van de invoer berekent `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-206">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="3d7ad-207">De volgende secties bevatten informatie over het initialiseren van de andere invoer voor de verschillende token gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-207">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="3d7ad-208">Als een vergelijking is de equivalente Python-code voor het genereren van een beveiligingstoken:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-208">As a comparison, the equivalent Python code to generate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="3d7ad-209">Aangezien de geldigheid van het token is gevalideerd op de machines IoT Hub, is de afwijking van de klok van de computer die het token genereert moet minimaal.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-209">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="3d7ad-210">SAS-tokens gebruiken in een apparaat-app</span><span class="sxs-lookup"><span data-stu-id="3d7ad-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="3d7ad-211">Er zijn twee manieren verkrijgen **DeviceConnect** machtigingen met IoT Hub met beveiligingstokens: gebruik een [symmetrische apparaatsleutel uit het identiteitenregister](#use-a-symmetric-key-in-the-identity-registry), of gebruik een [gedeelde toegangssleutel](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="3d7ad-211">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="3d7ad-212">Houd er rekening mee dat alle functionaliteit die toegankelijk is vanaf apparaten wordt blootgesteld aan het ontwerp voor eindpunten met voorvoegsel `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d7ad-213">De enige manier om dat IoT Hub wordt geverifieerd voor een specifiek apparaat maakt gebruik van de symmetrische sleutel voor apparaat-id.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-213">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="3d7ad-214">In gevallen wanneer een beleid voor gedeelde toegang wordt gebruikt voor toegang tot de functionaliteit van apparaten, de oplossing moet rekening houden met het onderdeel voor het uitgeven van het beveiligingstoken als een vertrouwde subonderdeel.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-214">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="3d7ad-215">Het apparaat gerichte eindpunten zijn (onafhankelijk van het protocol):</span><span class="sxs-lookup"><span data-stu-id="3d7ad-215">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="3d7ad-216">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="3d7ad-216">Endpoint</span></span> | <span data-ttu-id="3d7ad-217">Functionaliteit</span><span class="sxs-lookup"><span data-stu-id="3d7ad-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="3d7ad-218">Apparaat-naar-cloud-berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="3d7ad-219">Cloud-naar-apparaat-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="3d7ad-220">Een symmetrische sleutel in het identiteitenregister gebruiken</span><span class="sxs-lookup"><span data-stu-id="3d7ad-220">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="3d7ad-221">Wanneer u een apparaat-id symmetrische sleutel voor het genereren van een token, de policyName (`skn`) element van het token wordt weggelaten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-221">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="3d7ad-222">Een token dat is gemaakt voor toegang tot alle apparaatfunctionaliteit moet bijvoorbeeld de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-222">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="3d7ad-223">resource-URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="3d7ad-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="3d7ad-224">de handtekeningsleutel: een symmetrische sleutel voor de `{device id}` identiteit</span><span class="sxs-lookup"><span data-stu-id="3d7ad-224">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="3d7ad-225">Er is geen naam van beleid</span><span class="sxs-lookup"><span data-stu-id="3d7ad-225">no policy name,</span></span>
* <span data-ttu-id="3d7ad-226">elk gewenst moment verlopen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-226">any expiration time.</span></span>

<span data-ttu-id="3d7ad-227">Een voorbeeld met behulp van de voorgaande Node.js-functie is:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-227">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="3d7ad-228">Het resultaat toegang tot alle functionaliteit voor device1 verleent, zou zijn:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-228">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="3d7ad-229">Het is mogelijk voor het genereren van een SAS-token met behulp van de .NET [apparaat explorer] [ lnk-device-explorer] hulpprogramma of de cross-platform, op basis van een knooppunt [iothub explorer] [ lnk-iothub-explorer]opdrachtregelprogramma.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-229">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="3d7ad-230">Gebruik een beleid voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="3d7ad-230">Use a shared access policy</span></span>

<span data-ttu-id="3d7ad-231">Als u een token van een gedeeld toegangsbeleid maakt, stelt de `skn` veld op de naam van het beleid.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-231">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="3d7ad-232">Dit beleid moet verlenen de **DeviceConnect** machtiging.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-232">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="3d7ad-233">De twee belangrijkste scenario's voor het gebruik van beleid voor gedeelde toegang te krijgen tot de functionaliteit voor apparaten zijn:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-233">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="3d7ad-234">[cloud protocol gateways][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="3d7ad-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="3d7ad-235">[token services] [ lnk-custom-auth] gebruikt voor het implementeren van aangepaste verificatieschema's.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-235">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="3d7ad-236">Omdat het beleid voor gedeelde toegang mogelijk toegang verlenen kunt tot verbinden als een apparaat, is het belangrijk dat u de juiste bron-URI bij het maken van beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-236">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="3d7ad-237">Deze instelling is vooral belangrijk voor token-services, die als bereik voor de token voor een specifiek apparaat met behulp van de bron-URI.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-237">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="3d7ad-238">Dit punt is minder relevant voor gateways protocol zoals ze zijn verkeer voor alle apparaten al op de volgende manier regelt.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="3d7ad-239">Als u bijvoorbeeld een token service met de vooraf gemaakte gedeeld toegangsbeleid aangeroepen **apparaat** zou maken van een token met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-239">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="3d7ad-240">resource-URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="3d7ad-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="3d7ad-241">de handtekeningsleutel: een van de sleutels van de `device` -beleid</span><span class="sxs-lookup"><span data-stu-id="3d7ad-241">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="3d7ad-242">de naam van beleid: `device`,</span><span class="sxs-lookup"><span data-stu-id="3d7ad-242">policy name: `device`,</span></span>
* <span data-ttu-id="3d7ad-243">elk gewenst moment verlopen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-243">any expiration time.</span></span>

<span data-ttu-id="3d7ad-244">Een voorbeeld met behulp van de voorgaande Node.js-functie is:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-244">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="3d7ad-245">Het resultaat toegang tot alle functionaliteit voor device1 verleent, zou zijn:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-245">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="3d7ad-246">Een protocolgateway hetzelfde token kan gebruiken voor alle apparaten eenvoudigweg de bron-URI te `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-246">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="3d7ad-247">Gebruik de beveiligingstokens van de onderdelen van service</span><span class="sxs-lookup"><span data-stu-id="3d7ad-247">Use security tokens from service components</span></span>

<span data-ttu-id="3d7ad-248">Serviceonderdelen kunnen alleen beveiligingstokens die werken met beleid voor gedeelde toegang tot de juiste machtigingen verlenen zoals hierboven is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-248">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="3d7ad-249">Dit is de servicefuncties beschikbaar op de eindpunten zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-249">Here is the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="3d7ad-250">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="3d7ad-250">Endpoint</span></span> | <span data-ttu-id="3d7ad-251">Functionaliteit</span><span class="sxs-lookup"><span data-stu-id="3d7ad-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="3d7ad-252">Maken, bijwerken, ophalen en verwijderen van apparaat-id's.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="3d7ad-253">Apparaat-naar-cloud-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="3d7ad-254">Feedback voor cloud-naar-apparaat-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="3d7ad-255">Cloud-naar-apparaat-berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="3d7ad-256">Als u bijvoorbeeld een service genereren met behulp van de vooraf gemaakte gedeeld toegangsbeleid aangeroepen **registryRead** zou maken van een token met de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-256">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="3d7ad-257">resource-URI: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="3d7ad-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="3d7ad-258">de handtekeningsleutel: een van de sleutels van de `registryRead` -beleid</span><span class="sxs-lookup"><span data-stu-id="3d7ad-258">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="3d7ad-259">de naam van beleid: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="3d7ad-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="3d7ad-260">elk gewenst moment verlopen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="3d7ad-261">Het resultaat toegang tot het lezen van alle apparaat-id's verlenen wilt, zou zijn:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-261">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="3d7ad-262">Ondersteunde X.509-certificaten</span><span class="sxs-lookup"><span data-stu-id="3d7ad-262">Supported X.509 certificates</span></span>

<span data-ttu-id="3d7ad-263">U kunt een X.509-certificaat gebruiken voor verificatie van een apparaat met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-263">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="3d7ad-264">Certificaten zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-264">Certificates include:</span></span>

* <span data-ttu-id="3d7ad-265">**Een bestaand X.509-certificaat**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="3d7ad-266">Een apparaat mogelijk al een X.509-certificaat dat is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="3d7ad-267">Het apparaat kan dit certificaat gebruiken om te verifiëren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-267">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="3d7ad-268">**Een automatisch gegenereerd en zelfondertekend certificaat X-509**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="3d7ad-269">Een fabrikant of interne-implementatie van deze certificaten genereren en de bijbehorende persoonlijke sleutel (en het certificaat) opslaan op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-269">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="3d7ad-270">U kunt hulpprogramma's gebruiken zoals [OpenSSL] [ lnk-openssl] en [Windows SelfSignedCertificate] [ lnk-selfsigned] hulpprogramma voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="3d7ad-271">**X.509-certificaat voor ondertekening van CA**.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="3d7ad-272">Als u wilt een apparaat te identificeren en deze kan worden geverifieerd met IoT Hub, kunt u een X.509-certificaat gegenereerd en ondertekend door een certificeringsinstantie (CA).</span><span class="sxs-lookup"><span data-stu-id="3d7ad-272">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="3d7ad-273">IoT Hub controleert alleen of de geconfigureerde vingerafdruk komt overeen met de vingerafdruk van het weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-273">IoT Hub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="3d7ad-274">IotHub biedt de certificaatketen niet valideren.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-274">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="3d7ad-275">Een apparaat kan gebruikmaken van een X.509-certificaat of een beveiligingstoken voor verificatie, maar niet beide.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="3d7ad-276">Een X.509-certificaat voor een apparaat registreren</span><span class="sxs-lookup"><span data-stu-id="3d7ad-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="3d7ad-277">De [Azure IoT Service SDK voor C#] [ lnk-service-sdk] (versie 1.0.8+) biedt ondersteuning voor het registreren van een apparaat dat gebruikmaakt van een X.509-certificaat voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-277">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="3d7ad-278">Andere API's zoals importeren/exporteren van apparaten bieden ook ondersteuning voor X.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="3d7ad-279">C\# ondersteuning</span><span class="sxs-lookup"><span data-stu-id="3d7ad-279">C\# Support</span></span>

<span data-ttu-id="3d7ad-280">De **RegistryManager** klasse biedt een programmatische manier kunt u een apparaat registreren.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-280">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="3d7ad-281">In het bijzonder de **AddDeviceAsync** en **UpdateDeviceAsync** methoden kunnen u registreren en bijwerken van een apparaat in de id-register van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-281">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="3d7ad-282">Deze twee methoden maken gebruik van een **apparaat** exemplaar als invoer.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="3d7ad-283">De **apparaat** klasse bevat een **verificatie** eigenschap waarmee u primaire en secundaire x.509-certificaatvingerafdrukken opgeven.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-283">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="3d7ad-284">De vingerafdruk van het vertegenwoordigt een SHA-1-hash van het X.509-certificaat (met behulp van binaire codering DER opgeslagen).</span><span class="sxs-lookup"><span data-stu-id="3d7ad-284">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="3d7ad-285">U hebt de optie voor het opgeven van de vingerafdruk van een primaire of een secundaire vingerafdruk of beide.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-285">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="3d7ad-286">Primaire en secundaire vingerafdrukken worden ondersteund voor het afhandelen van certificaat rollover-scenario's.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-286">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="3d7ad-287">IoT Hub geen vereist of het hele X.509-certificaat, alleen de vingerafdruk van het opslaan.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-287">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="3d7ad-288">Hier volgt een voorbeeld van C\# codefragment kunt u een apparaat met een X.509-certificaat registreren:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-288">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="3d7ad-289">Gebruik van een X.509-certificaat tijdens runtime-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="3d7ad-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="3d7ad-290">De [Azure IoT-device SDK voor .NET] [ lnk-client-sdk] (versie 1.0.11+) ondersteunt het gebruik van X.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-290">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="3d7ad-291">C\# ondersteuning</span><span class="sxs-lookup"><span data-stu-id="3d7ad-291">C\# Support</span></span>

<span data-ttu-id="3d7ad-292">De klasse **DeviceAuthenticationWithX509Certificate** ondersteunt het maken van **DeviceClient** exemplaren met behulp van een X.509-certificaat.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-292">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="3d7ad-293">Het X.509-certificaat moet zich in de indeling PFX (ook wel PKCS #12) dat de persoonlijke sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-293">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="3d7ad-294">Hier volgt een voorbeeld-codefragment:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="3d7ad-295">Verificatie van aangepast apparaat</span><span class="sxs-lookup"><span data-stu-id="3d7ad-295">Custom device authentication</span></span>

<span data-ttu-id="3d7ad-296">U kunt de IoT-Hub [identiteitsregister] [ lnk-identity-registry] beveiligingsreferenties per apparaat configureren en toegang beheren met [tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-296">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="3d7ad-297">Als een IoT-oplossing al een aangepaste identiteit register en/of de verificatie-schema heeft, kunt u een *token service* deze infrastructuur integreren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="3d7ad-298">Op deze manier kunt u andere IoT-functies in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="3d7ad-299">Een service voor beveiligingstokens is een aangepaste cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="3d7ad-300">Dit maakt gebruik van een IoT-Hub *gedeeld toegangsbeleid* met **DeviceConnect** machtigingen voor het maken *binnen het bereik van apparaat* tokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="3d7ad-301">Deze tokens inschakelen voor een apparaat verbinding maakt met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-301">These tokens enable a device to connect to your IoT hub.</span></span>

![Stappen van de service voor beveiligingstokens patroon][img-tokenservice]

<span data-ttu-id="3d7ad-303">Hier volgen de belangrijkste stappen van de service voor beveiligingstokens patroon:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-303">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="3d7ad-304">Maken van een Iothub gedeeld toegangsbeleid met **DeviceConnect** machtigingen voor uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="3d7ad-305">Kunt u dit beleid in de [Azure-portal] [ lnk-management-portal] of via een programma.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-305">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="3d7ad-306">De Tokenservice die gebruikmaakt van dit beleid voor het ondertekenen van de tokens die wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-306">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="3d7ad-307">Wanneer een apparaat voor toegang tot uw IoT-hub, wordt het token van een ondertekende aanvraagt van uw service voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-307">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="3d7ad-308">Het apparaat kunt verifiëren met uw aangepaste identiteit register/verificatieschema om te bepalen van de identiteit van het apparaat dat de token service gebruikt voor het maken van het token.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-308">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="3d7ad-309">De token-service retourneert een token.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-309">The token service returns a token.</span></span> <span data-ttu-id="3d7ad-310">Het token wordt gemaakt met behulp van `/devices/{deviceId}` als `resourceURI`, met `deviceId` als het apparaat wordt geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-310">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="3d7ad-311">De token service gebruikt het beleid voor gedeelde toegang voor het maken van het token.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-311">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="3d7ad-312">Het apparaat gebruikt het token rechtstreeks met de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-312">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3d7ad-313">U kunt de .NET-klasse [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] of de Java-klasse [IotHubServiceSasToken] [ lnk-java-sas] voor het maken van een token in uw service voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-313">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="3d7ad-314">De token-service kan het verlopen van het token naar wens ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-314">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="3d7ad-315">Wanneer het token is verlopen, servers de iothub de apparaatverbinding.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-315">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="3d7ad-316">Het apparaat moet vervolgens een nieuw token aanvragen van de service voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-316">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="3d7ad-317">Een korte verlooptijd verhoogt de belasting van het apparaat en de service voor beveiligingstokens.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-317">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="3d7ad-318">Voor een apparaat verbinding maken met uw hub, moet u nog steeds deze toevoegen aan de id-register van IoT Hub, zelfs als het apparaat gebruikmaakt van een token en niet de apparaatsleutel van een verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-318">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="3d7ad-319">Daarom kunt u blijven gebruiken per apparaat toegangsbeheer door in- of uitschakelen van apparaat-id's in de [identiteitsregister][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-319">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="3d7ad-320">Deze benadering vermindert het risico van het gebruik van tokens met lange verstrijken tijden.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-320">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="3d7ad-321">Vergelijking met een aangepaste gateway</span><span class="sxs-lookup"><span data-stu-id="3d7ad-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="3d7ad-322">Het patroon van de service voor beveiligingstokens is de aanbevolen manier voor het implementeren van een aangepaste identiteit register/verificatieschema met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-322">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="3d7ad-323">Dit patroon wordt aanbevolen omdat IoT Hub blijft het grootste gedeelte van het verkeer van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-323">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="3d7ad-324">Echter, als de aangepaste verificatieschema dus met het protocol verweven is, hebt u mogelijk nodig een *aangepaste gateway* alle verkeer verwerken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-324">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="3d7ad-325">Het gebruik van een voorbeeld van een dergelijk scenario[Transport Layer Security (TLS) en vooraf gedeelde sleutels (PSKs)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="3d7ad-326">Zie voor meer informatie de [protocolgateway] [ lnk-protocols] onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-326">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="3d7ad-327">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-327">Reference topics:</span></span>

<span data-ttu-id="3d7ad-328">De volgende onderwerpen met naslaginformatie bieden u meer informatie over het beheren van toegang tot uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-328">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="3d7ad-329">Machtigingen van de IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="3d7ad-329">IoT Hub permissions</span></span>

<span data-ttu-id="3d7ad-330">De volgende tabel bevat de machtigingen die u kunt toegang tot uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-330">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="3d7ad-331">Machtiging</span><span class="sxs-lookup"><span data-stu-id="3d7ad-331">Permission</span></span> | <span data-ttu-id="3d7ad-332">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3d7ad-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="3d7ad-333">**RegistryRead**</span><span class="sxs-lookup"><span data-stu-id="3d7ad-333">**RegistryRead**</span></span> |<span data-ttu-id="3d7ad-334">Verleent leestoegang tot het identiteitsregister.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-334">Grants read access to the identity registry.</span></span> <span data-ttu-id="3d7ad-335">Zie voor meer informatie [identiteitsregister][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="3d7ad-336">Deze machtiging wordt gebruikt door de back-end-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="3d7ad-337">**RegistryReadWrite**</span><span class="sxs-lookup"><span data-stu-id="3d7ad-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="3d7ad-338">Verleent lezen en schrijven in het identiteitsregister.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-338">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="3d7ad-339">Zie voor meer informatie [identiteitsregister][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="3d7ad-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="3d7ad-340">Deze machtiging wordt gebruikt door de back-end-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="3d7ad-341">**ServiceConnect**</span><span class="sxs-lookup"><span data-stu-id="3d7ad-341">**ServiceConnect**</span></span> |<span data-ttu-id="3d7ad-342">Verleent toegang tot de cloud service gerichte communicatie en controle-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-342">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="3d7ad-343">Geeft het recht op apparaat-naar-cloud-berichten ontvangen berichten van cloud naar apparaat verzenden en het ophalen van de bijbehorende levering bevestigingen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-343">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="3d7ad-344">Verleent toestemming voor het ophalen van de levering van bevestigingen voor het bestand uploadt.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-344">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="3d7ad-345">Verleent toestemming voor toegang tot apparaat horende bijwerken tags en gewenste eigenschappen, gemelde eigenschappen ophalen en uitvoeren van query's.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-345">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="3d7ad-346">Deze machtiging wordt gebruikt door de back-end-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="3d7ad-347">**DeviceConnect**</span><span class="sxs-lookup"><span data-stu-id="3d7ad-347">**DeviceConnect**</span></span> |<span data-ttu-id="3d7ad-348">Verleent toegang tot apparaat gerichte eindpunten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-348">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="3d7ad-349">Verleent toestemming voor apparaat-naar-cloud-berichten verzenden en ontvangen berichten van de cloud-naar-apparaat.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-349">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="3d7ad-350">Verleent toestemming voor het uploaden van het bestand uitvoeren vanaf een apparaat.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-350">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="3d7ad-351">Geeft het recht apparaat twin gewenst eigenschap meldingen ontvangen en bijwerken van apparaat twin gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-351">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="3d7ad-352">Verleent toestemming voor het uitvoeren van bestand uploadt.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-352">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="3d7ad-353">Deze machtiging wordt gebruikt door apparaten.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="3d7ad-354">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="3d7ad-354">Additional reference material</span></span>

<span data-ttu-id="3d7ad-355">Er zijn andere onderwerpen waarnaar wordt verwezen in de IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-355">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="3d7ad-356">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft de verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-356">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="3d7ad-357">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijving van de quota en beperking gedrag die betrekking hebben op de service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-357">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="3d7ad-358">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] geeft een lijst van de verschillende SDK's kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub-taal.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-358">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="3d7ad-359">[IoT Hub-querytaal] [ lnk-query] beschrijft de querytaal kunt u gegevens ophalen uit IoT Hub over uw apparaat horende en taken.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-359">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="3d7ad-360">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor het MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="3d7ad-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d7ad-361">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d7ad-361">Next steps</span></span>

<span data-ttu-id="3d7ad-362">Nu u hebt geleerd hoe toegangsbeheer IoT Hub, kunt u mogelijk geïnteresseerd in de volgende onderwerpen van IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-362">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="3d7ad-363">[Horende apparaten gebruiken om de status en configuraties te synchroniseren][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="3d7ad-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="3d7ad-364">[Een directe methode aangeroepen voor een apparaat][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="3d7ad-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="3d7ad-365">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="3d7ad-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="3d7ad-366">Als u wilt uitproberen enkele concepten die in dit artikel wordt beschreven, kunt u mogelijk geïnteresseerd in de volgende zelfstudies met IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="3d7ad-366">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="3d7ad-367">[Aan de slag met Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="3d7ad-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="3d7ad-368">[Het verzenden van berichten van de cloud-naar-apparaat met IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="3d7ad-368">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="3d7ad-369">[IoT Hub apparaat-naar-cloud-berichten verwerken][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="3d7ad-369">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
