---
title: Ondersteuning voor Azure IoT Hub MQTT begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - ondersteuning voor apparaten die verbinding maken met een IoT Hub apparaat gerichte eindpunt met behulp van de protocollen MQTT-protocol. Bevat informatie over ingebouwde MQTT ondersteuning op het apparaat van de Azure IoT SDK's.
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
ms.openlocfilehash: eab70c1aa9c49a137c2ac1012449d57915fb0d27
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="communicate-with-your-iot-hub-using-the-mqtt-protocol"></a><span data-ttu-id="33cf2-104">Communiceren met uw iothub met behulp van de protocollen MQTT-protocol</span><span class="sxs-lookup"><span data-stu-id="33cf2-104">Communicate with your IoT hub using the MQTT protocol</span></span>

<span data-ttu-id="33cf2-105">IoT-Hub kunt u apparaten om te communiceren met de IoT Hub apparaat-eindpunten met behulp van de [protocollen MQTT v3.1.1] [ lnk-mqtt-org] -protocol op poort 8883 of protocollen MQTT v3.1.1 via WebSocket-protocol op poort 443.</span><span class="sxs-lookup"><span data-stu-id="33cf2-105">IoT Hub enables devices to communicate with the IoT Hub device endpoints using the [MQTT v3.1.1][lnk-mqtt-org] protocol on port 8883 or MQTT v3.1.1 over WebSocket protocol on port 443.</span></span> <span data-ttu-id="33cf2-106">IoT Hub is vereist voor alle communicatie moet worden beveiligd met behulp van TLS/SSL (daarom IoT Hub biedt geen ondersteuning voor niet-beveiligde verbindingen via poort. 1883).</span><span class="sxs-lookup"><span data-stu-id="33cf2-106">IoT Hub requires all device communication to be secured using TLS/SSL (hence, IoT Hub doesn’t support non-secure connections over port 1883).</span></span>

## <a name="connecting-to-iot-hub"></a><span data-ttu-id="33cf2-107">Verbinden met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="33cf2-107">Connecting to IoT Hub</span></span>

