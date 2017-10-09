---
title: aaaOverview van verificatie en model van Azure Event Hubs | Microsoft Docs
description: Verificatie en beveiliging model overzicht van Event Hubs.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 93841e30-0c5c-4719-9dc1-57a4814342e7
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/30/2017
ms.author: sethm;clemensv
ms.openlocfilehash: e57ccda33e5ee20e635487cf91d9e8af594d3bd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-authentication-and-security-model-overview"></a>Verificatie en beveiliging model overzicht van Event Hubs
Hello Azure Event Hubs beveiligingsmodel aan Hallo volgens de vereisten voldoet:

* Alleen clients die geldige referenties kunnen gegevens tooan event hub te verzenden.
* Een client kan een andere client niet imiteren.
* Een rogue client worden verzenden van gegevens tooan event hub geblokkeerd.

## <a name="client-authentication"></a>Clientverificatie
Hallo Event Hubs-beveiligingsmodel is gebaseerd op een combinatie van [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) tokens en *gebeurtenisuitgevers*. Een gebeurtenisuitgever definieert een virtuele-eindpunt voor een event hub. Hallo publisher kan alleen worden gebruikt toosend berichten tooan event hub. Het is niet mogelijk tooreceive berichten van een uitgever.

Normaal gesproken een event hub maakt gebruik van een uitgever per client. Alle berichten die tooany met Hallo uitgevers van een event hub worden verzonden zijn in de wachtrij binnen event hub. Uitgevers inschakelen verfijnd toegangsbeheer en beperking.

Elke client Event Hubs is een unieke token, dat geüploade toohello client is toegewezen. Hallo-tokens worden geproduceerd, zodat elke unieke token toegang tooa andere unieke uitgever verleent. Een client die beschikken over een token kan alleen tooone publisher, maar er is geen andere uitgever verzenden. Als meerdere clients delen hetzelfde token vervolgens elk van deze Hallo deelt een uitgever.

Niet aanbevolen, is maar het mogelijk tooequip apparaten met tokens die directe toegang tooan event hub verlenen. Elk apparaat met dit token verzenden rechtstreeks in de event hub berichten. Dergelijk apparaat geen onderwerp toothrottling worden. Hallo-apparaat kan niet verder worden gebeurd toothat event hub verzendt.

Alle tokens zijn ondertekend met een SAS-sleutel. Normaal gesproken alle tokens zijn ondertekend met Hallo dezelfde sleutel. Clients zich niet op de hoogte van de sleutel Hallo; Dit voorkomt dat andere clients die produceren van tokens.

### <a name="create-hello-sas-key"></a>Hallo SAS-sleutel maken

Bij het maken van een naamruimte Event Hubs Hallo service genereert een 256-bits SAS-sleutel met de naam **RootManageSharedAccessKey**. Deze sleutel verleent verzenden, luisteren en rechten toohello naamruimte wilt beheren. U kunt ook aanvullende sleutels maken. Het is raadzaam het produceren van een sleutel die verleent machtigingen toohello specifieke event hub verzendt. Hallo rest van dit onderwerp, wordt ervan uitgegaan dat u deze sleutel naam **EventHubSendKey**.

Hallo voorbeeld te volgen, wordt er een sleutel verzenden alleen-lezen gemaakt bij het maken van Hallo event hub:

```csharp
// Create namespace manager.
string serviceNamespace = "YOUR_NAMESPACE";
string namespaceManageKeyName = "RootManageSharedAccessKey";
string namespaceManageKey = "YOUR_ROOT_MANAGE_SHARED_ACCESS_KEY";
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, string.Empty);
TokenProvider td = TokenProvider.CreateSharedAccessSignatureTokenProvider(namespaceManageKeyName, namespaceManageKey);
NamespaceManager nm = new NamespaceManager(namespaceUri, namespaceManageTokenProvider);

// Create event hub with a SAS rule that enables sending toothat event hub
EventHubDescription ed = new EventHubDescription("MY_EVENT_HUB") { PartitionCount = 32 };
string eventHubSendKeyName = "EventHubSendKey";
string eventHubSendKey = SharedAccessAuthorizationRule.GenerateRandomKey();
SharedAccessAuthorizationRule eventHubSendRule = new SharedAccessAuthorizationRule(eventHubSendKeyName, eventHubSendKey, new[] { AccessRights.Send });
ed.Authorization.Add(eventHubSendRule); 
nm.CreateEventHub(ed);
```

### <a name="generate-tokens"></a>Genereren van tokens

U kunt tokens met Hallo SAS-sleutel genereren. U moet slechts één token per client wordt gemaakt. Tokens kunnen vervolgens worden geproduceerd met behulp van de volgende methode Hallo. Alle tokens worden gegenereerd met behulp van Hallo **EventHubSendKey** sleutel. Elke token is een unieke URI toegewezen.

