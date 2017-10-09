---
title: ondersteuning voor Azure IoT Hub MQTT aaaUnderstand | Microsoft Docs
description: Ontwikkelaars begeleiden - ondersteuning voor apparaten die verbinding maken gebruik van IoT Hub apparaat gerichte eindpunt tooan Hallo MQTT-protocol. Bevat informatie over ingebouwde ondersteuning voor protocollen MQTT in hello Azure IoT-apparaat-SDK's.
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a><span data-ttu-id="04907-104">Communiceren met uw iothub met Hallo MQTT protocol</span><span class="sxs-lookup"><span data-stu-id="04907-104">Communicate with your IoT hub using hello MQTT protocol</span></span>

<span data-ttu-id="04907-105">IoT-Hub kunt u apparaten toocommunicate met Hallo Iothub apparaat eindpunten met Hallo [protocollen MQTT v3.1.1] [ lnk-mqtt-org] -protocol op poort 8883 of protocollen MQTT v3.1.1 via WebSocket-protocol op poort 443.</span><span class="sxs-lookup"><span data-stu-id="04907-105">IoT Hub enables devices toocommunicate with hello IoT Hub device endpoints using hello [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="04907-106">IoT Hub is vereist voor alle communicatie toobe van het apparaat beveiligd met TLS/SSL (daarom IoT Hub biedt geen ondersteuning voor niet-beveiligde verbindingen via poort. 1883).</span><span class="sxs-lookup"><span data-stu-id="04907-106">IoT Hub requires all device communication toobe secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-tooiot-hub"></a><span data-ttu-id="04907-107">Verbinding maken met tooIoT Hub</span><span class="sxs-lookup"><span data-stu-id="04907-107">Connecting tooIoT Hub</span></span>

<span data-ttu-id="04907-108">Een apparaat Hallo MQTT protocol tooconnect tooan IoT-hub kunt gebruiken met behulp van Hallo-bibliotheken in Hallo [Azure IoT SDK's] [ lnk-device-sdks] of rechtstreeks via Hallo MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="04907-108">A device can use hello MQTT protocol tooconnect tooan IoT hub either by using hello libraries in hello [Azure IoT SDKs][lnk-device-sdks] or by using hello MQTT protocol directly.</span></span>

## <a name="using-hello-device-sdks"></a><span data-ttu-id="04907-109">Hallo apparaat SDK's gebruiken</span><span class="sxs-lookup"><span data-stu-id="04907-109">Using hello device SDKs</span></span>

<span data-ttu-id="04907-110">[Apparaat-SDK's] [ lnk-device-sdks] die ondersteuning Hallo MQTT protocol zijn beschikbaar voor Java, Node.js, C, C# en Python.</span><span class="sxs-lookup"><span data-stu-id="04907-110">[Device SDKs][lnk-device-sdks] that support hello MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="04907-111">Hallo apparaat-SDK's gebruiken Hallo standaard IoT Hub connection string tooestablish een verbinding tooan IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="04907-111">hello device SDKs use hello standard IoT Hub connection string tooestablish a connection tooan IoT hub.</span></span> <span data-ttu-id="04907-112">toouse hello MQTT protocol Hallo client protocol parameter moet worden ingesteld te**MQTT**.</span><span class="sxs-lookup"><span data-stu-id="04907-112">toouse hello MQTT protocol, hello client protocol parameter must be set too**MQTT**.</span></span> <span data-ttu-id="04907-113">Standaard verbinding Hallo apparaat-SKD's tooan IoT Hub met Hallo **CleanSession** vlag ingesteld te**0** en gebruik **QoS 1** voor uitwisseling van berichten met Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="04907-113">By default, hello device SDKs connect tooan IoT Hub with hello **CleanSession** flag set too**0** and use **QoS 1** for message exchange with hello IoT hub.</span></span>

<span data-ttu-id="04907-114">Wanneer een apparaat is verbonden tooan IoT-hub, bieden Hallo apparaat-SKD's methoden waarmee Hallo toosend apparaatberichten tooand berichten ontvangen van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="04907-114">When a device is connected tooan IoT hub, hello device SDKs provide methods that enable hello device toosend messages tooand receive messages from an IoT hub.</span></span>

<span data-ttu-id="04907-115">Hallo volgende tabel bevat koppelingen toocode voorbeelden voor elke taal die wordt ondersteund en geeft op Hallo parameter toouse tooestablish een verbinding tooIoT Hub met Hallo MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="04907-115">hello following table contains links toocode samples for each supported language and specifies hello parameter toouse tooestablish a connection tooIoT Hub using hello MQTT protocol.</span></span>

| <span data-ttu-id="04907-116">Taal</span><span class="sxs-lookup"><span data-stu-id="04907-116">Language</span></span> | <span data-ttu-id="04907-117">Parameter protocol</span><span class="sxs-lookup"><span data-stu-id="04907-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="04907-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="04907-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="04907-119">Azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="04907-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="04907-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="04907-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="04907-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="04907-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="04907-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="04907-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="04907-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="04907-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="04907-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="04907-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="04907-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="04907-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="04907-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="04907-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="04907-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="04907-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a><span data-ttu-id="04907-128">Migreren van een apparaat-app van AMQP tooMQTT</span><span class="sxs-lookup"><span data-stu-id="04907-128">Migrating a device app from AMQP tooMQTT</span></span>

<span data-ttu-id="04907-129">Als u van Hallo gebruikmaakt [apparaat-SKD's][lnk-device-sdks], overschakelen via AMQP vereist tooMQTT Hallo protocol parameter in de initialisatie van de client Hallo wijzigen, zoals eerder gezegd.</span><span class="sxs-lookup"><span data-stu-id="04907-129">If you are using hello [device SDKs][lnk-device-sdks], switching from using AMQP tooMQTT requires changing hello protocol parameter in hello client initialization as stated previously.</span></span>

<span data-ttu-id="04907-130">Wanneer doet, moet u ervoor dat toocheck Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="04907-130">When doing so, make sure toocheck hello following items:</span></span>

* <span data-ttu-id="04907-131">AMQP retourneert fouten voor veel voorwaarden terwijl MQTT Hallo verbinding verbreekt.</span><span class="sxs-lookup"><span data-stu-id="04907-131">AMQP returns errors for many conditions, while MQTT terminates hello connection.</span></span> <span data-ttu-id="04907-132">Als gevolg hiervan uw uitzonderingsverwerking logica mogelijk enkele wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="04907-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="04907-133">Hallo biedt geen ondersteuning voor protocollen MQTT *afwijzen* operations tijdens het ontvangen van [cloud-naar-apparaatberichten][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="04907-133">MQTT does not support hello *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="04907-134">Als uw back-endserver voor apps tooreceive een reactie van apparaattoepassing hello moet, kunt u overwegen [methoden directe][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="04907-134">If your back-end app needs tooreceive a response from hello device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-hello-mqtt-protocol-directly"></a><span data-ttu-id="04907-135">Hallo MQTT protocol direct gebruik te maken</span><span class="sxs-lookup"><span data-stu-id="04907-135">Using hello MQTT protocol directly</span></span>
<span data-ttu-id="04907-136">Als een apparaat niet kan Hallo apparaat-SDK's, kan deze toohello openbaar apparaat eindpunten met Hallo MQTT protocol op poort 8883 nog steeds verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="04907-136">If a device cannot use hello device SDKs, it can still connect toohello public device endpoints using hello MQTT protocol on port 8883.</span></span> <span data-ttu-id="04907-137">In Hallo **CONNECT** Hallo na waarden moet worden gebruikt in pakket Hallo apparaat:</span><span class="sxs-lookup"><span data-stu-id="04907-137">In hello **CONNECT** packet hello device should use hello following values:</span></span>

* <span data-ttu-id="04907-138">Voor Hallo **ClientId** veld, gebruikt u Hallo **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="04907-138">For hello **ClientId** field, use hello **deviceId**.</span></span>
* <span data-ttu-id="04907-139">Voor Hallo **gebruikersnaam** veld `{iothubhostname}/{device_id}/api-version=2016-11-14`, waarbij {iothubhostname} is Hallo volledige CName van Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="04907-139">For hello **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is hello full CName of hello IoT hub.</span></span>

    <span data-ttu-id="04907-140">Bijvoorbeeld, als hello naam van uw IoT-hub is **contoso.azure devices.net** en als de naam van uw apparaat Hallo **MyDevice01**, Hallo volledige **gebruikersnaam** veld moet bevatten `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="04907-140">For example, if hello name of your IoT hub is **contoso.azure-devices.net** and if hello name of your device is **MyDevice01**, hello full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="04907-141">Voor Hallo **wachtwoord** veld, gebruikt u een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="04907-141">For hello **Password** field, use a SAS token.</span></span> <span data-ttu-id="04907-142">Hallo-indeling van SAS-token is Hallo Hallo dezelfde als voor zowel hello HTTP- en AMQP protocollen:</span><span class="sxs-lookup"><span data-stu-id="04907-142">hello format of hello SAS token is hello same as for both hello HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="04907-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="04907-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="04907-144">Voor meer informatie over het toogenerate SAS-tokens, Zie Hallo apparaat sectie [IoT Hub met behulp van beveiligingstokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="04907-144">For more information about how toogenerate SAS tokens, see hello device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="04907-145">Bij het testen, kunt u ook hello gebruiken [apparaat explorer] [ lnk-device-explorer] hulpprogramma tooquickly genereren van een SAS-token die u kunt kopiëren en plakken in uw eigen code in:</span><span class="sxs-lookup"><span data-stu-id="04907-145">When testing, you can also use hello [device explorer][lnk-device-explorer] tool tooquickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="04907-146">Ga toohello **Management** tabblad **apparaat Explorer**.</span><span class="sxs-lookup"><span data-stu-id="04907-146">Go toohello **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="04907-147">Klik op **SAS-Token** (top rechts).</span><span class="sxs-lookup"><span data-stu-id="04907-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="04907-148">Op **SASTokenForm**, selecteert u uw apparaat in Hallo **DeviceID** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="04907-148">On **SASTokenForm**, select your device in hello **DeviceID** drop down.</span></span> <span data-ttu-id="04907-149">Stel uw **TTL**.</span><span class="sxs-lookup"><span data-stu-id="04907-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="04907-150">Klik op **genereren** toocreate uw token.</span><span class="sxs-lookup"><span data-stu-id="04907-150">Click **Generate** toocreate your token.</span></span>

     <span data-ttu-id="04907-151">Hallo SAS-token die wordt gegenereerd is deze structuur: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="04907-151">hello SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="04907-152">onderdeel van dit token toouse als Hallo Hallo **wachtwoord** veld tooconnect met behulp van protocollen MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="04907-152">hello part of this token toouse as hello **Password** field tooconnect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="04907-153">MQTT verbinding maken met en pakketten verbreken, IoT-Hub geeft een gebeurtenis op Hallo **Operations Monitoring** kanaal met aanvullende informatie waarmee u kunt tootroubleshoot verbindingsproblemen.</span><span class="sxs-lookup"><span data-stu-id="04907-153">For MQTT connect and disconnect packets, IoT Hub issues an event on hello **Operations Monitoring** channel with additional information that can help you tootroubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="04907-154">Verzenden van apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="04907-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="04907-155">Nadat u de verbinding is geslaagd, een apparaat kunt verzenden met het berichten tooIoT Hub met `devices/{device_id}/messages/events/` of `devices/{device_id}/messages/events/{property_bag}` als een **onderwerpnaam**.</span><span class="sxs-lookup"><span data-stu-id="04907-155">After making a successful connection, a device can send messages tooIoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="04907-156">Hallo `{property_bag}` element kunt Hallo apparaat toosend berichten met aanvullende eigenschappen in een url-notatie.</span><span class="sxs-lookup"><span data-stu-id="04907-156">hello `{property_bag}` element enables hello device toosend messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="04907-157">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04907-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="04907-158">Dit `{property_bag}` element gebruikt Hallo dezelfde codering voor queryreeksen in Hallo HTTP-protocol.</span><span class="sxs-lookup"><span data-stu-id="04907-158">This `{property_bag}` element uses hello same encoding as for query strings in hello HTTP protocol.</span></span>
>
>

<span data-ttu-id="04907-159">Hallo apparaattoepassing kunt `devices/{device_id}/messages/events/{property_bag}` als Hallo **wordt de naam van onderwerp** toodefine *berichten wordt* toobe doorgestuurd als een bericht telemetrie.</span><span class="sxs-lookup"><span data-stu-id="04907-159">hello device app can also use `devices/{device_id}/messages/events/{property_bag}` as hello **Will topic name** toodefine *Will messages* toobe forwarded as a telemetry message.</span></span>

- <span data-ttu-id="04907-160">IoT Hub biedt geen ondersteuning voor QoS-2-berichten.</span><span class="sxs-lookup"><span data-stu-id="04907-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="04907-161">Als een apparaat-app een bericht met publiceert **QoS 2**, IoT-Hub Hallo netwerkverbinding wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="04907-161">If a device app publishes a message with **QoS 2**, IoT Hub closes hello network connection.</span></span>
- <span data-ttu-id="04907-162">IoT Hub behouden berichten niet bewaard is gebleven.</span><span class="sxs-lookup"><span data-stu-id="04907-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="04907-163">Als een apparaat een bericht met Hallo verzendt **behouden** vlag ingesteld too1, IoT-Hub toegevoegd Hallo **x-opt-behouden** toepassingsbericht eigenschap toohello.</span><span class="sxs-lookup"><span data-stu-id="04907-163">If a device sends a message with hello **RETAIN** flag set too1, IoT Hub adds hello **x-opt-retain** application property toohello message.</span></span> <span data-ttu-id="04907-164">In dit geval wordt in plaats van de persistente Hallo behouden bericht, IoT-Hub wordt doorgegeven toohello back-end-app.</span><span class="sxs-lookup"><span data-stu-id="04907-164">In this case, instead of persisting hello retain message, IoT Hub passes it toohello backend app.</span></span>
- <span data-ttu-id="04907-165">IoT Hub ondersteunt slechts één actieve MQTT verbinding per apparaat.</span><span class="sxs-lookup"><span data-stu-id="04907-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="04907-166">Alle nieuwe MQTT verbinding namens Hallo dezelfde apparaat-ID wordt IoT Hub toodrop Hallo bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="04907-166">Any new MQTT connection on behalf of hello same device ID causes IoT Hub toodrop hello existing connection.</span></span>

<span data-ttu-id="04907-167">Zie voor meer informatie [Messaging-handleiding voor ontwikkelaars][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="04907-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="04907-168">Cloud-naar-apparaat-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="04907-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="04907-169">tooreceive berichten uit IoT Hub, een apparaat moet zich abonneren met `devices/{device_id}/messages/devicebound/#` als een **onderwerp Filter**.</span><span class="sxs-lookup"><span data-stu-id="04907-169">tooreceive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="04907-170">Hallo met meerdere niveaus jokertekens  **#**  in Hallo onderwerp Filter alleen tooallow apparaat tooreceive aanvullende eigenschappen in de onderwerpnaam Hallo Hallo wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="04907-170">hello multi-level wildcard **#** in hello Topic Filter is used only tooallow hello device tooreceive additional properties in hello topic name.</span></span> <span data-ttu-id="04907-171">IoT Hub kan geen gebruik van Hallo Hallo  **#**  of **?**</span><span class="sxs-lookup"><span data-stu-id="04907-171">IoT Hub does not allow hello usage of hello **#** or **?**</span></span> <span data-ttu-id="04907-172">jokertekens voor het filteren van de onderliggende onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="04907-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="04907-173">Omdat in IoT Hub is niet algemeen pub sub messaging broker, ondersteunt deze alleen onderwerpnamen Hallo gedocumenteerd en onderwerp filters.</span><span class="sxs-lookup"><span data-stu-id="04907-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports hello documented topic names and topic filters.</span></span>

<span data-ttu-id="04907-174">Hallo apparaat ontvangt geen berichten uit IoT Hub, totdat deze is geabonneerd tooits apparaatspecifieke eindpunt, vertegenwoordigd door Hallo `devices/{device_id}/messages/devicebound/#` onderwerp filter.</span><span class="sxs-lookup"><span data-stu-id="04907-174">hello device does not receive any messages from IoT Hub, until it has successfully subscribed tooits device-specific endpoint, represented by hello `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="04907-175">Nadat een geslaagde abonnement is ingesteld, begint Hallo apparaat alleen cloud-naar-apparaat-berichten dat is verzonden tooit na Hallo Hallo abonnement ontvangen.</span><span class="sxs-lookup"><span data-stu-id="04907-175">After successful subscription has been established, hello device starts receiving only cloud-to-device messages that have been sent tooit after hello time of hello subscription.</span></span> <span data-ttu-id="04907-176">Als het Hallo-apparaat verbinding maakt met **CleanSession** vlag ingesteld te**0**, Hallo abonnement over de verschillende sessies worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="04907-176">If hello device connects with **CleanSession** flag set too**0**, hello subscription is persisted across different sessions.</span></span> <span data-ttu-id="04907-177">In dit geval Hallo volgende keer dat deze verbinding met maakt **CleanSession 0** Hallo apparaat ontvangt openstaande berichten die zijn verzonden tooit terwijl er verbinding is verbroken.</span><span class="sxs-lookup"><span data-stu-id="04907-177">In this case, hello next time it connects with **CleanSession 0** hello device receives outstanding messages that have been sent tooit while it was disconnected.</span></span> <span data-ttu-id="04907-178">Als het Hallo-apparaat gebruikt **CleanSession** vlag ingesteld te**1** echter deze niet ontvangt berichten uit IoT Hub totdat ze tooits apparaat-eindpunt onderschrijft.</span><span class="sxs-lookup"><span data-stu-id="04907-178">If hello device uses **CleanSession** flag set too**1** though, it does not receive any messages from IoT Hub until it subscribes tooits device-endpoint.</span></span>

<span data-ttu-id="04907-179">IoT Hub berichten met Hallo levert **onderwerpnaam** `devices/{device_id}/messages/devicebound/`, of `devices/{device_id}/messages/devicebound/{property_bag}` als er een berichteigenschappen.</span><span class="sxs-lookup"><span data-stu-id="04907-179">IoT Hub delivers messages with hello **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="04907-180">`{property_bag}`url-codering sleutel-waardeparen van berichteigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="04907-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="04907-181">Alleen de toepassingseigenschappen en de gebruiker instelbare eigenschappen (zoals **messageId** of **correlationId**) zijn opgenomen in de eigenschappenverzameling Hallo.</span><span class="sxs-lookup"><span data-stu-id="04907-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in hello property bag.</span></span> <span data-ttu-id="04907-182">Namen van de eigenschap System hebben Hallo voorvoegsel  **$** , toepassingseigenschappen Hallo oorspronkelijke eigenschapsnaam met geen voorvoegsel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="04907-182">System property names have hello prefix **$**, application properties use hello original property name with no prefix.</span></span>

<span data-ttu-id="04907-183">Wanneer een apparaat-app op is geabonneerd tooa onderwerp met **QoS 2**, IoT-Hub verleent maximale QoS-niveau 1 in Hallo **SUBACK** pakket.</span><span class="sxs-lookup"><span data-stu-id="04907-183">When a device app subscribes tooa topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in hello **SUBACK** packet.</span></span> <span data-ttu-id="04907-184">Daarna biedt IoT Hub berichten toohello apparaat met behulp van QoS-1.</span><span class="sxs-lookup"><span data-stu-id="04907-184">After that, IoT Hub delivers messages toohello device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="04907-185">Ophalen van de eigenschappen van een apparaat-twin</span><span class="sxs-lookup"><span data-stu-id="04907-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="04907-186">Eerst een apparaat is lid van te`$iothub/twin/res/#`, tooreceive Hallo bewerking antwoorden.</span><span class="sxs-lookup"><span data-stu-id="04907-186">First, a device subscribes too`$iothub/twin/res/#`, tooreceive hello operation's responses.</span></span> <span data-ttu-id="04907-187">Vervolgens verzendt een leeg bericht tootopic `$iothub/twin/GET/?$rid={request id}`, met de ingestelde waarde voor **aanvraag-id**. Hallo-service stuurt vervolgens een antwoordbericht met Hallo apparaat twin gegevens over onderwerp `$iothub/twin/res/{status}/?$rid={request id}`, met behulp van dezelfde Hallo  **aanvraag-id** als Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="04907-187">Then, it sends an empty message tootopic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**. hello service then sends a response message containing hello device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using hello same **request id** as hello request.</span></span>

<span data-ttu-id="04907-188">Aanvraag-id mag geldige waarde voor de waarde van een bericht eigenschap conform [messaging Ontwikkelaarshandleiding voor IoT-Hub][lnk-messaging], en de status wordt gevalideerd als een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="04907-188">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="04907-189">antwoordtekst Hallo bevat Hallo sectie met eigenschappen van Hallo apparaat twin:</span><span class="sxs-lookup"><span data-stu-id="04907-189">hello response body contains hello properties section of hello device twin:</span></span>

<span data-ttu-id="04907-190">Hallo-hoofdtekst van Hallo identiteit registervermelding beperkt toohello 'Eigenschappen' lid, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04907-190">hello body of hello identity registry entry limited toohello “properties” member, for example:</span></span>

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

<span data-ttu-id="04907-191">Hallo statuscodes zijn:</span><span class="sxs-lookup"><span data-stu-id="04907-191">hello possible status codes are:</span></span>

|<span data-ttu-id="04907-192">Status</span><span class="sxs-lookup"><span data-stu-id="04907-192">Status</span></span> | <span data-ttu-id="04907-193">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="04907-193">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="04907-194">200</span><span class="sxs-lookup"><span data-stu-id="04907-194">200</span></span> | <span data-ttu-id="04907-195">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="04907-195">Success</span></span> |
| <span data-ttu-id="04907-196">429</span><span class="sxs-lookup"><span data-stu-id="04907-196">429</span></span> | <span data-ttu-id="04907-197">Te veel aanvragen (beperkt), conform [beperking IoT-Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="04907-197">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="04907-198">5**</span><span class="sxs-lookup"><span data-stu-id="04907-198">5**</span></span> | <span data-ttu-id="04907-199">Server-fouten</span><span class="sxs-lookup"><span data-stu-id="04907-199">Server errors</span></span> |

<span data-ttu-id="04907-200">Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="04907-200">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="04907-201">Update apparaat twin gerapporteerd eigenschappen</span><span class="sxs-lookup"><span data-stu-id="04907-201">Update device twin's reported properties</span></span>

<span data-ttu-id="04907-202">Hallo hieronder wordt beschreven hoe een apparaat Hallo bijgewerkt gerapporteerd eigenschappen in Hallo apparaat twin in IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="04907-202">hello following sequence describes how a device updates hello reported properties in hello device twin in IoT Hub:</span></span>

1. <span data-ttu-id="04907-203">Een apparaat moet eerst abonneren toohello `$iothub/twin/res/#` onderwerp tooreceive Hallo van bewerking reacties uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="04907-203">A device must first subscribe toohello `$iothub/twin/res/#` topic tooreceive hello operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="04907-204">Een apparaat verzendt een bericht waarin Hallo apparaat twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` onderwerp.</span><span class="sxs-lookup"><span data-stu-id="04907-204">A device sends a message that contains hello device twin update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="04907-205">Dit bericht bevat een **aanvraag-id** waarde.</span><span class="sxs-lookup"><span data-stu-id="04907-205">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="04907-206">Hallo service en vervolgens verzendt een antwoordbericht met nieuwe ETag-waarde voor Hallo Hallo gemelde eigenschappen verzameling op onderwerp `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="04907-206">hello service then sends a response message that contains hello new ETag value for hello reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="04907-207">Dit maakt gebruik van dezelfde Hallo antwoordbericht **aanvraag-id** als Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="04907-207">This response message uses hello same **request id** as hello request.</span></span>

<span data-ttu-id="04907-208">Hallo-bericht aanvraagtekst bevat een JSON-document, wat zorgt voor nieuwe waarden voor de gerapporteerde eigenschappen (geen andere eigenschap of metagegevens kan worden aangepast).</span><span class="sxs-lookup"><span data-stu-id="04907-208">hello request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="04907-209">Elk lid in de JSON-document Hallo updates of Hallo overeenkomend lid in Hallo apparaat twin document toevoegen.</span><span class="sxs-lookup"><span data-stu-id="04907-209">Each member in hello JSON document updates or add hello corresponding member in hello device twin’s document.</span></span> <span data-ttu-id="04907-210">Een ledenset te`null`, verwijderingen Hallo lid van Hallo dat object bevat.</span><span class="sxs-lookup"><span data-stu-id="04907-210">A member set too`null`, deletes hello member from hello containing object.</span></span> <span data-ttu-id="04907-211">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04907-211">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="04907-212">Hallo statuscodes zijn:</span><span class="sxs-lookup"><span data-stu-id="04907-212">hello possible status codes are:</span></span>

|<span data-ttu-id="04907-213">Status</span><span class="sxs-lookup"><span data-stu-id="04907-213">Status</span></span> | <span data-ttu-id="04907-214">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="04907-214">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="04907-215">200</span><span class="sxs-lookup"><span data-stu-id="04907-215">200</span></span> | <span data-ttu-id="04907-216">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="04907-216">Success</span></span> |
| <span data-ttu-id="04907-217">400</span><span class="sxs-lookup"><span data-stu-id="04907-217">400</span></span> | <span data-ttu-id="04907-218">Ongeldige aanvraag.</span><span class="sxs-lookup"><span data-stu-id="04907-218">Bad Request.</span></span> <span data-ttu-id="04907-219">Ongeldige JSON</span><span class="sxs-lookup"><span data-stu-id="04907-219">Malformed JSON</span></span> |
| <span data-ttu-id="04907-220">429</span><span class="sxs-lookup"><span data-stu-id="04907-220">429</span></span> | <span data-ttu-id="04907-221">Te veel aanvragen (beperkt), conform [beperking IoT-Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="04907-221">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="04907-222">5**</span><span class="sxs-lookup"><span data-stu-id="04907-222">5**</span></span> | <span data-ttu-id="04907-223">Server-fouten</span><span class="sxs-lookup"><span data-stu-id="04907-223">Server errors</span></span> |

<span data-ttu-id="04907-224">Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="04907-224">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="04907-225">Ontvangende gewenste eigenschappen updatemeldingen</span><span class="sxs-lookup"><span data-stu-id="04907-225">Receiving desired properties update notifications</span></span>

<span data-ttu-id="04907-226">Wanneer een apparaat is verbonden, IoT Hub verzendt meldingen toohello onderwerp `$iothub/twin/PATCH/properties/desired/?$version={new version}`, die inhoud Hallo Hallo update uitgevoerd door Hallo back-end oplossing bevatten.</span><span class="sxs-lookup"><span data-stu-id="04907-226">When a device is connected, IoT Hub sends notifications toohello topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain hello content of hello update performed by hello solution back end.</span></span> <span data-ttu-id="04907-227">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="04907-227">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="04907-228">Als voor updates voor de eigenschap `null` waarden betekent dat Hallo JSON-object lid wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="04907-228">As for property updates, `null` values means that hello JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="04907-229">IoT Hub genereert wijzigingsmeldingen alleen wanneer apparaten zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="04907-229">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="04907-230">Zorg ervoor dat tooimplement hello [apparaat opnieuw verbinden stroom] [ lnk-devguide-twin-reconnection] tookeep Hallo gewenst eigenschappen tussen IoT Hub en Hallo apparaattoepassing gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="04907-230">Make sure tooimplement hello [device reconnection flow][lnk-devguide-twin-reconnection] tookeep hello desired properties synchronized between IoT Hub and hello device app.</span></span>

<span data-ttu-id="04907-231">Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="04907-231">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-tooa-direct-method"></a><span data-ttu-id="04907-232">Directe methode tooa reageren</span><span class="sxs-lookup"><span data-stu-id="04907-232">Respond tooa direct method</span></span>

<span data-ttu-id="04907-233">Eerst een apparaat toosubscribe te heeft`$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="04907-233">First, a device has toosubscribe too`$iothub/methods/POST/#`.</span></span> <span data-ttu-id="04907-234">IoT Hub verzendt methode aanvragen toohello onderwerp `$iothub/methods/POST/{method name}/?$rid={request id}`, met een geldige JSON of een lege hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="04907-234">IoT Hub sends method requests toohello topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="04907-235">toorespond, Hallo apparaat verzendt een bericht met een geldige JSON of een lege hoofdtekst toohello onderwerp `$iothub/methods/res/{status}/?$rid={request id}`, waarbij **aanvraag-id** heeft toomatch Hallo in aanvraag het Hallo-bericht, en **status** toobe is een geheel getal .</span><span class="sxs-lookup"><span data-stu-id="04907-235">toorespond, hello device sends a message with a valid JSON or empty body toohello topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has toomatch hello one in hello request message, and **status** has toobe an integer.</span></span>

<span data-ttu-id="04907-236">Zie voor meer informatie [directe methode Ontwikkelaarshandleiding voor][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="04907-236">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="04907-237">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="04907-237">Additional considerations</span></span>

<span data-ttu-id="04907-238">Als een definitieve overweging als u nodig hebt toocustomize hello MQTT protocol gedrag Hallo cloud-zijde, moet u nagaan Hallo [protocolgateway van Azure IOT] [ lnk-azure-protocol-gateway] waarmee u toodeploy hoge prestaties aangepaste protocol-gateway die rechtstreeks met IoT Hub-interfaces.</span><span class="sxs-lookup"><span data-stu-id="04907-238">As a final consideration, if you need toocustomize hello MQTT protocol behavior on hello cloud side, you should review hello [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you toodeploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="04907-239">Hello Azure IoT-protocolgateway kunt u toocustomize Hallo apparaat protocol tooaccommodate brownfield MQTT implementaties of andere aangepaste protocollen.</span><span class="sxs-lookup"><span data-stu-id="04907-239">hello Azure IoT protocol gateway enables you toocustomize hello device protocol tooaccommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="04907-240">Deze aanpak is echter vereist die u uitvoert en een aangepaste protocol-gateway werkt.</span><span class="sxs-lookup"><span data-stu-id="04907-240">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04907-241">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="04907-241">Next steps</span></span>

<span data-ttu-id="04907-242">toolearn meer informatie over het protocol van de protocollen MQTT hello, Zie Hallo [MQTT documentatie][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="04907-242">toolearn more about hello MQTT protocol, see hello [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="04907-243">toolearn meer informatie over het plannen van de implementatie van uw IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="04907-243">toolearn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="04907-244">[Azure gecertificeerd voor de catalogus van IoT-apparaat][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="04907-244">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="04907-245">[Ondersteuning voor aanvullende protocollen][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="04907-245">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="04907-246">[Vergelijken met Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="04907-246">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="04907-247">[Schalen, HA en Noodherstel][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="04907-247">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="04907-248">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="04907-248">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="04907-249">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="04907-249">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="04907-250">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="04907-250">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