<span data-ttu-id="33cf2-108">Een apparaat kan de protocollen MQTT-protocol gebruiken verbinding maken met een IoT-hub die via de bibliotheken in de [Azure IoT SDK's] [ lnk-device-sdks] of door de protocollen MQTT protocol rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="33cf2-108">A device can use the MQTT protocol to connect to an IoT hub either by using the libraries in the [Azure IoT SDKs][lnk-device-sdks] or by using the MQTT protocol directly.</span></span>

## <a name="using-the-device-sdks"></a><span data-ttu-id="33cf2-109">De SDK's van het apparaat</span><span class="sxs-lookup"><span data-stu-id="33cf2-109">Using the device SDKs</span></span>

<span data-ttu-id="33cf2-110">[Apparaat-SDK's] [ lnk-device-sdks] die ondersteuning bieden voor het protocol MQTT zijn beschikbaar voor Java, Node.js, C, C# en Python.</span><span class="sxs-lookup"><span data-stu-id="33cf2-110">[Device SDKs][lnk-device-sdks] that support the MQTT protocol are available for Java, Node.js, C, C#, and Python.</span></span> <span data-ttu-id="33cf2-111">De apparaat-SDK's gebruiken de standaard IoT Hub-verbindingsreeks een verbinding maken met een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="33cf2-111">The device SDKs use the standard IoT Hub connection string to establish a connection to an IoT hub.</span></span> <span data-ttu-id="33cf2-112">De parameter van de client-protocol voor het gebruik van de protocollen MQTT protocol moet worden ingesteld op **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-112">To use the MQTT protocol, the client protocol parameter must be set to **MQTT**.</span></span> <span data-ttu-id="33cf2-113">Standaard, het apparaat SDK's verbinding maken met een IoT Hub met de **CleanSession** vlag ingesteld op **0** en gebruik **QoS 1** voor uitwisseling van berichten met de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="33cf2-113">By default, the device SDKs connect to an IoT Hub with the **CleanSession** flag set to **0** and use **QoS 1** for message exchange with the IoT hub.</span></span>

<span data-ttu-id="33cf2-114">Wanneer een apparaat is verbonden met een IoT-hub, bieden de apparaat-SKD's methoden waarmee het apparaat berichten te verzenden en ontvangen van berichten van een IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="33cf2-114">When a device is connected to an IoT hub, the device SDKs provide methods that enable the device to send messages to and receive messages from an IoT hub.</span></span>

<span data-ttu-id="33cf2-115">De volgende tabel bevat koppelingen naar codevoorbeelden voor elke ondersteunde taal en Hiermee geeft u de parameter moet een verbinding maken met IoT Hub met behulp van de protocollen MQTT-protocol gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33cf2-115">The following table contains links to code samples for each supported language and specifies the parameter to use to establish a connection to IoT Hub using the MQTT protocol.</span></span>

| <span data-ttu-id="33cf2-116">Taal</span><span class="sxs-lookup"><span data-stu-id="33cf2-116">Language</span></span> | <span data-ttu-id="33cf2-117">Parameter protocol</span><span class="sxs-lookup"><span data-stu-id="33cf2-117">Protocol parameter</span></span> |
| --- | --- |
| <span data-ttu-id="33cf2-118">[Node.js][lnk-sample-node]</span><span class="sxs-lookup"><span data-stu-id="33cf2-118">[Node.js][lnk-sample-node]</span></span> |<span data-ttu-id="33cf2-119">Azure-iot-device-mqtt</span><span class="sxs-lookup"><span data-stu-id="33cf2-119">azure-iot-device-mqtt</span></span> |
| <span data-ttu-id="33cf2-120">[Java][lnk-sample-java]</span><span class="sxs-lookup"><span data-stu-id="33cf2-120">[Java][lnk-sample-java]</span></span> |<span data-ttu-id="33cf2-121">IotHubClientProtocol.MQTT</span><span class="sxs-lookup"><span data-stu-id="33cf2-121">IotHubClientProtocol.MQTT</span></span> |
| <span data-ttu-id="33cf2-122">[C][lnk-sample-c]</span><span class="sxs-lookup"><span data-stu-id="33cf2-122">[C][lnk-sample-c]</span></span> |<span data-ttu-id="33cf2-123">MQTT_Protocol</span><span class="sxs-lookup"><span data-stu-id="33cf2-123">MQTT_Protocol</span></span> |
| <span data-ttu-id="33cf2-124">[C#][lnk-sample-csharp]</span><span class="sxs-lookup"><span data-stu-id="33cf2-124">[C#][lnk-sample-csharp]</span></span> |<span data-ttu-id="33cf2-125">TransportType.Mqtt</span><span class="sxs-lookup"><span data-stu-id="33cf2-125">TransportType.Mqtt</span></span> |
| <span data-ttu-id="33cf2-126">[Python][lnk-sample-python]</span><span class="sxs-lookup"><span data-stu-id="33cf2-126">[Python][lnk-sample-python]</span></span> |<span data-ttu-id="33cf2-127">IoTHubTransportProvider.MQTT</span><span class="sxs-lookup"><span data-stu-id="33cf2-127">IoTHubTransportProvider.MQTT</span></span> |

### <a name="migrating-a-device-app-from-amqp-to-mqtt"></a><span data-ttu-id="33cf2-128">Migreren van een apparaat-app van AMQP naar MQTT</span><span class="sxs-lookup"><span data-stu-id="33cf2-128">Migrating a device app from AMQP to MQTT</span></span>

<span data-ttu-id="33cf2-129">Als u de [apparaat-SKD's][lnk-device-sdks], wijzigen van de parameter protocol in de clientinitialisatie van de, zoals eerder gezegd overschakelen via AMQP naar MQTT vereist.</span><span class="sxs-lookup"><span data-stu-id="33cf2-129">If you are using the [device SDKs][lnk-device-sdks], switching from using AMQP to MQTT requires changing the protocol parameter in the client initialization as stated previously.</span></span>

<span data-ttu-id="33cf2-130">Wanneer doet, zorg er dan voor dat het volgende controleren:</span><span class="sxs-lookup"><span data-stu-id="33cf2-130">When doing so, make sure to check the following items:</span></span>

* <span data-ttu-id="33cf2-131">AMQP retourneert fouten voor veel voorwaarden terwijl MQTT wordt de verbinding verbroken.</span><span class="sxs-lookup"><span data-stu-id="33cf2-131">AMQP returns errors for many conditions, while MQTT terminates the connection.</span></span> <span data-ttu-id="33cf2-132">Als gevolg hiervan uw uitzonderingsverwerking logica mogelijk enkele wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-132">As a result your exception handling logic might require some changes.</span></span>
* <span data-ttu-id="33cf2-133">MQTT biedt geen ondersteuning voor de *afwijzen* operations tijdens het ontvangen van [cloud-naar-apparaatberichten][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="33cf2-133">MQTT does not support the *reject* operations when receiving [cloud-to-device messages][lnk-messaging].</span></span> <span data-ttu-id="33cf2-134">Als uw back-endserver voor apps een reactie ontvangen van de app voor het apparaat moet, kunt u overwegen [methoden directe][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="33cf2-134">If your back-end app needs to receive a response from the device app, consider using [direct methods][lnk-methods].</span></span>

## <a name="using-the-mqtt-protocol-directly"></a><span data-ttu-id="33cf2-135">Met behulp van het protocol MQTT rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="33cf2-135">Using the MQTT protocol directly</span></span>
<span data-ttu-id="33cf2-136">Als een apparaat niet kan het apparaat-SDK's, kan deze nog steeds verbinding maken met de openbare apparaat eindpunten met de protocollen MQTT-protocol op poort 8883.</span><span class="sxs-lookup"><span data-stu-id="33cf2-136">If a device cannot use the device SDKs, it can still connect to the public device endpoints using the MQTT protocol on port 8883.</span></span> <span data-ttu-id="33cf2-137">In de **CONNECT** pakket het apparaat moet de volgende waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="33cf2-137">In the **CONNECT** packet the device should use the following values:</span></span>

* <span data-ttu-id="33cf2-138">Voor de **ClientId** veld, gebruikt u de **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-138">For the **ClientId** field, use the **deviceId**.</span></span>
* <span data-ttu-id="33cf2-139">Voor de **gebruikersnaam** veld `{iothubhostname}/{device_id}/api-version=2016-11-14`, waarbij {iothubhostname} is de volledige CName van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="33cf2-139">For the **Username** field, use `{iothubhostname}/{device_id}/api-version=2016-11-14`, where {iothubhostname} is the full CName of the IoT hub.</span></span>

    <span data-ttu-id="33cf2-140">Bijvoorbeeld, als de naam van uw IoT-hub is **contoso.azure devices.net** en als de naam van uw apparaat **MyDevice01**, de volledige **gebruikersnaam** veld moetbevatten`contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span><span class="sxs-lookup"><span data-stu-id="33cf2-140">For example, if the name of your IoT hub is **contoso.azure-devices.net** and if the name of your device is **MyDevice01**, the full **Username** field should contain `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.</span></span>
* <span data-ttu-id="33cf2-141">Voor de **wachtwoord** veld, gebruikt u een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="33cf2-141">For the **Password** field, use a SAS token.</span></span> <span data-ttu-id="33cf2-142">De indeling van het SAS-token is hetzelfde als voor de HTTP- en AMQP protocollen:</span><span class="sxs-lookup"><span data-stu-id="33cf2-142">The format of the SAS token is the same as for both the HTTP and AMQP protocols:</span></span><br/><span data-ttu-id="33cf2-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span><span class="sxs-lookup"><span data-stu-id="33cf2-143">`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.</span></span>

    <span data-ttu-id="33cf2-144">Zie voor meer informatie over het genereren van SAS-tokens de apparaat-sectie van [IoT Hub met behulp van beveiligingstokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="33cf2-144">For more information about how to generate SAS tokens, see the device section of [Using IoT Hub security tokens][lnk-sas-tokens].</span></span>

    <span data-ttu-id="33cf2-145">Bij het testen, kunt u ook gebruiken de [apparaat explorer] [ lnk-device-explorer] hulpprogramma snel een SAS-token dat u kunt kopiëren en plakken in uw eigen code genereren:</span><span class="sxs-lookup"><span data-stu-id="33cf2-145">When testing, you can also use the [device explorer][lnk-device-explorer] tool to quickly generate a SAS token that you can copy and paste into your own code:</span></span>

  1. <span data-ttu-id="33cf2-146">Ga naar de **Management** tabblad **apparaat Explorer**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-146">Go to the **Management** tab in **Device Explorer**.</span></span>
  2. <span data-ttu-id="33cf2-147">Klik op **SAS-Token** (top rechts).</span><span class="sxs-lookup"><span data-stu-id="33cf2-147">Click **SAS Token** (top right).</span></span>
  3. <span data-ttu-id="33cf2-148">Op **SASTokenForm**, selecteer het apparaat in de **DeviceID** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="33cf2-148">On **SASTokenForm**, select your device in the **DeviceID** drop down.</span></span> <span data-ttu-id="33cf2-149">Stel uw **TTL**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-149">Set your **TTL**.</span></span>
  4. <span data-ttu-id="33cf2-150">Klik op **genereren** uw token maken.</span><span class="sxs-lookup"><span data-stu-id="33cf2-150">Click **Generate** to create your token.</span></span>

     <span data-ttu-id="33cf2-151">De SAS-token dat gegenereerd, is deze structuur: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="33cf2-151">The SAS token that's generated has this structure: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

     <span data-ttu-id="33cf2-152">Het deel van dit token gebruiken als de **wachtwoord** veld verbinding maken via de protocollen MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span><span class="sxs-lookup"><span data-stu-id="33cf2-152">The part of this token to use as the **Password** field to connect using MQTT is: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.</span></span>

<span data-ttu-id="33cf2-153">MQTT verbinding maken met en pakketten verbreken, IoT-Hub geeft een gebeurtenis op de **Operations Monitoring** kanaal met aanvullende informatie die u helpen kan bij het oplossen van problemen met de netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="33cf2-153">For MQTT connect and disconnect packets, IoT Hub issues an event on the **Operations Monitoring** channel with additional information that can help you to troubleshoot connectivity issues.</span></span>

### <a name="sending-device-to-cloud-messages"></a><span data-ttu-id="33cf2-154">Verzenden van apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="33cf2-154">Sending device-to-cloud messages</span></span>

<span data-ttu-id="33cf2-155">Nadat u de verbinding is geslaagd, een apparaat kunt verzenden berichten naar IoT Hub met `devices/{device_id}/messages/events/` of `devices/{device_id}/messages/events/{property_bag}` als een **onderwerpnaam**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-155">After making a successful connection, a device can send messages to IoT Hub using `devices/{device_id}/messages/events/` or `devices/{device_id}/messages/events/{property_bag}` as a **Topic Name**.</span></span> <span data-ttu-id="33cf2-156">De `{property_bag}` element kunt u het apparaat te verzenden van berichten met aanvullende eigenschappen in een url-notatie.</span><span class="sxs-lookup"><span data-stu-id="33cf2-156">The `{property_bag}` element enables the device to send messages with additional properties in a url-encoded format.</span></span> <span data-ttu-id="33cf2-157">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33cf2-157">For example:</span></span>

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> <span data-ttu-id="33cf2-158">Dit `{property_bag}` element gebruikt dezelfde codering voor queryreeksen in de HTTP-protocol.</span><span class="sxs-lookup"><span data-stu-id="33cf2-158">This `{property_bag}` element uses the same encoding as for query strings in the HTTP protocol.</span></span>
>
>

<span data-ttu-id="33cf2-159">De apparaat-app kunt `devices/{device_id}/messages/events/{property_bag}` als de **wordt de naam van onderwerp** definiëren *berichten wordt* moeten worden doorgestuurd als een bericht telemetrie.</span><span class="sxs-lookup"><span data-stu-id="33cf2-159">The device app can also use `devices/{device_id}/messages/events/{property_bag}` as the **Will topic name** to define *Will messages* to be forwarded as a telemetry message.</span></span>

- <span data-ttu-id="33cf2-160">IoT Hub biedt geen ondersteuning voor QoS-2-berichten.</span><span class="sxs-lookup"><span data-stu-id="33cf2-160">IoT Hub does not support QoS 2 messages.</span></span> <span data-ttu-id="33cf2-161">Als een apparaat-app een bericht met publiceert **QoS 2**, IoT Hub de netwerkverbinding wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="33cf2-161">If a device app publishes a message with **QoS 2**, IoT Hub closes the network connection.</span></span>
- <span data-ttu-id="33cf2-162">IoT Hub behouden berichten niet bewaard is gebleven.</span><span class="sxs-lookup"><span data-stu-id="33cf2-162">IoT Hub does not persist Retain messages.</span></span> <span data-ttu-id="33cf2-163">Als een apparaat een bericht met verzendt de **behouden** vlag ingesteld op 1, IoT-Hub voegt de **x-opt-behouden** -eigenschap van toepassing op het bericht.</span><span class="sxs-lookup"><span data-stu-id="33cf2-163">If a device sends a message with the **RETAIN** flag set to 1, IoT Hub adds the **x-opt-retain** application property to the message.</span></span> <span data-ttu-id="33cf2-164">In dit geval wordt in plaats van het behouden blijven van het bericht behouden, IoT-Hub wordt doorgegeven aan de back-end-app.</span><span class="sxs-lookup"><span data-stu-id="33cf2-164">In this case, instead of persisting the retain message, IoT Hub passes it to the backend app.</span></span>
- <span data-ttu-id="33cf2-165">IoT Hub ondersteunt slechts één actieve MQTT verbinding per apparaat.</span><span class="sxs-lookup"><span data-stu-id="33cf2-165">IoT Hub only supports one active MQTT connection per device.</span></span> <span data-ttu-id="33cf2-166">Een nieuwe verbinding MQTT namens de dezelfde apparaat-ID zorgt ervoor dat de IoT-Hub verwijderen van de bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="33cf2-166">Any new MQTT connection on behalf of the same device ID causes IoT Hub to drop the existing connection.</span></span>

<span data-ttu-id="33cf2-167">Zie voor meer informatie [Messaging-handleiding voor ontwikkelaars][lnk-messaging].</span><span class="sxs-lookup"><span data-stu-id="33cf2-167">For more information, see [Messaging developer's guide][lnk-messaging].</span></span>

### <a name="receiving-cloud-to-device-messages"></a><span data-ttu-id="33cf2-168">Cloud-naar-apparaat-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="33cf2-168">Receiving cloud-to-device messages</span></span>

<span data-ttu-id="33cf2-169">Voor het ontvangen van berichten uit IoT Hub, een apparaat moet abonneren met `devices/{device_id}/messages/devicebound/#` als een **onderwerp Filter**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-169">To receive messages from IoT Hub, a device should subscribe using `devices/{device_id}/messages/devicebound/#` as a **Topic Filter**.</span></span> <span data-ttu-id="33cf2-170">Het jokerteken met meerdere niveaus  **#**  in het onderwerp Filter wordt alleen gebruikt om aanvullende eigenschappen ontvangen in de onderwerpnaam van het apparaat toestaan.</span><span class="sxs-lookup"><span data-stu-id="33cf2-170">The multi-level wildcard **#** in the Topic Filter is used only to allow the device to receive additional properties in the topic name.</span></span> <span data-ttu-id="33cf2-171">IoT Hub is niet toegestaan voor het gebruik van de  **#**  of **?**</span><span class="sxs-lookup"><span data-stu-id="33cf2-171">IoT Hub does not allow the usage of the **#** or **?**</span></span> <span data-ttu-id="33cf2-172">jokertekens voor het filteren van de onderliggende onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-172">wildcards for filtering of sub-topics.</span></span> <span data-ttu-id="33cf2-173">Omdat in IoT Hub is niet algemeen pub sub messaging broker, ondersteunt deze alleen de gedocumenteerde onderwerpnamen en onderwerp filters.</span><span class="sxs-lookup"><span data-stu-id="33cf2-173">Since IoT Hub is not a general purpose pub-sub messaging broker, it only supports the documented topic names and topic filters.</span></span>

<span data-ttu-id="33cf2-174">Het apparaat niet ontvangt berichten uit IoT Hub, totdat deze is geabonneerd op het eindpunt apparaatspecifieke, vertegenwoordigd door de `devices/{device_id}/messages/devicebound/#` onderwerp filter.</span><span class="sxs-lookup"><span data-stu-id="33cf2-174">The device does not receive any messages from IoT Hub, until it has successfully subscribed to its device-specific endpoint, represented by the `devices/{device_id}/messages/devicebound/#` topic filter.</span></span> <span data-ttu-id="33cf2-175">Nadat een geslaagde abonnement is ingesteld, wordt het apparaat wordt gestart alleen cloud-naar-apparaat-berichten dat is verzonden naar deze na de tijd van het abonnement ontvangen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-175">After successful subscription has been established, the device starts receiving only cloud-to-device messages that have been sent to it after the time of the subscription.</span></span> <span data-ttu-id="33cf2-176">Als het apparaat verbinding met maakt **CleanSession** vlag ingesteld op **0**, het abonnement over de verschillende sessies worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="33cf2-176">If the device connects with **CleanSession** flag set to **0**, the subscription is persisted across different sessions.</span></span> <span data-ttu-id="33cf2-177">In dit geval wordt de volgende keer dat deze verbinding maakt met **CleanSession 0** het apparaat heeft openstaande berichten die zijn verzonden naar het terwijl er geen verbinding was ontvangen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-177">In this case, the next time it connects with **CleanSession 0** the device receives outstanding messages that have been sent to it while it was disconnected.</span></span> <span data-ttu-id="33cf2-178">Als het apparaat gebruikmaakt van **CleanSession** vlag ingesteld op **1** echter er komt geen ontvangen alle berichten uit IoT Hub totdat het apparaat-eindpunt worden bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="33cf2-178">If the device uses **CleanSession** flag set to **1** though, it does not receive any messages from IoT Hub until it subscribes to its device-endpoint.</span></span>

<span data-ttu-id="33cf2-179">IoT Hub biedt berichten met de **onderwerpnaam** `devices/{device_id}/messages/devicebound/`, of `devices/{device_id}/messages/devicebound/{property_bag}` als er een berichteigenschappen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-179">IoT Hub delivers messages with the **Topic Name** `devices/{device_id}/messages/devicebound/`, or `devices/{device_id}/messages/devicebound/{property_bag}` if there are any message properties.</span></span> <span data-ttu-id="33cf2-180">`{property_bag}`url-codering sleutel-waardeparen van berichteigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="33cf2-180">`{property_bag}` contains url-encoded key/value pairs of message properties.</span></span> <span data-ttu-id="33cf2-181">Alleen de toepassingseigenschappen en de gebruiker instelbare eigenschappen (zoals **messageId** of **correlationId**) zijn opgenomen in de eigenschappenverzameling.</span><span class="sxs-lookup"><span data-stu-id="33cf2-181">Only application properties and user-settable system properties (such as **messageId** or **correlationId**) are included in the property bag.</span></span> <span data-ttu-id="33cf2-182">Namen van de eigenschap System hebben het voorvoegsel  **$** , toepassingseigenschappen oorspronkelijke naam van de eigenschap met geen voorvoegsel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33cf2-182">System property names have the prefix **$**, application properties use the original property name with no prefix.</span></span>

<span data-ttu-id="33cf2-183">Wanneer een app voor het apparaat is lid van een onderwerp met **QoS 2**, IoT-Hub geeft het maximum aantal QoS-niveau 1 in de **SUBACK** pakket.</span><span class="sxs-lookup"><span data-stu-id="33cf2-183">When a device app subscribes to a topic with **QoS 2**, IoT Hub grants maximum QoS level 1 in the **SUBACK** packet.</span></span> <span data-ttu-id="33cf2-184">Daarna biedt IoT Hub berichten op het apparaat met behulp van QoS-1.</span><span class="sxs-lookup"><span data-stu-id="33cf2-184">After that, IoT Hub delivers messages to the device using QoS 1.</span></span>

### <a name="retrieving-a-device-twins-properties"></a><span data-ttu-id="33cf2-185">Ophalen van de eigenschappen van een apparaat-twin</span><span class="sxs-lookup"><span data-stu-id="33cf2-185">Retrieving a device twin's properties</span></span>

<span data-ttu-id="33cf2-186">Eerst een apparaat is lid van `$iothub/twin/res/#`, voor het ontvangen van reacties van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="33cf2-186">First, a device subscribes to `$iothub/twin/res/#`, to receive the operation's responses.</span></span> <span data-ttu-id="33cf2-187">Vervolgens wordt een leeg bericht verzonden naar onderwerp `$iothub/twin/GET/?$rid={request id}`, met de ingestelde waarde voor **aanvraag-id**.</span><span class="sxs-lookup"><span data-stu-id="33cf2-187">Then, it sends an empty message to topic `$iothub/twin/GET/?$rid={request id}`, with a populated value for **request id**.</span></span> <span data-ttu-id="33cf2-188">De service verzendt vervolgens een antwoordbericht, waarin de gegevens van het apparaat twin op onderwerp `$iothub/twin/res/{status}/?$rid={request id}`, met behulp van dezelfde **aanvraag-id** als de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="33cf2-188">The service then sends a response message containing the device twin data on topic `$iothub/twin/res/{status}/?$rid={request id}`, using the same **request id** as the request.</span></span>

<span data-ttu-id="33cf2-189">Aanvraag-id mag geldige waarde voor de waarde van een bericht eigenschap conform [messaging Ontwikkelaarshandleiding voor IoT-Hub][lnk-messaging], en de status wordt gevalideerd als een geheel getal.</span><span class="sxs-lookup"><span data-stu-id="33cf2-189">Request id can be any valid value for a message property value, as per [IoT Hub messaging developer's guide][lnk-messaging], and status is validated as an integer.</span></span>
<span data-ttu-id="33cf2-190">Hoofdtekst van de reactie bevat het eigenschappengedeelte van het apparaat twin:</span><span class="sxs-lookup"><span data-stu-id="33cf2-190">The response body contains the properties section of the device twin:</span></span>

<span data-ttu-id="33cf2-191">De hoofdtekst van de identiteit registervermelding beperkt tot het lid 'Eigenschappen', bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33cf2-191">The body of the identity registry entry limited to the “properties” member, for example:</span></span>

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

<span data-ttu-id="33cf2-192">De mogelijke statuscodes zijn:</span><span class="sxs-lookup"><span data-stu-id="33cf2-192">The possible status codes are:</span></span>

|<span data-ttu-id="33cf2-193">Status</span><span class="sxs-lookup"><span data-stu-id="33cf2-193">Status</span></span> | <span data-ttu-id="33cf2-194">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="33cf2-194">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="33cf2-195">200</span><span class="sxs-lookup"><span data-stu-id="33cf2-195">200</span></span> | <span data-ttu-id="33cf2-196">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="33cf2-196">Success</span></span> |
| <span data-ttu-id="33cf2-197">429</span><span class="sxs-lookup"><span data-stu-id="33cf2-197">429</span></span> | <span data-ttu-id="33cf2-198">Te veel aanvragen (beperkt), conform [beperking IoT-Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="33cf2-198">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="33cf2-199">5**</span><span class="sxs-lookup"><span data-stu-id="33cf2-199">5**</span></span> | <span data-ttu-id="33cf2-200">Server-fouten</span><span class="sxs-lookup"><span data-stu-id="33cf2-200">Server errors</span></span> |

<span data-ttu-id="33cf2-201">Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="33cf2-201">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="update-device-twins-reported-properties"></a><span data-ttu-id="33cf2-202">Update apparaat twin gerapporteerd eigenschappen</span><span class="sxs-lookup"><span data-stu-id="33cf2-202">Update device twin's reported properties</span></span>

<span data-ttu-id="33cf2-203">De volgende procedure wordt beschreven hoe een apparaat bijgewerkt voor de gerapporteerde eigenschappen in de apparaat-twin in IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="33cf2-203">The following sequence describes how a device updates the reported properties in the device twin in IoT Hub:</span></span>

1. <span data-ttu-id="33cf2-204">Een apparaat moet zich eerst abonneren op de `$iothub/twin/res/#` onderwerp van de bewerking reacties van IoT-Hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="33cf2-204">A device must first subscribe to the `$iothub/twin/res/#` topic to receive the operation's responses from IoT Hub.</span></span>

1. <span data-ttu-id="33cf2-205">Een apparaat verzendt een bericht met de apparaat-twin update naar de `$iothub/twin/PATCH/properties/reported/?$rid={request id}` onderwerp.</span><span class="sxs-lookup"><span data-stu-id="33cf2-205">A device sends a message that contains the device twin update to the `$iothub/twin/PATCH/properties/reported/?$rid={request id}` topic.</span></span> <span data-ttu-id="33cf2-206">Dit bericht bevat een **aanvraag-id** waarde.</span><span class="sxs-lookup"><span data-stu-id="33cf2-206">This message includes a **request id** value.</span></span>

1. <span data-ttu-id="33cf2-207">De service verzendt vervolgens een antwoordbericht met de nieuwe ETag-waarde voor de verzameling gemelde eigenschappen op onderwerp `$iothub/twin/res/{status}/?$rid={request id}`.</span><span class="sxs-lookup"><span data-stu-id="33cf2-207">The service then sends a response message that contains the new ETag value for the reported properties collection on topic `$iothub/twin/res/{status}/?$rid={request id}`.</span></span> <span data-ttu-id="33cf2-208">Dit antwoordbericht maakt gebruik van dezelfde **aanvraag-id** als de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="33cf2-208">This response message uses the same **request id** as the request.</span></span>

<span data-ttu-id="33cf2-209">De berichttekst voor de aanvraag bevat een JSON-document, wat zorgt voor nieuwe waarden voor de gerapporteerde eigenschappen (geen andere eigenschap of metagegevens kan worden aangepast).</span><span class="sxs-lookup"><span data-stu-id="33cf2-209">The request message body contains a JSON document, which provides new values for reported properties (no other property or metadata can be modified).</span></span>
<span data-ttu-id="33cf2-210">Elk lid in het JSON-document updates of het bijbehorende lid in de apparaat-twin document toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-210">Each member in the JSON document updates or add the corresponding member in the device twin’s document.</span></span> <span data-ttu-id="33cf2-211">Een lid is ingesteld op `null`, verwijdert u het lid van het containerobject.</span><span class="sxs-lookup"><span data-stu-id="33cf2-211">A member set to `null`, deletes the member from the containing object.</span></span> <span data-ttu-id="33cf2-212">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33cf2-212">For example:</span></span>

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

<span data-ttu-id="33cf2-213">De mogelijke statuscodes zijn:</span><span class="sxs-lookup"><span data-stu-id="33cf2-213">The possible status codes are:</span></span>

|<span data-ttu-id="33cf2-214">Status</span><span class="sxs-lookup"><span data-stu-id="33cf2-214">Status</span></span> | <span data-ttu-id="33cf2-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="33cf2-215">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="33cf2-216">200</span><span class="sxs-lookup"><span data-stu-id="33cf2-216">200</span></span> | <span data-ttu-id="33cf2-217">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="33cf2-217">Success</span></span> |
| <span data-ttu-id="33cf2-218">400</span><span class="sxs-lookup"><span data-stu-id="33cf2-218">400</span></span> | <span data-ttu-id="33cf2-219">Ongeldige aanvraag.</span><span class="sxs-lookup"><span data-stu-id="33cf2-219">Bad Request.</span></span> <span data-ttu-id="33cf2-220">Ongeldige JSON</span><span class="sxs-lookup"><span data-stu-id="33cf2-220">Malformed JSON</span></span> |
| <span data-ttu-id="33cf2-221">429</span><span class="sxs-lookup"><span data-stu-id="33cf2-221">429</span></span> | <span data-ttu-id="33cf2-222">Te veel aanvragen (beperkt), conform [beperking IoT-Hub][lnk-quotas]</span><span class="sxs-lookup"><span data-stu-id="33cf2-222">Too many requests (throttled), as per [IoT Hub throttling][lnk-quotas]</span></span> |
| <span data-ttu-id="33cf2-223">5**</span><span class="sxs-lookup"><span data-stu-id="33cf2-223">5**</span></span> | <span data-ttu-id="33cf2-224">Server-fouten</span><span class="sxs-lookup"><span data-stu-id="33cf2-224">Server errors</span></span> |

<span data-ttu-id="33cf2-225">Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="33cf2-225">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="receiving-desired-properties-update-notifications"></a><span data-ttu-id="33cf2-226">Ontvangende gewenste eigenschappen updatemeldingen</span><span class="sxs-lookup"><span data-stu-id="33cf2-226">Receiving desired properties update notifications</span></span>

<span data-ttu-id="33cf2-227">Wanneer een apparaat is verbonden, IoT-Hub meldingen worden verzonden naar het onderwerp `$iothub/twin/PATCH/properties/desired/?$version={new version}`, die de inhoud van de update die wordt uitgevoerd door de back-end oplossing bevatten.</span><span class="sxs-lookup"><span data-stu-id="33cf2-227">When a device is connected, IoT Hub sends notifications to the topic `$iothub/twin/PATCH/properties/desired/?$version={new version}`, which contain the content of the update performed by the solution back end.</span></span> <span data-ttu-id="33cf2-228">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33cf2-228">For example:</span></span>

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

<span data-ttu-id="33cf2-229">Als voor updates voor de eigenschap `null` waarden betekent dat het JSON-Objectlid wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="33cf2-229">As for property updates, `null` values means that the JSON object member is being deleted.</span></span>


> [!IMPORTANT] 
> <span data-ttu-id="33cf2-230">IoT Hub genereert wijzigingsmeldingen alleen wanneer apparaten zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="33cf2-230">IoT Hub generates change notifications only when devices are connected.</span></span> <span data-ttu-id="33cf2-231">Zorg ervoor dat voor het implementeren van de [apparaat opnieuw verbinden stroom] [ lnk-devguide-twin-reconnection] te houden van de gewenste eigenschappen gesynchroniseerd tussen IoT Hub en de app voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="33cf2-231">Make sure to implement the [device reconnection flow][lnk-devguide-twin-reconnection] to keep the desired properties synchronized between IoT Hub and the device app.</span></span>

<span data-ttu-id="33cf2-232">Zie voor meer informatie [Ontwikkelaarshandleiding voor apparaat horende][lnk-devguide-twin].</span><span class="sxs-lookup"><span data-stu-id="33cf2-232">For more information, see [Device twins developer's guide][lnk-devguide-twin].</span></span>

### <a name="respond-to-a-direct-method"></a><span data-ttu-id="33cf2-233">Reageren op een directe methode</span><span class="sxs-lookup"><span data-stu-id="33cf2-233">Respond to a direct method</span></span>

<span data-ttu-id="33cf2-234">Eerst een apparaat heeft om zich te abonneren op `$iothub/methods/POST/#`.</span><span class="sxs-lookup"><span data-stu-id="33cf2-234">First, a device has to subscribe to `$iothub/methods/POST/#`.</span></span> <span data-ttu-id="33cf2-235">IoT Hub verzendt methodeaanvragen naar het onderwerp `$iothub/methods/POST/{method name}/?$rid={request id}`, met een geldige JSON of een lege hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="33cf2-235">IoT Hub sends method requests to the topic `$iothub/methods/POST/{method name}/?$rid={request id}`, with either a valid JSON or an empty body.</span></span>

<span data-ttu-id="33cf2-236">Om te reageren, het apparaat verzendt een bericht met een geldige JSON of een lege hoofdtekst naar het onderwerp `$iothub/methods/res/{status}/?$rid={request id}`, waarbij **aanvraag-id** moet overeenkomen met de naam in het aanvraagbericht en **status** moet een geheel getal zijn.</span><span class="sxs-lookup"><span data-stu-id="33cf2-236">To respond, the device sends a message with a valid JSON or empty body to the topic `$iothub/methods/res/{status}/?$rid={request id}`, where **request id** has to match the one in the request message, and **status** has to be an integer.</span></span>

<span data-ttu-id="33cf2-237">Zie voor meer informatie [directe methode Ontwikkelaarshandleiding voor][lnk-methods].</span><span class="sxs-lookup"><span data-stu-id="33cf2-237">For more information, see [Direct method developer's guide][lnk-methods].</span></span>

### <a name="additional-considerations"></a><span data-ttu-id="33cf2-238">Aanvullende overwegingen</span><span class="sxs-lookup"><span data-stu-id="33cf2-238">Additional considerations</span></span>

<span data-ttu-id="33cf2-239">Als een definitieve overweging wanneer moet u het gedrag van protocollen MQTT protocol aan de cloud aanpassen raadpleegt u de [protocolgateway van Azure IOT] [ lnk-azure-protocol-gateway] waarmee u een aangepaste krachtige implementeren protocolgateway die rechtstreeks met IoT Hub-interfaces.</span><span class="sxs-lookup"><span data-stu-id="33cf2-239">As a final consideration, if you need to customize the MQTT protocol behavior on the cloud side, you should review the [Azure IoT protocol gateway][lnk-azure-protocol-gateway] that enables you to deploy a high-performance custom protocol gateway that interfaces directly with IoT Hub.</span></span> <span data-ttu-id="33cf2-240">De Azure IoT-protocol-gateway kunt u het apparaat-protocol voor brownfield MQTT implementaties of andere aangepaste protocollen wilt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="33cf2-240">The Azure IoT protocol gateway enables you to customize the device protocol to accommodate brownfield MQTT deployments or other custom protocols.</span></span> <span data-ttu-id="33cf2-241">Deze aanpak is echter vereist die u uitvoert en een aangepaste protocol-gateway werkt.</span><span class="sxs-lookup"><span data-stu-id="33cf2-241">This approach does require, however, that you run and operate a custom protocol gateway.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33cf2-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33cf2-242">Next steps</span></span>

<span data-ttu-id="33cf2-243">Zie voor meer informatie over het protocol MQTT, de [MQTT documentatie][lnk-mqtt-docs].</span><span class="sxs-lookup"><span data-stu-id="33cf2-243">To learn more about the MQTT protocol, see the [MQTT documentation][lnk-mqtt-docs].</span></span>

<span data-ttu-id="33cf2-244">Zie voor meer informatie over het plannen van de implementatie van uw IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="33cf2-244">To learn more about planning your IoT Hub deployment, see:</span></span>

* <span data-ttu-id="33cf2-245">[Azure gecertificeerd voor de catalogus van IoT-apparaat][lnk-devices]</span><span class="sxs-lookup"><span data-stu-id="33cf2-245">[Azure Certified for IoT device catalog][lnk-devices]</span></span>
* <span data-ttu-id="33cf2-246">[Ondersteuning voor aanvullende protocollen][lnk-protocols]</span><span class="sxs-lookup"><span data-stu-id="33cf2-246">[Support additional protocols][lnk-protocols]</span></span>
* <span data-ttu-id="33cf2-247">[Vergelijken met Event Hubs][lnk-compare]</span><span class="sxs-lookup"><span data-stu-id="33cf2-247">[Compare with Event Hubs][lnk-compare]</span></span>
* <span data-ttu-id="33cf2-248">[Schalen, HA en Noodherstel][lnk-scaling]</span><span class="sxs-lookup"><span data-stu-id="33cf2-248">[Scaling, HA, and DR][lnk-scaling]</span></span>

<span data-ttu-id="33cf2-249">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="33cf2-249">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="33cf2-250">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="33cf2-250">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="33cf2-251">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="33cf2-251">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
