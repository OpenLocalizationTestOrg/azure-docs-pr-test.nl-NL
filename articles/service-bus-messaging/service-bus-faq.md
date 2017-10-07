---
title: aaaAzure Service Bus Veelgestelde vragen (FAQ) | Microsoft Docs
description: Antwoorden op enkele veelgestelde vragen over Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>Veelgestelde vragen over Service Bus
Dit artikel worden enkele veelgestelde vragen over Microsoft Azure Service Bus. U kunt ook Hallo bezoeken [Azure ondersteunen Veelgestelde vragen over](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure-prijzen en -ondersteuning voor informatie.

## <a name="general-questions-about-azure-service-bus"></a>Algemene vragen over Azure Service Bus
### <a name="what-is-azure-service-bus"></a>Wat is Azure Service Bus?
[Azure Service Bus](service-bus-messaging-overview.md) is een asynchrone messaging cloudplatform waarmee u gegevens toosend tussen ontkoppelde systemen. Microsoft biedt deze functie als een service, wat betekent dat u niet toohost uw eigen hardware in volgorde toouse hoeft deze.

### <a name="what-is-a-service-bus-namespace"></a>Wat is een Service Bus-naamruimte?
Een [naamruimte](service-bus-create-namespace-portal.md) biedt een scoping container voor het adresseren van Service Bus-resources in uw toepassing. Maken van een wordt benodigde toouse Service Bus is en een Hallo eerste stappen aan de slag.

### <a name="what-is-an-azure-service-bus-queue"></a>Wat is een Azure Service Bus-wachtrij?
Een [Service Bus-wachtrij](service-bus-queues-topics-subscriptions.md) is een entiteit waarin berichten worden opgeslagen. Wachtrijen zijn bijzonder nuttig wanneer u meerdere toepassingen of meerdere onderdelen van een gedistribueerde toepassing die toocommunicate met elkaar nodig hebt. Hallo-wachtrij is vergelijkbaar tooa distribution center in dat meerdere producten (berichten) worden ontvangen en vervolgens vanuit die locatie worden verzonden.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Wat zijn Azure Service Bus-onderwerpen en abonnementen?
Een onderwerp kan worden weergegeven als een wachtrij en wanneer u meerdere abonnementen, wordt een uitgebreidere messaging model; in wezen een een-op-veel-communicatie-hulpprogramma. Dit model publiceren/abonneren (of *pub subitems*) Hiermee wordt een toepassing die u een bericht tooa onderwerp met meerdere abonnementen toohave bericht ontvangen door meerdere toepassingen verzendt.

### <a name="what-is-a-partitioned-entity"></a>Wat is een gepartitioneerde entiteit?
Een conventionele wachtrij of onderwerp is verwerkt door een enkel bericht broker en opgeslagen in één berichten-store. Een [gepartitioneerde wachtrij of onderwerp](service-bus-partitioning.md) wordt verwerkt door meerdere bericht beleggingsmakelaars en opgeslagen in meerdere berichten-stores. Dit betekent dat de totale doorvoer van een gepartitioneerde wachtrij of onderwerp Hallo wordt niet langer beperkt door het Hallo-prestaties van een enkel bericht broker of berichten-store. Bovendien weer een tijdelijke onderbreking van berichten-store niet een gepartitioneerde wachtrij of onderwerp niet beschikbaar.

Houd er rekening mee dat ordening wordt niet gegarandeerd bij gebruik van partitionering entiteiten. U kunt nog steeds verzenden en ontvangen van berichten van Hallo andere partities in Hallo-gebeurtenis met een partitie is niet beschikbaar.

## <a name="best-practices"></a>Aanbevolen procedures
### <a name="what-are-some-azure-service-bus-best-practices"></a>Wat zijn enkele aanbevolen procedures van Azure Service Bus?
* [Aanbevolen procedures voor verbeterde prestaties met Service Bus] [ Best practices for performance improvements using Service Bus] – dit artikel wordt beschreven hoe toooptimize prestaties bij het uitwisselen van berichten.

### <a name="what-should-i-know-before-creating-entities"></a>Wat moet ik weten voordat u entiteiten
Hallo volgende eigenschappen van een wachtrij en onderwerp zijn niet-wijzigbaar. Neem dit rekening houden wanneer u uw entiteiten inrichten als dit niet worden gewijzigd zonder dat er een nieuwe entiteit in de vervanging.

* Grootte
* Partitionering
* Sessies
* Detectie van duplicaten
* Snelle entiteit

## <a name="pricing"></a>Prijzen
Deze sectie worden enkele veelgestelde vragen over prijzen Hallo Service Bus-structuur.

Hallo [Service Bus-prijzen en facturering](service-bus-pricing-billing.md) artikel wordt uitgelegd Hallo facturering meters in Service Bus en voor informatie over Service Bus prijzen opties, Zie [Service Bus prijsinformatie](https://azure.microsoft.com/pricing/details/service-bus/).

U kunt ook Hallo bezoeken [Veelgestelde vragen over Azure-ondersteuning](http://go.microsoft.com/fwlink/?LinkID=185083) voor algemene Azure prijsinformatie. 

### <a name="how-do-you-charge-for-service-bus"></a>Hoe u kosten in rekening gebracht voor Service Bus?
Zie voor volledige informatie over prijzen voor Service Bus [Service Bus prijsinformatie][Pricing overview]. Bovendien toohello prijzen genoteerd, worden in rekening gebracht voor de bijbehorende gegevensoverdracht voor uitgaande buiten Hallo Datacenter waarin de toepassing is ingericht.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>Welke informatie over het gebruik van Service Bus is onderwerp toodata overdracht? Wat is er geen?
Een overdracht van gegevens binnen een bepaald Azure-regio is opgegeven zonder kosten, evenals binnenkomende gegevensoverdracht. Gegevensoverdracht buiten een regio is onderwerp tooegress kosten die u kunnen vinden [hier](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Service Bus kosten in rekening gebracht voor de opslag?
Nee, Service Bus biedt geen kosten in rekening gebracht voor opslag. Er is echter een quotum beperkende Hallo maximum hoeveelheid gegevens die kan worden gehandhaafd per wachtrij/onderwerp. Zie de volgende veelgestelde vragen over Hallo.

## <a name="quotas"></a>Quota

Zie voor een lijst met Service Bus-limieten en quota's, Hallo [overzicht van Service Bus-quota][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Beschikt over Service Bus quota voor gebruik?
Standaard voor een cloud service Microsoft Hiermee stelt u een cumulatieve maandelijkse gebruiksgegevens van die is berekend voor alle abonnementen van de klant. Omdat we begrijpen dat u deze limieten moet mogelijk, neem contact op met klantenservice op elk gewenst moment zodat we kunnen uw behoeften te begrijpen en pas deze limieten op de juiste wijze. Voor Service Bus is Hallo cumulatieve gebruiksquotum 5 miljard berichten per maand.

Terwijl we Hallo rechts toodisable een klantaccount die de quota voor gebruik in een bepaalde maand heeft overschreden reserveren, wordt e-mailmelding bieden en meerdere pogingen toocontact een klant maken voordat u geen actie. Klanten die deze quota overschrijdt nog steeds die verantwoordelijk is voor de kosten die groter is dan Hallo quota's.

Net als bij andere services op Azure Service Bus zorgt ervoor dat een set specifieke quota tooensure dat er evenredige gebruik van resources is. U vindt meer informatie over deze quota in Hallo [overzicht van Service Bus-quota][Quotas overview].

## <a name="troubleshooting"></a>Problemen oplossen
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Wat zijn enkele Hallo uitzonderingen die worden gegenereerd door de Azure Service Bus-API's en hun voorgestelde acties?
Zie voor een lijst van mogelijke Service Bus-uitzonderingen [uitzonderingen overzicht][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Wat is er een Shared Access Signature en welke talen ondersteuning voor een handtekening te genereren?
Handtekeningen voor gedeelde toegang zijn een verificatiemethode op basis van SHA-256 beveiligde hashes of URI's. Voor informatie over het toogenerate uw eigen handtekeningen in het knooppunt, PHP, Java en C\#, Zie Hallo [Shared Access Signatures] [ Shared Access Signatures] artikel.

## <a name="subscription-and-namespace-management"></a>Abonnement en de naamruimte management
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Hoe Migreer ik een naamruimte tooanother Azure-abonnement?

U kunt een naamruimte verplaatsen van een Azure-abonnement tooanother, met behulp van beide Hallo [Azure-portal](https://portal.azure.com) of PowerShell-opdrachten. In bewerking in volgorde tooexecute hello, moet Hallo-naamruimte al actief zijn. Hallo-gebruiker Hallo opdrachten uitvoeren moet een beheerder zijn op beide Hallo-bron en doel abonnementen.

#### <a name="portal"></a>Portal

toouse hello Azure portal toomigrate Service Bus-naamruimten tooanother abonnement, volg Hallo aanwijzingen [hier](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Hallo verplaatst volgende reeks PowerShell-opdrachten een naamruimte van tooanother van een Azure-abonnement. tooexecute deze bewerking Hallo naamruimte al actief moet zijn, en Hallo-gebruiker die het Hallo PowerShell-opdrachten moet een beheerder zijn op beide Hallo bron en doel-abonnementen.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Service Bus Zie Hallo volgende onderwerpen.

* [Introducing Azure Service Bus Premium (blogbericht)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Introducing Azure Service Bus Premium (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Overzicht van Service Bus](service-bus-messaging-overview.md)
* [Overzicht van Azure Service Bus-architectuur](service-bus-fundamentals-hybrid-solutions.md)
* [Aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