```csharp
public static string SharedAccessSignatureTokenProvider.GetSharedAccessSignature(string keyName, string sharedAccessKey, string resource, TimeSpan tokenTimeToLive)
```

Wanneer u deze methode aanroept, Hallo URI moet worden opgegeven als `//<NAMESPACE>.servicebus.windows.net/<EVENT_HUB_NAME>/publishers/<PUBLISHER_NAME>`. Voor alle tokens Hallo URI is identiek zijn, met uitzondering van Hallo `PUBLISHER_NAME`, die moeten verschillend zijn voor elk token. In het ideale geval `PUBLISHER_NAME` vertegenwoordigt Hallo-ID van Hallo-client die de token die ontvangt.

Deze methode genereert een token met Hallo structuur te volgen:

```csharp
SharedAccessSignature sr={URI}&sig={HMAC_SHA256_SIGNATURE}&se={EXPIRATION_TIME}&skn={KEY_NAME}
```

Hallo token verlooptijd is in seconden van 1 januari 1970 opgegeven. Hallo Hieronder volgt een voorbeeld van een token:

```csharp
SharedAccessSignature sr=contoso&sig=nPzdNN%2Gli0ifrfJwaK4mkK0RqAB%2byJUlt%2bGFmBHG77A%3d&se=1403130337&skn=RootManageSharedAccessKey
```

Normaal gesproken hebben Hallo tokens een levensduur die er ongeveer als volgt of Hallo levensduur van de client Hallo overschrijdt. Als Hallo client Hallo mogelijkheid tooobtain een nieuw token, kunnen tokens met een kortere levensduur kunnen worden gebruikt.

### <a name="sending-data"></a>Verzenden van gegevens
Zodra het Hallo-tokens zijn gemaakt, wordt elke client ingericht met een eigen unieke token.

Wanneer Hallo-client verzendt de gegevens in een event hub, tags deze de verzendaanvraag met Hallo-token. een aanvaller inbreuk en stelen Hallo-token, Hallo communicatie tussen client hello en Hallo event hub tooprevent moet plaatsvinden via een versleuteld kanaal.

### <a name="blacklisting-clients"></a>Beschermde clients
Als een token wordt gestolen door een aanvaller, kan de aanvaller Hallo Hallo client waarvan de token is gestolen imiteren. Een client beleid wordt gerenderd die client onbruikbaar totdat het een nieuw token die gebruikmaakt van een andere uitgever ontvangt.

## <a name="authentication-of-back-end-applications"></a>Verificatie van de back-end-toepassingen

een beveiligingsmodel dat vergelijkbare toohello model dat wordt gebruikt voor Service Bus-onderwerpen worden de veiligheidsmaatregelen tooauthenticate back-end-toepassingen die Hallo gegevens die worden gegenereerd door clients van Event Hubs, Event Hubs gebruiken. Een consumergroep Event Hubs is gelijkwaardig tooa abonnement tooa Service Bus-onderwerp. Een client kan een consumergroep maken als Hallo aanvraag toocreate Hallo-consumergroep gaat vergezeld van een token dat verleent machtigingen voor Hallo event hub kunt beheren, of voor Hallo naamruimte toowhich Hallo event hub behoort. Een client is toegestaan tooconsume gegevens uit een consumergroep als Hallo ontvangt met de aanvraag vergezeld gaat van een token dat verleent rechten op consumergroep ontvangen, hello event hub, of Hallo naamruimte toowhich Hallo event hub behoort.

Hallo huidige versie van Service Bus biedt SAS regels geen ondersteuning voor afzonderlijke abonnementen. Hallo die dezelfde voor Event Hubs consumer-groepen geldt. SAS-ondersteuning wordt toegevoegd voor beide functies in toekomstige Hallo.

Hallo geen SAS-verificatie voor afzonderlijke consumer-groepen, kunt u SAS sleutels toosecure alle consumergroepen met een gemeenschappelijke sleutel. Deze aanpak kunt een toepassing tooconsume-gegevens uit een aantal Hallo consumer-groepen van een event hub.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Event Hubs, gaat u naar de volgende onderwerpen Hallo:

* [Event Hubs-overzicht]
* [Overzicht van handtekeningen voor gedeelde toegang]
* [Voorbeeldtoepassingen die gebruikmaken van Event Hubs]

[Event Hubs-overzicht]: event-hubs-what-is-event-hubs.md
[Voorbeeldtoepassingen die gebruikmaken van Event Hubs]: https://github.com/Azure/azure-event-hubs/tree/master/samples
[Overzicht van handtekeningen voor gedeelde toegang]: ../service-bus-messaging/service-bus-sas.md

