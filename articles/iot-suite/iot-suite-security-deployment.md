---
title: aaaSecure uw implementatie van het Internet der dingen | Microsoft Docs
description: Dit artikel details hoe toosecure uw IoT-implementatie
services: 
suite: iot-suite
documentationcenter: 
author: YuriDio
manager: timlt
editor: 
ms.assetid: 95c23341-16b0-4954-b3f2-d2e82ab7b367
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: befba8f2009279c2217dcd3496d529139134ec01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-iot-deployment"></a>Uw IoT-implementatie beveiligen
In dit artikel biedt de volgende detailniveau Hallo voor het beveiligen van Hallo op basis van Azure IoT-Internet der dingen (IoT)-infrastructuur. Gedetailleerde gegevens voor het configureren en implementeren van elk onderdeel tooimplementation worden gekoppeld. Het bevat ook vergelijkingen en -keuzes tussen verschillende concurrerende methoden.

Hello Azure IoT implementatie beveiligen kan worden onderverdeeld in drie beveiligingsgebieden na Hallo:

* **Apparaatbeveiliging**: beveiligen Hallo IoT-apparaat terwijl deze is geïmplementeerd in Hallo wilde.
* **Verbindingsbeveiliging**: alle gegevens die worden overgedragen tussen Hallo IoT-apparaat en IoT Hub gezorgd is vertrouwelijk en fraudebestendig.
* **Cloud Security**: de mogelijkheid geven toosecure gegevens terwijl deze doorloopt en wordt opgeslagen in de cloud Hallo.

![Drie beveiligingsgebieden][img-overview]

## <a name="secure-device-provisioning-and-authentication"></a>Beveiligen van mobiele apparaten inrichten en verificatie
Hello Azure IoT Suite beveiligt IoT-apparaten door Hallo volgende twee methoden:

* Door een unieke id van de sleutel (beveiligingstokens) voor elk apparaat kan worden gebruikt door Hallo apparaat toocommunicate Hello IoT Hub.
* Met behulp van een apparaat op [X.509-certificaat] [ lnk-x509] en de persoonlijke sleutel als een manier tooauthenticate Hallo apparaat toohello IoT Hub. Deze verificatiemethode zorgt ervoor dat Hallo persoonlijke sleutel op Hallo-apparaat is niet bekend buiten Hallo-apparaat op elk gewenst moment een hoger niveau van beveiliging bieden.

methode Hello security token biedt verificatie voor elke aanroep van Hallo apparaat tooIoT Hub door een aanroep van de symmetrische sleutel tooeach Hallo koppelen. Verificatie op basis van een X.509 kunt verificatie van een IoT-apparaat op de fysieke laag Hallo als onderdeel van Hallo TLS-verbinding tot stand brengen. Hallo beveiliging op tokens gebaseerde methode kan worden gebruikt zonder Hallo x.509-verificatie een minder veilige patroon is. Hallo keuze tussen Hallo twee methoden wordt voornamelijk bepaald hoe veilig Hallo apparaatverificatie moet toobe en beschikbaarheid van beveiligde opslag op Hallo-apparaat (toostore Hallo persoonlijke sleutel veilig).

## <a name="iot-hub-security-tokens"></a>Beveiligingstokens van IoT Hub
IoT-Hub maakt gebruik van beveiliging tokens tooauthenticate apparaten en services tooavoid, sleutels op Hallo netwerk verzenden. Bovendien zijn beveiligingstokens beperkt in geldigheid en het bereik. Azure IoT SDK's automatisch genereren van tokens zonder speciale configuratie. Sommige scenario's, Hallo gebruiker toogenerate vereisen echter en beveiligingstokens rechtstreeks gebruiken. Het gaat hierbij om direct gebruik van de protocollen MQTT, AMQP of HTTP-verwerkingsinformatie Hallo Hallo of Hallo-implementatie van Hallo Tokenservice patroon.

Meer informatie over het Hallo-structuur van het beveiligingstoken Hallo en het gebruik ervan vindt u in de volgende artikelen Hallo:

