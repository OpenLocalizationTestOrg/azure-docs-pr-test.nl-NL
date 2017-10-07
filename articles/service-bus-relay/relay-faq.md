---
title: aaaAzure Relay Veelgestelde vragen | Microsoft Docs
description: Krijg antwoorden toosome Veelgestelde vragen over Azure Relay.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>Veelgestelde vragen over Azure Relay

In dit artikel worden enkele veelgestelde vragen (FAQ's) over [Azure Relay](https://azure.microsoft.com/services/service-bus/). Raadpleeg voor algemene Azure-prijzen en -ondersteuning informatie, [Azure ondersteunen Veelgestelde vragen over](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions"></a>Algemene vragen
### <a name="what-is-azure-relay"></a>Wat is Azure Relay?
Hallo [Azure Relay-service](relay-what-is-it.md) vereenvoudigt uw hybride toepassingen doordat u veiliger zichtbaar services die zich in een zakelijke enterprise netwerk toohello openbare cloud bevinden. Hallo-services kan worden blootgesteld zonder de firewallverbinding van een te openen en zonder Tussenkomende wijzigingen tooa bedrijfsnetwerkinfrastructuur.

### <a name="what-is-a-relay-namespace"></a>Wat is een Relay-naamruimte?
Een [naamruimte](relay-create-namespace-portal.md) een scoping container die u tooaddress Relay-resources in uw toepassing gebruiken kunt is. U moet een naamruimte toouse Relay maken. Dit is een van de eerste stappen Hallo in aan de slag.

### <a name="what-happened-tooservice-bus-relay-service"></a>Welke happened tooService service Bus Relay?
Hallo eerder Service Bus Relay-service met de naam heet nu WCF Relay. U kunt blijven toouse deze service zoals gebruikelijk. Hallo hybride verbindingen functie is een bijgewerkte versie van een service die wordt is getransplanteerd van Azure BizTalk Services. WCF Relay en hybride verbindingen blijven toobe ondersteund.

## <a name="pricing"></a>Prijzen
Deze sectie antwoorden enkele veelgestelde vragen over Hallo Relay structuur prijzen. U kunt ook zien [Veelgestelde vragen over Azure-ondersteuning](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure prijsinformatie. Zie voor meer informatie over prijzen voor Relay [Service Bus prijsinformatie][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>Hoe u kosten in rekening gebracht voor hybride verbindingen en WCF Relay?
Zie voor meer informatie over prijzen voor Relay Hallo [hybride verbindingen en WCF-Relays] [ Pricing overview] tabel op Hallo Service Bus detailpagina met prijzen. Bovendien toohello prijzen genoteerd op die pagina's worden in rekening gebracht voor de bijbehorende gegevensoverdracht voor uitgaande buiten Hallo datacenter waarin de toepassing is ingericht.

### <a name="how-am-i-billed-for-hybrid-connections"></a>Hoe ben ik in rekening gebracht voor hybride verbindingen?
Hier volgen drie facturering voorbeeldscenario's voor hybride verbindingen:

*   Scenario 1:
    *   U hebt één listener, zoals een exemplaar van hybride verbindingen Manager geïnstalleerd en continu uitgevoerd voor de hele maand Hallo Hallo.
    *   U verzenden 3 GB aan gegevens via de verbinding Hallo tijdens Hallo maand. 
    *   De totale kosten is $5.
*   Scenario 2:
    *   U hebt één listener, zoals een exemplaar van hybride verbindingen Manager geïnstalleerd en continu uitgevoerd voor de hele maand Hallo Hallo.
    *   U verzenden 10 GB aan gegevens via de verbinding Hallo tijdens Hallo maand.
    *   De totale kosten is $7,50. $5 voor Hallo verbinding is en eerste 5 GB + $2,50 voor Hallo aanvullende 5 GB aan gegevens.
*   Scenario 3:
    *   U hebt twee instanties, A en B, hybride verbindingen Manager geïnstalleerd en continu uitgevoerd voor de hele maand Hallo Hallo.
    *   U verzenden 3 GB aan gegevens via een verbinding in Hallo maand.
    *   U verzenden 6 GB aan gegevens via verbinding B tijdens Hallo maand.
    *   De totale kosten is $10,50. Dat is $5 voor de verbinding een + $5 voor verbinding B + $0,50 (voor Hallo zesde gigabyte op verbinding B).

Houd er rekening mee dat Hallo gebruikt in Hallo voorbeelden van toepassing zijn alleen tijdens de evaluatieperiode voor Hallo hybride verbindingen. Prijzen zijn onderwerp toochange bij algemene beschikbaarheid van hybride verbindingen.

### <a name="how-are-hours-calculated-for-relay"></a>Hoe worden uren berekend voor Relay?

Relay WCF is alleen beschikbaar in Standard-laag naamruimten. Prijzen en [verbinding quota](../service-bus-messaging/service-bus-quotas.md) voor anders relays zijn niet gewijzigd. Dit betekent dat relays gaan toobe kosten in rekening gebracht op basis van het aantal berichten (geen bewerkingen) Hallo en uren relay. Zie voor meer informatie, Hallo ['Hybride verbindingen en WCF Relays'](https://azure.microsoft.com/pricing/details/service-bus/) tabel op Hallo detailpagina met prijzen.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>Wat gebeurt er als ik heb meer dan één listener verbonden tooa specifieke relay?
In sommige gevallen kan een enkele relay meerdere verbonden listeners hebben. Een relay wordt beschouwd als open wanneer ten minste één relay-listener verbonden tooit is. Toe te voegen listeners tooan open relay resultaten in extra doorgifte-uren. aantal Hallo van relay afzenders (clients die worden aangeroepen of verzenden berichten toorelays) die zijn verbonden tooa relay heeft geen invloed op Hallo berekening van de doorgifte-uren.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>Hoe wordt de Hallo berichten meter voor WCF-Relays berekend?
(**Dit geldt alleen tooWCF relays. Berichten zijn geen kosten voor hybride verbindingen.** )

In het algemeen factureerbare berichten voor relays zijn berekend met behulp van Hallo dezelfde methode die wordt gebruikt voor brokered entiteiten (wachtrijen, onderwerpen en abonnementen) die eerder zijn beschreven. Er zijn echter enkele belangrijke verschillen.

Verzenden van een bericht tooa Service Bus relay wordt behandeld als een 'volledige via' verzenden toohello relay listener die het Hallo-bericht ontvangt. Dit wordt niet beschouwd als een verzenden bewerking toohello Service Bus relay, gevolgd door een levering toohello relay-listener. Een aanroep van aanvragen / antwoorden stijl service (van omhoog too64 KB) op basis van de resultaten van een relay-listener in twee factureerbare berichten: één factureerbare bericht voor het Hallo-aanvraag en één factureerbare bericht voor antwoord Hallo (ervan uitgaande antwoord Hallo ook 64 KB of kleiner). Dit is anders dan het gebruik van een wachtrij toomediate tussen een client en een service. Als u een wachtrij toomediate tussen een client en een service, vereist hello aanvragen / antwoorden patroon een aanvraag verzenden toohello wachtrij, gevolgd door een wachtrij halen/levering van Hallo wachtrij toohello-service. Dit wordt gevolgd door een antwoord verzenden tooanother wachtrij en een wachtrij halen/levering van die wachtrij toohello-client. Met behulp van dezelfde veronderstellingen gedurende (omhoog too64 KB grootte) Hallo via Hallo wachtrij patroon levert 4 factureerbare berichten. U wordt gefactureerd voor tweemaal Hallo aantal berichten tooimplement Hallo die hetzelfde patroon dat u doen met behulp van de relay. Natuurlijk, zijn er voordelen toousing wachtrijen tooachieve dit patroon, zoals duurzaamheid en load leveling. Deze voordelen mogelijk extra kosten Hallo rechtvaardigen.

Relays die worden geopend met behulp van Hallo **netTCPRelay** WCF binding berichten behandelen niet als afzonderlijke berichten, maar als een stroom van gegevens die binnenkomen via Hallo-systeem. Wanneer u deze binding gebruikt, alleen hebben hello afzender en de listener inzicht in Hallo framing Hallo afzonderlijke berichten worden verzonden en ontvangen. Voor relays die gebruikmaken van Hallo **netTCPRelay** binding, alle gegevens wordt behandeld als een stroom voor het berekenen van factureerbare berichten. In dit geval berekent Service Bus Hallo totale hoeveelheid gegevens verzonden of ontvangen via elke afzonderlijke relay op basis van de 5 minuten. Onderverdeeld die totale hoeveelheid gegevens door 64 KB toodetermine Hallo aantal factureerbare berichten voor die relay in die periode.

## <a name="quotas"></a>Quota
| De naam van de quota | Bereik | Type | Gedrag wanneer overschreden | Waarde |
| --- | --- | --- | --- | --- |
| Gelijktijdige listeners op een relay |Entiteit |Statisch |De volgende aanvragen voor aanvullende verbindingen worden geweigerd en een uitzondering is ontvangen door Hallo code aanroepen. |25 |
| Gelijktijdige relay-listeners |Hele systeem |Statisch |De volgende aanvragen voor aanvullende verbindingen worden geweigerd en een uitzondering is ontvangen door Hallo code aanroepen. |2,000 |
| Gelijktijdige relay-verbindingen per alle relay-eindpunten in de naamruimte van een service |Hele systeem |Statisch |- |5,000 |
| Relay-eindpunten per Servicenaamruimte |Hele systeem |Statisch |- |10.000 |
| Berichtgrootte voor [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) en [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) doorstuurt |Hele systeem |Statisch |Binnenkomende berichten die groter is dan deze quota worden geweigerd en een uitzondering is ontvangen door Hallo code aanroepen. |64 kB |
| Berichtgrootte voor [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) en [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) doorstuurt |Hele systeem |Statisch |- |Onbeperkt |

### <a name="does-relay-have-any-usage-quotas"></a>Heeft Relay quota voor gebruik?
Microsoft stelt voor elke cloudservice wordt standaard een cumulatieve maandelijkse gebruiksgegevens van die is berekend voor alle abonnementen voor een klant. We begrijpen dat op tijdstippen uw behoeften, deze limieten overschrijdt mogelijk. U kunt contact opnemen met customer support op elk gewenst moment zodat we kunnen uw behoeften te begrijpen en pas deze limieten op de juiste wijze. Service bus zijn Hallo gebruiksgegevens quota als volgt uit:

* 5 miljard berichten
* 2 miljoen relayuren

Hoewel we Hallo rechts toodisable een account dat groter is dan de maandelijkse quota voor gebruik reserveren, bieden we een e-mailmelding en maken we meerdere pogingen toocontact Hallo klant alvorens een actie te ondernemen. Klanten die groter is dan deze quota zijn nog steeds zelf verantwoordelijk voor extra kosten.

### <a name="naming-restrictions"></a>Beperkingen voor naamgeving
De naam van een Relay-naamruimte moet tussen 6 en 50 tekens lang zijn.

## <a name="subscription-and-namespace-management"></a>Abonnement en de naamruimte management
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Hoe Migreer ik een naamruimte tooanother Azure-abonnement?

een naamruimte van een Azure-abonnement tooanother abonnement toomove, kunt u beide Hallo gebruik [Azure-portal](https://portal.azure.com) of PowerShell-opdrachten gebruiken. een naamruimte tooanother abonnement toomove, Hallo-naamruimte moet al actief zijn. Hallo gebruiker Hallo opdrachten uit te voeren, moet een beheerder op beide Hallo bron en doel-abonnementen.

#### <a name="azure-portal"></a>Azure Portal

toouse hello Azure portal toomigrate Azure Relay naamruimten uit in één abonnement tooanother abonnement, Zie [verplaatsen van resources tooa nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toouse PowerShell toomove een naamruimte uit één Azure-abonnement tooanother abonnement, gebruik Hallo reeks opdrachten te volgen. tooexecute deze bewerking Hallo naamruimte al moet actief zijn en Hallo-gebruiker die het Hallo PowerShell-opdrachten moet een beheerder op beide Hallo bron en doel-abonnementen.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>Welke Hallo uitzonderingen zijn gegenereerd door Azure Relay-API's en voorgestelde acties die u kunt nemen?
Zie voor een beschrijving van de algemene uitzonderingen en voorgestelde acties die u kunt uitvoeren, [Relay-uitzonderingen][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>Wat is er een shared access signature en welke talen kan ik gebruiken toogenerate een handtekening?
Shared Access Signatures (SAS) zijn een verificatiemethode op basis van beveiligde SHA-256-hashes of URI's. Voor informatie over hoe toogenerate uw eigen handtekeningen in het knooppunt, PHP, Java, C en C#, Zie [Service Bus-verificatie met handtekeningen voor gedeelde toegang][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>Is het mogelijk toowhitelist relay eindpunten?
Ja. Hallo relay client maakt verbindingen toohello Azure Relay-service met behulp van de volledig gekwalificeerde domeinnamen. Klanten kunnen Voeg een vermelding voor `*.servicebus.windows.net` op firewalls die ondersteuning bieden voor DNS-whitelisting.

## <a name="next-steps"></a>Volgende stappen
* [Een naamruimte maken](relay-create-namespace-portal.md)
* [Aan de slag met .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Aan de slag met knooppunten](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md