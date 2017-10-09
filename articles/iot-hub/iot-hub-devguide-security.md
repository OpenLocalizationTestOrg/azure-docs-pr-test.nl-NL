---
title: aaaUnderstand security voor Azure IoT Hub | Microsoft Docs
description: Ontwikkelaars begeleiden - hoe toocontrol toegang krijgen tot tooIoT Hub voor apparaat-apps en apps van de back-end. Bevat informatie over beveiligingstokens en ondersteuning voor X.509-certificaten.
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
ms.openlocfilehash: 717726328a6bb5c5c334a123d0abfed711b2c3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-access-tooiot-hub"></a>Beheer toegang tooIoT Hub

Dit artikel wordt beschreven Hallo opties voor het beveiligen van uw IoT-hub. IoT Hub gebruikt *machtigingen* toogrant toegang tooeach IoT-hubeindpunt. Machtigingen beperken Hallo toegang tooan IoT-hub op basis van functionaliteit.

Dit artikel wordt beschreven:

* Hallo andere machtigingen die u tooa apparaat of back-endserver voor apps tooaccess uw IoT-hub verleent kunt.
* Hallo-proces en Hallo verificatietokens tooverify machtigingen wordt gebruikt.
* Hoe referenties tooscope toolimit toegang tot toospecific bronnen.
* IoT Hub-ondersteuning voor het X.509-certificaten.
* Aangepast apparaat verificatiemechanismen die gebruikmaken van bestaande apparaten identiteit registers of verificatieschema's.

### <a name="when-toouse"></a>Wanneer toouse

U moet hebben gemachtigd tooaccess van Hallo Iothub-eindpunten. Een apparaat moet bijvoorbeeld een token met beveiligingsreferenties samen met elk bericht dat tooiot Hub worden verzonden.

## <a name="access-control-and-permissions"></a>Toegangsbeheer en machtigingen