* [Security token structuur][lnk-security-tokens]
* [Met SAS-tokens als een apparaat][lnk-sas-tokens]

Elke IoT-Hub heeft een [identiteitsregister] [ lnk-identity-registry] die kunnen worden gebruikt toocreate per apparaat bronnen in Hallo-service, zoals een wachtrij met onderweg cloud-naar-apparaat-berichten en tooallow toegang toohello apparaat gerichte eindpunten. Hallo id-register IoT Hub biedt een veilige opslag van apparaat-id's en sleutels voor een oplossing. Persoon die of groepen van apparaat-id's kunnen worden toegevoegd tooan staan, of een blokkeringslijst, volledige controle toegang tot het apparaat inschakelen. Hallo bevatten volgende artikelen meer details over Hallo-structuur van Hallo id-register en ondersteunde bewerkingen.

[IoT Hub zoals MQTT AMQP en HTTP-protocollen ondersteunt][lnk-protocols]. Elk van deze protocollen beveiligingstokens uit Hallo IoT-apparaat tooIoT Hub anders gebruiken:

* AMQP: SASL zonder opmaak en op basis van Claims AMQP-beveiliging ({policyName}@sas.root. { iothubName} in geval van IoT hub-niveau tokens; Hallo {deviceId} in het geval van tokens binnen het bereik van apparaat).
* MQTT: Pakket wordt gebruikt {deviceId} VERBINDEN als Hallo {ClientId}, {IoThubhostname} / {deviceId} in Hallo **gebruikersnaam** veld en een SAS-token in Hallo **wachtwoord** veld.
* HTTP: Ongeldig token is in de aanvraagheader Hallo-autorisatie.

ID-register IoT Hub kan worden gebruikte tooconfigure per apparaat beveiligingsreferenties en toegangscontrole. Echter, als een IoT-oplossing heeft al een aanzienlijke investering een [aangepast apparaat identiteit register en/of verificatie schema][lnk-custom-auth], kunnen worden geïntegreerd in een bestaande infrastructuur met IoT Hub door het maken van een token service.

### <a name="x509-certificate-based-device-authentication"></a>Verificatie van de X.509-apparaten op basis van certificaten
Hallo gebruik van een [X.509-certificaat op basis van apparaten] [ lnk-protocols] en de bijbehorende persoonlijke en openbare sleutelpaar staat aanvullende verificatie op de fysieke laag Hallo. Hallo persoonlijke sleutel wordt veilig opgeslagen in het Hallo-apparaat en is niet buiten Hallo-apparaat kan worden gedetecteerd. Hallo X.509-certificaat bevat informatie over het Hallo-apparaat, zoals de apparaat-ID en de andere organisatie-gegevens. Een handtekening van het Hallo-certificaat wordt gegenereerd met behulp van de persoonlijke sleutel Hallo.

Inrichting stroom op hoog niveau apparaat:

* Koppelen van een id tooa fysiek apparaat – apparaat-id en/of x.509-certificaat gekoppeld toohello apparaat tijdens apparaat productie of bedrijf stellen.
* Overeenkomende identiteit invoer in IoT Hub-apparaat-id en bijbehorende apparaatgegevens in Hallo id-register IoT Hub maken.
* Vingerafdruk van het x.509-certificaat veilig opslaan in het register van IoT Hub-identiteit.

### <a name="root-certificate-on-device"></a>Basiscertificaat op apparaat
Tijdens het maken van een beveiligde TLS-verbinding met IoT Hub, verifieert Hallo IoT-apparaat met een basiscertificaat dat deel uitmaakt van Hallo apparaat SDK IoT-Hub. Voor Hallo C client SDK Hallo certificaat bevindt zich onder de map Hallo '\\c\\certificaten ' onder de hoofdmap Hallo van Hallo-opslagplaats. Deze basiscertificaten lange levensduur hebben, maar ze nog steeds mogelijk verlopen of worden ingetrokken. Als er is geen manier om bij te werken Hallo-certificaat op Hallo apparaat hello apparaat mogelijk geen verbinding toosubsequently toohello IoT Hub (of een andere cloudservice). Met een basiscertificaat betekent tooupdate Hallo zodra Hallo IoT-apparaat is geïmplementeerd, wordt dit risico effectief beperken.

