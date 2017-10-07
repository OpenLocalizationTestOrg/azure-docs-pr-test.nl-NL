---
title: aaaAzure functies gebruiks- en App Service-plannen | Microsoft Docs
description: Begrijpen hoe Azure Functions toomeet Hallo behoeften van uw werkbelastingen gebeurtenisafhankelijke schaalt.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: 5b63649c-ec7f-4564-b168-e0a74cb7e0f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/12/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3826915b93328635d9295efe90ecc421e6c56af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure Functions gebruiks- en App Service-plannen 

## <a name="introduction"></a>Inleiding

U kunt Azure Functions uitvoeren in twee verschillende modi: verbruik plannings- en Azure App Service-abonnement. rekencapaciteit Hallo verbruik plan automatisch toegewezen wanneer uw code wordt uitgevoerd, als de belasting van de benodigde toohandle uitgeschaald en vervolgens omlaag geschaald wanneer de code wordt niet uitgevoerd. Ja, u hoeft toopay voor niet-actieve virtuele machines en tooreserve capaciteit vooraf niet hebt. Dit artikel is gericht op Hallo verbruik plan. Zie voor meer informatie over de werking van App Service-abonnement Hallo Hallo [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Als u niet bekend bent met Azure Functions, raadpleegt u Hallo [overzicht van Azure Functions](functions-overview.md).

Wanneer u een functie-app maakt, moet u een hosting-plan configureren voor functies die Hallo-app bevat. In beide modi, een exemplaar van Hallo *Azure Functions host* Hallo functies worden uitgevoerd. Hallo type plan besturingselementen:

* Hoe host exemplaren worden uitgebreid.
* Hallo-resources die beschikbaar tooeach host.

Op dit moment moet u Hallo plantype kiezen tijdens het maken van Hallo van Hallo functie-app. U kunt deze later wijzigen. 

U kunt schalen tussen lagen op Hallo App Service-abonnement. Op Hallo verbruik plan verwerkt de Azure Functions automatisch alle brontoewijzing.

## <a name="consumption-plan"></a>Verbruiksabonnement

Wanneer u een plan verbruik gebruikt, worden instanties van hello Azure Functions host dynamisch toegevoegd en verwijderd op basis van het aantal inkomende gebeurtenissen Hallo. Dit abonnement automatisch wordt geschaald en u in rekening worden gebracht rekenresources alleen wanneer uw functies worden uitgevoerd. Op een plan verbruik kan een functie voor een maximum van tien minuten uitgevoerd. 

> [!NOTE]
> Hallo standaardtime-out voor de functies worden uitgevoerd op een plan verbruik is 5 minuten. Hallo-waarden zijn toegenomen too10 minuten Hallo functie-App door het wijzigen van de eigenschap Hallo `functionTimeout` in [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Facturering is gebaseerd op uitvoeringstijd en geheugen dat wordt gebruikt en het wordt getotaliseerd over alle functies binnen een functie-app. Zie voor meer informatie, Hallo [Azure Functions pagina met prijzen].

Hallo verbruik plan is standaard Hallo en Hallo volgende voordelen biedt:
- U betaalt alleen wanneer uw functies worden uitgevoerd.
- Automatisch geschaald uitbreiden, zelfs tijdens perioden van hoge laadt.

## <a name="app-service-plan"></a>App Service-plan

In het Hallo-App Service plan, uw functie-apps worden uitgevoerd via exclusieve virtuele machines op Basic, Standard en Premium-SKU's vergelijkbaar tooWeb Apps. Toegewezen virtuele machines zijn toegewezen tooyour App Service-apps, wat betekent dat Hallo functies host altijd wordt uitgevoerd.

Houd rekening met een App Service-plan in de volgende gevallen Hallo:
- U hebt bestaande, onderbenutte virtuele machines waarop andere App Service-exemplaren.
- Verwacht u dat uw apps functie toorun continu, of bijna continu.
- U moet meer opties voor de CPU of geheugen dan wat op Hallo verbruik plan is opgegeven.
- U moet langer zijn dan Hallo maximale uitvoeringstijd toegestaan op Hallo verbruik plan toorun.

Een virtuele machine worden losgekoppeld-kosten van de grootte van zowel runtime en geheugen. Als gevolg hiervan Betaal je geen meer dan Hallo kosten van Hallo VM-instantie die u toewijst. Zie voor meer informatie over de werking van App Service-abonnement Hallo Hallo [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Met App Service-abonnement kunt u handmatig uitschalen door meer VM-exemplaren toe te voegen of u automatisch schalen kunt inschakelen. Zie voor meer informatie [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). U kunt ook opschalen door een ander App Service-abonnement te kiezen. Zie voor meer informatie [een app in Azure opschalen](../app-service-web/web-sites-scale.md). Als u van plan bent toorun JavaScript-functies op een App Service-abonnement, kiest u een plan dat minder kernen heeft. Zie voor meer informatie, Hallo [verwijzing in JavaScript voor functies](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: hello portal links toothis section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###AlwaysOn

Als u op een App Service-plan uitvoert, moet u Hallo inschakelen **altijd op** instellen zodat uw app in de functie correct wordt uitgevoerd. Op een App Service-abonnement gaat runtime van functions Hallo inactief na een paar minuten van inactiviteit, zodat alleen HTTP-triggers '' uw functies ontwaken wordt. Dit is vergelijkbaar toohow die webjobs moet Always On ingesteld hebben. 

AlwaysOn is alleen beschikbaar op een App Service-abonnement. Een plan verbruik activeert Hallo platform functie apps automatisch.

## <a name="storage-account-requirements"></a>Opslagvereisten voor account

Een functie-app vereist op een plan verbruik of een App Service-abonnement en een Azure Storage-account die ondersteuning biedt voor opslag in Azure Blob, wachtrijen en tabellen. Azure Functions gebruikt intern, Azure Storage voor bewerkingen zoals het beheren van triggers en functies die logboekregistratie. Sommige opslagaccounts bieden geen ondersteuning voor wachtrijen en tabellen, zoals alleen-blob storage-accounts (met inbegrip van premium-opslag) en opslagaccounts met replicatie van de zone-redundante opslag. Deze accounts zijn gefilterd uit Hallo **Opslagaccount** blade als u een functie-app.

toolearn meer informatie over opslagaccounttypen, Zie [Inleiding tot Azure Storage-services Hallo](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-hello-consumption-plan-works"></a>Hoe werkt dit plan van Hallo verbruik

Hallo verbruik plan schaalt automatisch CPU en geheugenbronnen door extra exemplaren van Hallo functies host, op basis van het aantal gebeurtenissen die de functies worden geactiveerd op Hallo toe te voegen. Elk exemplaar van Hallo functies host is beperkt too1.5 GB aan geheugen.

Wanneer u Hallo verbruik die als host fungeert voor plan, functie codebestanden worden opgeslagen op Azure-bestandsshares op Hallo belangrijkste storage-account. Wanneer u de belangrijkste opslagaccount Hallo verwijdert, wordt deze inhoud is verwijderd en kan niet worden hersteld.

> [!NOTE]
> Wanneer u een blob-trigger op een plan verbruik, kunnen er up tooa 10 minuten vertraging bij de verwerking van nieuwe blobs als een functie-app niet actief is geworden. Nadat het Hallo-functie-app wordt uitgevoerd, worden onmiddellijk blobs verwerkt. Dit eerste tooavoid uitstellen, kunt u een Hallo volgende opties:
> - Gebruik een App Service-abonnement met altijd op ingeschakeld.
> - Gebruik een ander mechanisme tootrigger Hallo blob verwerken, zoals een wachtrijbericht die Hallo blob-naam bevat. Zie voor een voorbeeld [wachtrij trigger met blob invoer binding](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Runtime-schaling

Azure Functions maakt gebruik van een onderdeel genaamd Hallo *scale controller* toomonitor Hallo snelheid van gebeurtenissen en bepalen of tooscale out- of omlaag schalen. Hallo scale controller gebruikt methodiek voor elk triggertype. Bijvoorbeeld, wanneer u een Azure Queue storage-trigger, schalen het op basis van Hallo wachtrijlengte en Hallo leeftijd van Hallo-bericht van oudste wachtrij.

Hallo-eenheid van de schaal is Hallo functie-app. Wanneer de functie-app Hallo is uitgebreid, meer resources zijn toegewezen toorun meerdere exemplaren van hello Azure Functions-host. Als u daarentegen zoals Reken-aanvraag wordt verlaagd, Hallo scale controller functie host worden exemplaren verwijderd. het aantal exemplaren Hallo uiteindelijk verkleind toozero wanneer er geen functies worden uitgevoerd binnen een functie-app.

![Schaal controller controle van gebeurtenissen en het maken van exemplaren](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Factureringsmodel

Financieel voor Hallo verbruik plan in detail op Hallo beschreven wordt [Azure Functions pagina met prijzen]. Gebruik op het niveau Hallo functie-app wordt geaggregeerd en telt alleen Hallo keer dat de functiecode wordt uitgevoerd. Hallo volgen eenheden voor facturering: 
* **Brongebruik in gigabyte (GB-s) seconden**. Berekend als een combinatie van de grootte van het systeemgeheugen en de uitvoeringstijd voor alle functies binnen een functie-app. 
* **Uitvoeringen**. Geteld telkens wanneer een functie wordt uitgevoerd in reactie tooan gebeurtenis geactiveerd door een binding.

[Azure Functions pagina met prijzen]: https://azure.microsoft.com/pricing/details/functions