U kunt verlenen [machtigingen](#iot-hub-permissions) in Hallo volgende manieren:

* **IoT hub-niveau gedeelde toegangsbeleid**. Beleid voor gedeelde toegang kunnen verlenen tot een combinatie van [machtigingen](#iot-hub-permissions). U kunt beleid definiëren in Hallo [Azure-portal][lnk-management-portal], of programmatisch met behulp van Hallo [resourceprovider IoT Hub REST-API's][lnk-resource-provider-apis]. Een nieuwe iothub heeft Hallo standaardbeleidsregels te volgen:

  * **iothubowner**: beleid met alle machtigingen.
  * **service**: beleid met **ServiceConnect** machtiging.
  * **apparaat**: beleid met **DeviceConnect** machtiging.
  * **registryRead**: beleid met **RegistryRead** machtiging.
  * **registryReadWrite**: beleid met **RegistryRead** en RegistryWrite machtigingen.
  * **Beveiligingsreferenties per apparaat**. Elke IoT-Hub bevat een [identiteitsregister][lnk-identity-registry]. U kunt beveiligingsreferenties op die verlenen configureren voor elk apparaat in het identiteitenregister van deze **DeviceConnect** toohello bijbehorende apparaat eindpunten binnen het bereik van machtigingen.

Bijvoorbeeld in een typische IoT-oplossing:

* Hallo device management-component gebruikt Hallo *registryReadWrite* beleid.
* Hallo gebeurtenis processor component gebruikt Hallo *service* beleid.
* Hallo runtime-apparaat zakelijke logica component gebruikt Hallo *service* beleid.
* Afzonderlijke apparaten verbinding maken met behulp van referenties opgeslagen in de id-register Hallo iothub.

> [!NOTE]
> Zie [machtigingen](#iot-hub-permissions) voor gedetailleerde informatie.

## <a name="authentication"></a>Authentication

Azure IoT Hub verleent toegang tooendpoints door te controleren of een token tegen Hallo gedeeld toegangsbeleid en identiteit register beveiligingsreferenties.

Beveiligingsreferenties zoals symmetrische sleutels worden nooit verzonden via de kabel Hallo.

> [!NOTE]
> Hello Azure IoT Hub-resourceprovider is beveiligd via uw Azure-abonnement, omdat alle providers op Hallo [Azure Resource Manager][lnk-azure-resource-manager].

Voor meer informatie over het beveiligingstokens tooconstruct en gebruik, Zie [IoT Hub beveiligingstokens][lnk-sas-tokens].

### <a name="protocol-specifics"></a>Protocol-specificaties

Elke ondersteunde protocollen, zoals MQTT AMQP en HTTP, transporten tokens op verschillende manieren.

Wanneer u MQTT, hello CONNECT-pakket heeft de Hallo deviceId Hallo ClientId, {iothubhostname} / {deviceId} in het veld Hallo-gebruikersnaam en een SAS-token in het wachtwoordveld Hallo. {iothubhostname} moet worden Hallo volledige CName van Hallo iothub (bijvoorbeeld contoso.azure-devices.net).

Wanneer u [AMQP][lnk-amqp], IoT-Hub ondersteunt [SASL zonder opmaak] [ lnk-sasl-plain] en [AMQP Claims-beveiliging op basis van-] [ lnk-cbs].

Als u het AMQP claims-beveiliging op basis-, standaard Hallo geeft aan hoe tootransmit deze tokens.

Hallo voor SASL zonder opmaak, **gebruikersnaam** kan zijn:

* `{policyName}@sas.root.{iothubName}`Als met IoT hub-niveau tokens.
* `{deviceId}@sas.{iothubname}`Als het gebruik van tokens binnen het bereik van apparaat.

In beide gevallen Hallo wachtwoordveld bevat Hallo-token, zoals beschreven in [IoT Hub beveiligingstokens][lnk-sas-tokens].

HTTP wordt de verificatie geïmplementeerd door een geldig token in Hallo **autorisatie** aanvraag-header.

#### <a name="example"></a>Voorbeeld

Gebruikersnaam (DeviceId is hoofdlettergevoelig):`iothubname.azure-devices.net/DeviceId`

Wachtwoord (genereren van SAS-token Hello [apparaat explorer] [ lnk-device-explorer] hulpprogramma):`SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`

> [!NOTE]
> Hallo [Azure IoT SDK's] [ lnk-sdks] automatisch genereren van tokens om verbinding te maken toohello service. In sommige gevallen hello Azure IoT SDK's ondersteunen geen alle Hallo protocollen of alle Hallo-verificatiemethoden.

### <a name="special-considerations-for-sasl-plain"></a>Speciale overwegingen voor SASL zonder opmaak

Als u SASL zonder opmaak met AMQP, kunt een client die verbinding tooan iothub een één-token gebruiken voor elke TCP-verbinding. Hallo-token is verlopen, Hallo TCP-verbinding verbreekt Hallo service als een reconnect activeert. Dit gedrag, is terwijl niet problematisch voor een back-end-app beschadigen voor een apparaat-app voor Hallo volgende redenen:

* Gateways verbinding meestal namens veel apparaten. Wanneer u SASL zonder opmaak, hebben ze toocreate een afzonderlijke TCP-verbinding voor elk apparaat verbinden tooan IoT-hub. Dit scenario aanzienlijk verhoogd Hallo verbruik van kracht en netwerkresources en Hallo latentie van elk apparaatverbinding.
* Resource beperkte apparaten nadelig worden beïnvloed door Hallo toegenomen gebruik van bronnen tooreconnect nadat elke token is verlopen.

## <a name="scope-iot-hub-level-credentials"></a>Bereik IoT hub-niveau referenties

U kunt het beveiligingsbeleid van IoT hub-niveau bereik tokens met een beperkte resource-URI te maken. Hallo eindpunt toosend apparaat-naar-cloud-berichten van een apparaat is bijvoorbeeld **/devices/ {deviceId} / berichten/gebeurtenissen**. U kunt ook een IoT hub-niveau gedeeld toegangsbeleid met **DeviceConnect** machtigingen toosign een token waarvan resourceURI wordt **/devices/ {deviceId}**. Deze methode maakt u een token dat is alleen bruikbaar toosend berichten namens apparaat **deviceId**.

Deze methode is vergelijkbaar toohello [Event Hubs uitgeversbeleid][lnk-event-hubs-publisher-policy], en kunt u aangepaste tooimplement-verificatiemethoden.

## <a name="security-tokens"></a>Beveiligingstokens

Beveiliging van IoT-Hub maakt gebruik van tokens tooauthenticate apparaten en services tooavoid sleutels op Hallo kabel verzenden. Bovendien zijn beveiligingstokens beperkt in geldigheid en het bereik. [Azure IoT SDK's] [ lnk-sdks] automatisch genereren van tokens zonder speciale configuratie. Sommige scenario's moet u toogenerate en beveiligingstokens rechtstreeks gebruiken. Dergelijke scenario's omvatten:

* Hallo direct gebruik van Hallo MQTT, AMQP of HTTP-verwerkingsinformatie.
* Hallo-implementatie van het patroon van de service voor beveiligingstokens hello, zoals wordt beschreven in [aangepaste apparaatverificatie][lnk-custom-auth].

IoT Hub kan ook apparaten tooauthenticate met IoT Hub met [X.509-certificaten][lnk-x509].

### <a name="security-token-structure"></a>Security token structuur

U beveiliging tokens toogrant tijd begrensd toegang toodevices en services toospecific functionaliteit gebruiken in IoT-Hub. tooget autorisatie tooconnect tooIoT Hub, apparaten en services moeten zijn ondertekend met een gedeelde toegang of de symmetrische sleutel beveiligingstokens verzenden. Deze sleutels worden opgeslagen met een apparaat-id in het identiteitenregister Hallo.

Een token dat is ondertekend met een gedeelde toegang sleutel verleent toegang tooall Hallo functionaliteit die is gekoppeld aan gedeelde Hallo beleid toegangsmachtigingen. Een token die is ondertekend met een apparaat-id symmetrische sleutel alleen verleent Hallo **DeviceConnect** machtiging voor Hallo apparaat-id die is gekoppeld.

Hallo-beveiligingstoken heeft Hallo volgende indeling:

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

Hier volgen Hallo verwachte waarden:

| Waarde | Beschrijving |
| --- | --- |
| {handtekening} |Een tekenreeks van de handtekening HMAC SHA256 Hallo vorm: `{URL-encoded-resourceURI} + "\n" + expiry`. **Belangrijke**: Hallo-sleutel is gedecodeerd van base64 en gebruikt als sleutel tooperform Hallo HMAC SHA256 berekening. |
| {resourceURI} |De voorvoegsels van URI (door het segment) Hallo-eindpunten die toegankelijk zijn met dit token, beginnen met de naam van de host van Hallo iothub (geen protocol). Bijvoorbeeld: `myHub.azure-devices.net/devices/device1` |
| {verstrijken} |UTF8-tekenreeksen voor het aantal seconden sinds Hallo epoche 00:00:00 UTC op 1 januari 1970. |
| {{URL-codering-resourceURI} |Lagere case URL-codering van Hallo kleine letters resource-URI |
| {policyName} |Hallo-naam van Hallo gedeelde toegang beleid toowhich die dit token verwijst. Ontbrekende als verwijst Hallo token toodevice register referenties. |

**Opmerking van het voorvoegsel**: Hallo de voorvoegsels van URI wordt berekend door het segment en niet door teken. Bijvoorbeeld `/a/b` is een voorvoegsel voor `/a/b/c` maar niet voor `/a/bc`.

Hallo volgende Node.js fragment toont een aangeroepen functie **generateSasToken** dat berekent de token van invoer Hallo Hallo `resourceUri, signingKey, policyName, expiresInMins`. Hallo volgende secties bevatten informatie over hoe de gebruiksvoorbeelden voor tooinitialize Hallo andere invoer voor andere Hallo-token.

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

Als een vergelijking hello gelijkwaardige Python-code toogenerate die een beveiligingstoken is:

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
> Aangezien Hallo geldigheid van het Hallo-token is gevalideerd op de machines IoT Hub, moet Hallo afwijking van de klok Hallo van Hallo-machine die Hallo token genereert minimaal zijn.

### <a name="use-sas-tokens-in-a-device-app"></a>SAS-tokens gebruiken in een apparaat-app

Er zijn twee manieren tooobtain **DeviceConnect** machtigingen met IoT Hub met beveiligingstokens: gebruik een [symmetrische apparaatsleutel van Hallo identiteitsregister](#use-a-symmetric-key-in-the-identity-registry), of gebruik een [gedeelde toegangssleutel](#use-a-shared-access-policy).

Houd er rekening mee dat alle functionaliteit die toegankelijk is vanaf apparaten wordt blootgesteld aan het ontwerp voor eindpunten met voorvoegsel `/devices/{deviceId}`.

> [!IMPORTANT]
> Hallo apparaat identiteit symmetrische sleutel maakt gebruik van de enige manier Hallo dat IoT Hub een specifiek apparaat moeten worden geverifieerd. In gevallen wanneer een beleid voor gedeelde toegang gebruikte tooaccess apparaatfunctionaliteit is, Hallo oplossing moet rekening houden Hallo onderdeel Hallo beveiligingstoken als een vertrouwde subonderdeel uitgeven.

Hallo apparaat gerichte eindpunten zijn (ongeacht Hallo protocol):

| Eindpunt | Functionaliteit |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |Apparaat-naar-cloud-berichten verzenden. |
| `{iot hub host name}/devices/{deviceId}/devicebound` |Cloud-naar-apparaat-berichten ontvangen. |

### <a name="use-a-symmetric-key-in-hello-identity-registry"></a>Een symmetrische sleutel in het identiteitenregister hello gebruiken

Wanneer u een apparaat-id symmetrische sleutel toogenerate een token, Hallo policyName (`skn`) element van het Hallo-token wordt weggelaten.

Bijvoorbeeld, een token gemaakt tooaccess functionaliteit voor alle apparaten moeten hebben Hallo volgende parameters:

* resource-URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* de handtekeningsleutel: een symmetrische sleutel voor Hallo `{device id}` identiteit
* Er is geen naam van beleid
* elk gewenst moment verlopen.

Een voorbeeld met behulp van Node.js-functie vóór Hallo is:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

Hallo-resultaat dat toegang tooall functionaliteit voor device1 verleent, zou zijn:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> Het is mogelijk toogenerate een SAS-token met Hallo .NET [apparaat explorer] [ lnk-device-explorer] hulpprogramma of platformoverschrijdende, op basis van een knooppunt Hallo [iothub explorer] [ lnk-iothub-explorer] opdrachtregelprogramma.

### <a name="use-a-shared-access-policy"></a>Gebruik een beleid voor gedeelde toegang

Wanneer u een token van een gedeeld toegangsbeleid maken, instellen Hallo `skn` toohello naam van het Hallo-beleid. Dit beleid moet verlenen Hallo **DeviceConnect** machtiging.

Hallo twee hoofdscenario's voor het gebruik van de functionaliteit voor gedeelde toegang beleid tooaccess apparaten zijn:

* [cloud protocol gateways][lnk-endpoints],
* [token services] [ lnk-custom-auth] tooimplement aangepaste verificatieschema's gebruikt.

Sinds Hallo verleent beleid voor gedeelde toegang mogelijk toegang tooconnect als een apparaat is belangrijk toouse Hallo juiste resource URI bij het maken van beveiligingstokens. Deze instelling is vooral belangrijk voor token-services, waarvoor tooscope Hallo token tooa specifieke apparaat Hallo resource-URI gebruikt. Dit punt is minder relevant voor gateways protocol zoals ze zijn verkeer voor alle apparaten al op de volgende manier regelt.

Als u bijvoorbeeld een token service met behulp van vooraf gemaakte Hallo gedeeld toegangsbeleid aangeroepen **apparaat** zou maken van een token Hello volgende parameters:

* resource-URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,
* de handtekeningsleutel: een van de sleutels Hallo Hallo `device` -beleid
* de naam van beleid: `device`,
* elk gewenst moment verlopen.

Een voorbeeld met behulp van Node.js-functie vóór Hallo is:

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

Hallo-resultaat dat toegang tooall functionaliteit voor device1 verleent, zou zijn:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

Een protocolgateway kan Hallo dezelfde token voor alle apparaten eenvoudigweg Hallo resource-URI te gebruiken`myhub.azure-devices.net/devices`.

### <a name="use-security-tokens-from-service-components"></a>Gebruik de beveiligingstokens van de onderdelen van service

Serviceonderdelen kunnen alleen beveiligingstokens met behulp van beleid voor gedeelde toegang Hallo relevante machtigingen verlenen zoals hierboven is gegenereerd.

Hier volgt Hallo servicefuncties op Hallo eindpunten:

| Eindpunt | Functionaliteit |
| --- | --- |
| `{iot hub host name}/devices` |Maken, bijwerken, ophalen en verwijderen van apparaat-id's. |
| `{iot hub host name}/messages/events` |Apparaat-naar-cloud-berichten ontvangen. |
| `{iot hub host name}/servicebound/feedback` |Feedback voor cloud-naar-apparaat-berichten ontvangen. |
| `{iot hub host name}/devicebound` |Cloud-naar-apparaat-berichten verzenden. |

Als u bijvoorbeeld een service genereren met behulp van vooraf gemaakte Hallo gedeeld toegangsbeleid aangeroepen **registryRead** zou maken van een token Hello volgende parameters:

* resource-URI: `{IoT hub name}.azure-devices.net/devices`,
* de handtekeningsleutel: een van de sleutels Hallo Hallo `registryRead` -beleid
* de naam van beleid: `registryRead`,
* elk gewenst moment verlopen.

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

Hallo resultaat toegang tooread alle apparaat-id's verlenen wilt, zou zijn:

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a>Ondersteunde X.509-certificaten

U kunt een x.509-certificaat tooauthenticate een apparaat gebruiken met IoT Hub. Certificaten zijn onder andere:

* **Een bestaand X.509-certificaat**. Een apparaat mogelijk al een X.509-certificaat dat is gekoppeld. Hallo-apparaat kunt u dit certificaat tooauthenticate gebruiken met IoT Hub.
* **Een automatisch gegenereerd en zelfondertekend certificaat X-509**. Een fabrikant of interne deployer kunt deze certificaten genereren en en opslaan Hallo bijbehorende persoonlijke sleutel (certificaat) op Hallo-apparaat. U kunt hulpprogramma's gebruiken zoals [OpenSSL] [ lnk-openssl] en [Windows SelfSignedCertificate] [ lnk-selfsigned] hulpprogramma voor dit doel.
* **X.509-certificaat voor ondertekening van CA**. tooidentify een apparaat en deze kan worden geverifieerd met IoT Hub, kunt u een X.509-certificaat gegenereerd en ondertekend door een certificeringsinstantie (CA). IoT Hub controleert alleen of die Hallo-vingerafdruk die zijn gepresenteerd overeenkomt met de vingerafdruk Hallo geconfigureerd. IotHub biedt Hallo certificaatketen niet valideren.

Een apparaat kan gebruikmaken van een X.509-certificaat of een beveiligingstoken voor verificatie, maar niet beide.

### <a name="register-an-x509-certificate-for-a-device"></a>Een X.509-certificaat voor een apparaat registreren

Hallo [Azure IoT Service SDK voor C#] [ lnk-service-sdk] (versie 1.0.8+) biedt ondersteuning voor het registreren van een apparaat dat gebruikmaakt van een X.509-certificaat voor verificatie. Andere API's zoals importeren/exporteren van apparaten bieden ook ondersteuning voor X.509-certificaten.

### <a name="c-support"></a>C\# ondersteuning

Hallo **RegistryManager** klasse biedt een tooregister programmatische manier een apparaat. In het bijzonder Hallo **AddDeviceAsync** en **UpdateDeviceAsync** methoden kunt u tooregister en een Hallo id-register IoT Hub-apparaat bijwerken. Deze twee methoden maken gebruik van een **apparaat** exemplaar als invoer. Hallo **apparaat** klasse bevat een **verificatie** eigenschap waarmee u toospecify primaire en secundaire x.509-certificaatvingerafdrukken. Hallo vingerafdruk vertegenwoordigt een SHA-1-hash van Hallo X.509-certificaat (met behulp van binaire codering DER opgeslagen). U hebt Hallo-optie voor het opgeven van de vingerafdruk van een primaire of een secundaire vingerafdruk of beide. Primaire en secundaire vingerafdrukken zijn ondersteunde toohandle certificaat overschakeling van de scenario's.

> [!NOTE]
> IoT Hub geen vereist of Hallo volledige x.509-certificaat, alleen de vingerafdruk van het Hallo wordt opgeslagen.

Hier volgt een voorbeeld van C\# code codefragment tooregister een apparaat met een X.509-certificaat:

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

### <a name="use-an-x509-certificate-during-run-time-operations"></a>Gebruik van een X.509-certificaat tijdens runtime-bewerkingen

Hallo [Azure IoT-device SDK voor .NET] [ lnk-client-sdk] (versie 1.0.11+) ondersteunt Hallo gebruik van X.509-certificaten.

### <a name="c-support"></a>C\# ondersteuning

Hallo klasse **DeviceAuthenticationWithX509Certificate** ondersteunt het maken van Hallo **DeviceClient** exemplaren met behulp van een X.509-certificaat. Hallo X.509-certificaat moet zich in hello (ook wel PKCS #12) PFX-indeling die Hallo persoonlijke sleutel bevat.

Hier volgt een voorbeeld-codefragment:

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a>Verificatie van aangepast apparaat

U kunt Hallo IoT Hub [identiteitsregister] [ lnk-identity-registry] tooconfigure per apparaat beveiligingsreferenties en toegang beheren met behulp van [tokens] [ lnk-sas-tokens] . Als een IoT-oplossing al een aangepaste identiteit register en/of de verificatie-schema heeft, kunt u een *token service* toointegrate deze infrastructuur met IoT Hub. Op deze manier kunt u andere IoT-functies in uw oplossing.

Een service voor beveiligingstokens is een aangepaste cloudservice. Dit maakt gebruik van een IoT-Hub *gedeeld toegangsbeleid* met **DeviceConnect** machtigingen toocreate *binnen het bereik van apparaat* tokens. Deze tokens inschakelen voor een apparaat tooconnect tooyour IoT-hub.

![Stappen voor het Hallo Tokenservice patroon][img-tokenservice]

Hieronder worden de belangrijkste stappen Hallo van Hallo Tokenservice patroon:

1. Maken van een Iothub gedeeld toegangsbeleid met **DeviceConnect** machtigingen voor uw IoT-hub. U kunt dit beleid kunt maken in Hallo [Azure-portal] [ lnk-management-portal] of via een programma. Hallo token service maakt gebruik van dit beleid toosign Hallo tokens wordt gemaakt.
1. Wanneer een apparaat tooaccess uw IoT-hub moet, wordt het token van een ondertekende aanvraagt van uw service voor beveiligingstokens. Hallo-apparaat kunt verifiëren met uw apparaat-id voor aangepaste identiteit register/verificatie schema toodetermine Hallo dat Hallo token service toocreate Hallo token gebruikt.
1. Hallo token service retourneert een token. Hallo token wordt gemaakt met `/devices/{deviceId}` als `resourceURI`, met `deviceId` als Hallo-apparaat wordt geverifieerd. Hallo token service gebruikt Hallo gedeelde beleid tooconstruct Hallo toegangstoken.
1. Hallo-apparaat gebruikt Hallo token rechtstreeks met de Hallo iothub.

> [!NOTE]
> U kunt .NET-klasse Hallo [SharedAccessSignatureBuilder] [ lnk-dotnet-sas] of Java-klasse Hallo [IotHubServiceSasToken] [ lnk-java-sas] toocreate een token in uw token service.

Hallo Tokenservice kunt Hallo token verloopt desgewenst instellen. Wanneer het Hallo-token is verlopen, servers Hallo IoT-hub Hallo apparaatverbinding. Hallo-apparaat moet vervolgens een nieuw token aanvragen van de service voor beveiligingstokens Hallo. Een korte verlooptijd verhoogt de belasting op Hallo-apparaat en de beveiligingstokenservice Hallo Hallo.

Voor een apparaat tooconnect tooyour hub, moet u nog steeds deze toevoegen toohello id-register IoT-Hub: hoewel Hallo apparaat van een token en niet een apparaat sleutel tooconnect gebruikmaakt. Daarom kunt u toegangsbeheer voor toouse per apparaat doorgaan met in- of uitschakelen van apparaat-id's in Hallo [identiteitsregister][lnk-identity-registry]. Deze aanpak vermindert Hallo risico's van het gebruik van tokens met lange verstrijken tijden.

### <a name="comparison-with-a-custom-gateway"></a>Vergelijking met een aangepaste gateway

Hallo Tokenservice patroon is Hallo aanbevolen manier tooimplement een aangepaste identiteit register/verificatieschema met IoT Hub. Dit patroon wordt aanbevolen omdat IoT Hub toohandle blijft de meeste Hallo oplossing verkeer. Echter, als aangepaste Hallo-verificatieschema dus met Hallo-protocol verweven is, hebt u mogelijk nodig een *aangepaste gateway* tooprocess alle verkeer Hallo. Het gebruik van een voorbeeld van een dergelijk scenario[Transport Layer Security (TLS) en vooraf gedeelde sleutels (PSKs)][lnk-tls-psk]. Zie voor meer informatie, Hallo [protocolgateway] [ lnk-protocols] onderwerp.

## <a name="reference-topics"></a>De onderwerpen waarnaar wordt verwezen:

Hallo bieden volgende naslagonderwerpen u meer informatie over het beheren van toegang tooyour iothub.

## <a name="iot-hub-permissions"></a>Machtigingen van de IoT-Hub

Hallo bevat volgende tabel Hallo machtigingen kunt u toocontrol toegang tooyour IoT-hub.

| Machtiging | Opmerkingen |
| --- | --- |
| **RegistryRead** |Verleent leestoegang toohello id-register. Zie voor meer informatie [identiteitsregister][lnk-identity-registry]. <br/>Deze machtiging wordt gebruikt door de back-end-cloudservices. |
| **RegistryReadWrite** |Verleent lees- en schrijftoegang toohello id-register. Zie voor meer informatie [identiteitsregister][lnk-identity-registry]. <br/>Deze machtiging wordt gebruikt door de back-end-cloudservices. |
| **ServiceConnect** |Verleent toegang tot toocloud service gerichte communicatie en controle-eindpunten. <br/>Verleent toestemming tooreceive apparaat-naar-cloud-berichten verzenden cloud-naar-apparaat-berichten en ophalen Hallo levering bevestigingen overeenkomt. <br/>Verleent toestemming tooretrieve levering van bevestigingen voor het bestand uploadt. <br/>Verleent toestemming tooaccess apparaat horende tooupdate labels gewenste eigenschappen gemelde eigenschappen ophalen en uitvoeren van query's. <br/>Deze machtiging wordt gebruikt door de back-end-cloudservices. |
| **DeviceConnect** |Verleent toegang tot toodevice gerichte eindpunten. <br/>Verleent toestemming toosend apparaat-naar-cloud-berichten en cloud-naar-apparaat-berichten ontvangen. <br/>Verleent toestemming tooperform uploaden bestand vanaf een apparaat. <br/>Verleent toestemming tooreceive twin gewenst eigenschap apparaatmeldingen en update apparaat twin gemelde eigenschappen. <br/>Verleent toestemming tooperform bestand uploadt. <br/>Deze machtiging wordt gebruikt door apparaten. |

## <a name="additional-reference-material"></a>Aanvullende referentiemateriaal

Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:

* [IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.
* [Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's en beperking gedrag die van toepassing zijn toohello service IoT Hub.
* [Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub SDK's.
* [IoT Hub-querytaal] [ lnk-query] Hallo querytaal tooretrieve informatie uit IoT Hub over uw apparaat horende taken kunt u hierin wordt beschreven.
* [Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe toocontrol toegang krijgen tot IoT Hub, kunt u mogelijk geïnteresseerd in de volgende onderwerpen voor IoT Hub developer guide Hallo:

* [Gebruik Apparaatstatus horende toosynchronize en configuraties][lnk-devguide-device-twins]
* [Een directe methode aangeroepen voor een apparaat][lnk-devguide-directmethods]
* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub zelfstudies te volgen:

* [Aan de slag met Azure IoT Hub][lnk-getstarted-tutorial]
* [Hoe toosend cloud-naar-apparaat met IoT Hub berichten][lnk-c2d-tutorial]
* [Hoe tooprocess IoT Hub apparaat-naar-cloud-berichten][lnk-d2c-tutorial]

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