## <a name="securing-hello-connection"></a>Hallo verbinding beveiligen
Internet-verbinding tussen Hallo IoT-apparaat en IoT Hub is beveiligd met behulp van Hallo Transport Layer Security (TLS) standaard. Azure IoT ondersteunt [TLS 1.2][lnk-tls12], TLS 1.1 en TLS 1.0 in deze volgorde. Ondersteuning voor TLS 1.0 wordt geleverd alleen voor achterwaartse compatibiliteit. Het verdient toouse TLS 1.2 omdat het meeste beveiliging Hallo biedt.

Azure IoT Suite ondersteunt Hallo Cipher Suites in deze volgorde te volgen.

| Coderingssuite | lengte |
| --- | --- |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq. FS 7680 bits RSA) |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq. FS 3072 bits RSA) |128 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq. FS 7680 bits RSA) |256 |
| TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq. FS 3072 bits RSA) |128 |
| TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c) |128 |
| TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35) |256 |
| TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f) |128 |
| TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa) |112 |

## <a name="securing-hello-cloud"></a>Hallo cloud beveiligen
Azure IoT-Hub kunt definitie van [toegangsbeheerbeleid] [ lnk-protocols] voor elke beveiligingssleutel. Hallo set machtigingen toogrant toegang tooeach van IoT-Hub eindpunten volgende wordt gebruikt. Machtigingen beperken Hallo toegang tooan die IOT-Hub op basis van functionaliteit.

* **RegistryRead**. Verleent leestoegang toohello id-register. Zie voor meer informatie [identiteitsregister][lnk-identity-registry].
* **RegistryReadWrite**. Verleent lees- en schrijftoegang toohello id-register. Zie voor meer informatie [identiteitsregister][lnk-identity-registry].
* **ServiceConnect**. Verleent toegang tot toocloud service gerichte communicatie en controle-eindpunten. Bijvoorbeeld, verleent deze machtiging tooback-end cloud services tooreceive apparaat-naar-cloud-berichten en berichten van de cloud naar apparaat verzenden ophalen Hallo levering bevestigingen overeenkomt.
* **DeviceConnect**. Verleent toegang tot toodevice gerichte eindpunten. Toestemming verleent toosend apparaat-naar-cloud-berichten en cloud-naar-apparaat-berichten ontvangen. Deze machtiging wordt gebruikt door apparaten.

Er zijn twee manieren tooobtain **DeviceConnect** machtigingen met IoT Hub met [beveiligingstokens][lnk-sas-tokens]: met een id-sleutel van het apparaat of een gedeelde toegangssleutel. Bovendien is het belangrijk toonote die toegankelijk is vanaf de apparaten van alle functionaliteit wordt blootgelegd door ontwerp voor eindpunten met voorvoegsel `/devices/{deviceId}`.

[Service-onderdelen kunnen alleen beveiligingstokens worden gegenereerd] [ lnk-service-tokens] gebruik gedeeld toegangsbeleid Hallo relevante machtigingen verlenen.

Azure IoT Hub en andere services die deel uitmaken van de oplossing Hallo wellicht toestaan van beheer van gebruikers met behulp van hello Azure Active Directory.

Gegevens ingenomen door Azure IoT Hub kan worden gebruikt door diverse services zoals Azure Stream Analytics en Azure blob-opslag. Deze services toestaan management toegang. Meer informatie over deze services en de beschikbare opties hieronder:

* [Azure Cosmos DB][lnk-docdb]: een schaalbare, volledig geïndexeerd databaseservice voor semi-gestructureerde gegevens die de metagegevens voor Hallo apparaten beheert u inricht, zoals kenmerken, configuratie en beveiligingseigenschappen. Cosmos DB biedt hoge prestaties en hoge gegevensdoorvoer verwerking, schema networkdirect indexeren van gegevens en een uitgebreide SQL-QueryInterface.
* [Azure Stream Analytics][lnk-asa]: realtime stroom wordt verwerkt in de cloud Hallo waarmee u toorapidly ontwikkelen en implementeren van een analyses voordelige oplossing toouncover realtime-inzichten verkrijgen van apparaten, sensoren infrastructuur en toepassingen. Hallo-gegevens van deze volledig beheerde service tooany volume kunnen worden geschaald en toch veel doorvoer, lage latentie en tolerantie kan bereiken.
* [Azure App Services][lnk-appservices]: een cloud platform toobuild krachtige web- en mobiele apps die verbinding toodata overal; in Hallo cloud of on-premises. Aansprekende mobiele apps bouwen voor iOS, Android en Windows. Integreren met uw Software als een Service (SaaS) en de enterprise-toepassingen met out-of-the-box-connectiviteit toodozens van cloud-gebaseerde services en toepassingen van de enterprise. De code in uw favoriete taal en IDE (.NET, Node.js, PHP, Python of Java) toobuild web-apps en API's sneller dan ooit.
* [Logic Apps][lnk-logicapps]: Hallo Logic Apps-functie van Azure App Service helpt bij het integreren van uw IoT-oplossing tooyour bestaande LOB-systemen en workflow-processen automatiseren. Logic Apps kan ontwikkelaars toodesign werkstromen die na een trigger worden gestart en vervolgens een aantal stappen uitgevoerd: regels en acties die krachtige connectors toointegrate met uw bedrijfsprocessen gebruiken. Logic Apps biedt out-of-the-box-connectiviteit tooa vast ecosysteem van SaaS, op basis van cloud en on-premises toepassingen.
* [Azure-blobopslag][lnk-blob]: betrouwbare en voordelige cloud-opslag voor Hallo gegevens die uw apparaten toohello cloud verzendt.

## <a name="conclusion"></a>Conclusie
Dit artikel bevat de mate van details over het ontwerpen en implementeren van een IoT-infrastructuur met behulp van Azure IoT overzicht van de uitvoering. Configureren van elk onderdeel van beveiligde toobe is de sleutel in het beveiligen van Hallo algemene IoT-infrastructuur. Hallo ontwerpbeslissingen die beschikbaar zijn in Azure IoT een bepaalde mate van flexibiliteit en keuze; elke keuze hebben echter beveiligingsgebied. Het is raadzaam dat elk van deze keuzes worden geëvalueerd door een/kosten van het risico-evaluatie.

## <a name="see-also"></a>Zie ook
U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:

* [Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]
* [Veelgestelde vragen over IoT Suite][lnk-faq]

U kunt meer informatie over beveiliging in IoT Hub [besturingselement toegang tooIoT Hub] [ lnk-devguide-security] in Hallo Ontwikkelaarshandleiding voor IoT Hub.


[img-overview]: media/iot-suite-security-deployment/overview.png

[lnk-security-tokens]: ../iot-hub/iot-hub-devguide-security.md#security-token-structure
[lnk-sas-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-protocols]: ../iot-hub/iot-hub-devguide-security.md
[lnk-custom-auth]: ../iot-hub/iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: http://www.itu.int/rec/T-REC-X.509-201210-I/en
[lnk-tls12]: https://tools.ietf.org/html/rfc5246
[lnk-service-tokens]: ../iot-hub/iot-hub-devguide-security.md#use-security-tokens-from-service-components
[lnk-docdb]: https://azure.microsoft.com/services/documentdb/
[lnk-asa]: https://azure.microsoft.com/services/stream-analytics/
[lnk-appservices]: https://azure.microsoft.com/services/app-service/
[lnk-logicapps]: https://azure.microsoft.com/services/app-service/logic/
[lnk-blob]: https://azure.microsoft.com/services/storage/

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-devguide-security]: ../iot-hub/iot-hub-devguide-security.md
