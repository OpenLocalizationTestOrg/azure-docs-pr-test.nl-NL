---
title: Azure Functions gebruiks- en App Service-plannen | Microsoft Docs
description: Begrijpen hoe Azure Functions schalen om te voldoen aan de behoeften van uw werkbelastingen gebeurtenisafhankelijke.
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
ms.openlocfilehash: 70e77e09b2e2116153159167af61776398904a3c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-consumption-and-app-service-plans"></a>Azure Functions gebruiks- en App Service-plannen 

## <a name="introduction"></a>Inleiding

U kunt Azure Functions uitvoeren in twee verschillende modi: verbruik plannings- en Azure App Service-abonnement. Het plan verbruik wijst automatisch rekencapaciteit wanneer uw code wordt uitgevoerd, indien nodig om belasting te verwerken uitgeschaald en vervolgens omlaag geschaald wanneer de code wordt niet uitgevoerd. Dus u hoeft niet te betalen voor niet-actieve virtuele machines en hoeft niet te worden van tevoren capaciteit reserveren. Dit artikel is gericht op het plan verbruik. Zie voor meer informatie over de werking van de App Service-abonnement de [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Als u niet bekend bent met Azure Functions, raadpleegt u de [overzicht van Azure Functions](functions-overview.md).

Wanneer u een functie-app maakt, moet u een hosting plan voor de functies die de app bevat. In beide modi, een exemplaar van de *Azure Functions host* de functies worden uitgevoerd. Het type van besturingselementen voor plannen:

* Hoe host exemplaren worden uitgebreid.
* De bronnen die beschikbaar voor elke host zijn.

Op dit moment moet u het type kiezen tijdens het maken van de functie-app. U kunt deze later wijzigen. 

U kunt schalen tussen lagen van de App Service-plan. Op het plan verbruik verwerkt Azure Functions automatisch alle brontoewijzing.

## <a name="consumption-plan"></a>Verbruiksabonnement

Wanneer u een plan verbruik gebruikt, worden instanties van de Azure Functions-host dynamisch toegevoegd en verwijderd op basis van het aantal binnenkomende gebeurtenissen. Dit abonnement automatisch wordt geschaald en u in rekening worden gebracht rekenresources alleen wanneer uw functies worden uitgevoerd. Op een plan verbruik kan een functie voor een maximum van tien minuten uitgevoerd. 

> [!NOTE]
> De standaardtime-out voor de functies worden uitgevoerd op een plan verbruik is 5 minuten. De waarde kan worden verhoogd tot 10 minuten voor de functie-App met het wijzigen van de eigenschap `functionTimeout` in [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

Facturering is gebaseerd op uitvoeringstijd en geheugen dat wordt gebruikt en het wordt getotaliseerd over alle functies binnen een functie-app. Zie voor meer informatie de [Azure Functions pagina met prijzen].

Het plan verbruik is de standaardinstelling en biedt de volgende voordelen:
- U betaalt alleen wanneer uw functies worden uitgevoerd.
- Automatisch geschaald uitbreiden, zelfs tijdens perioden van hoge laadt.

## <a name="app-service-plan"></a>App Service-plan

In het App Service-plan uw functie-apps worden uitgevoerd via exclusieve virtuele machines op Basic, Standard en Premium-SKU's, vergelijkbaar met Web-Apps. Toegewezen virtuele machines worden toegewezen aan uw App Service-apps, wat betekent dat de host functies altijd wordt uitgevoerd.

Houd rekening met een App Service-plan in de volgende gevallen:
- U hebt bestaande, onderbenutte virtuele machines waarop andere App Service-exemplaren.
- Verwacht u dat uw apps functie continu of bijna continu uit te voeren.
- U moet meer opties voor de CPU of geheugen dan is opgegeven op het plan verbruik.
- U moet langer zijn dan de maximale uitvoeringstijd toegestaan op het plan verbruik uitvoeren.

Een virtuele machine worden losgekoppeld-kosten van de grootte van zowel runtime en geheugen. Als gevolg hiervan Betaal je geen meer dan de kosten van de VM-instantie die u toewijst. Zie voor meer informatie over de werking van de App Service-abonnement de [gedetailleerd overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Met App Service-abonnement kunt u handmatig uitschalen door meer VM-exemplaren toe te voegen of u automatisch schalen kunt inschakelen. Zie voor meer informatie [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json). U kunt ook opschalen door een ander App Service-abonnement te kiezen. Zie voor meer informatie [een app in Azure opschalen](../app-service-web/web-sites-scale.md). Als u van plan bent voor het uitvoeren van JavaScript-functies op een App Service-abonnement, moet u een plan dat minder kernen heeft. Zie voor meer informatie de [verwijzing in JavaScript voor functies](functions-reference-node.md#choose-single-core-app-service-plans).  

<!-- Note: the portal links to this section via fwlink https://go.microsoft.com/fwlink/?linkid=830855 --> 
<a name="always-on"></a>
###AlwaysOn

Als u op een App Service-plan uitvoert, moet u inschakelen de **altijd op** instellen zodat uw app in de functie correct wordt uitgevoerd. Op een App Service-abonnement gaat de runtime van functions inactief na een paar minuten van inactiviteit, zodat alleen HTTP-triggers '' uw functies ontwaken wordt. Dit is vergelijkbaar met hoe WebJobs moet Always On ingesteld hebben. 

AlwaysOn is alleen beschikbaar op een App Service-abonnement. Functie apps die het automatisch door het platform wordt geactiveerd op een plan verbruik.

## <a name="storage-account-requirements"></a>Opslagvereisten voor account

Een functie-app vereist op een plan verbruik of een App Service-abonnement en een Azure Storage-account die ondersteuning biedt voor opslag in Azure Blob, wachtrijen en tabellen. Azure Functions gebruikt intern, Azure Storage voor bewerkingen zoals het beheren van triggers en functies die logboekregistratie. Sommige opslagaccounts bieden geen ondersteuning voor wachtrijen en tabellen, zoals alleen-blob storage-accounts (met inbegrip van premium-opslag) en opslagaccounts met replicatie van de zone-redundante opslag. Deze accounts zijn gefilterd uit de **Opslagaccount** blade als u een functie-app.

Zie voor meer informatie over opslagaccounttypen, [introductie van de Azure Storage-services](../storage/common/storage-introduction.md#introducing-the-azure-storage-services).

## <a name="how-the-consumption-plan-works"></a>Hoe werkt dit plan verbruik

Het plan verbruik schaalt automatisch CPU en geheugenbronnen door toe te voegen extra exemplaren van de host van functies, op basis van het aantal gebeurtenissen die de functies worden geactiveerd op. Elk exemplaar van de host van functies is beperkt tot 1,5 GB aan geheugen.

Wanneer u het verbruik die als host fungeert voor plan gebruikt, wordt de functie codebestanden worden opgeslagen op Azure-bestandsshares op de belangrijkste storage-account. Wanneer u de belangrijkste storage-account verwijdert, wordt deze inhoud is verwijderd en kan niet worden hersteld.

> [!NOTE]
> Wanneer u een blob-trigger op een plan verbruik, kunnen er maximaal 10 minuten vertraging bij de verwerking van nieuwe blobs als een functie-app niet actief is geworden. Nadat de functie-app wordt uitgevoerd, worden onmiddellijk blobs verwerkt. Overweeg om te voorkomen dat deze initiële vertraging, een van de volgende opties:
> - Gebruik een App Service-abonnement met altijd op ingeschakeld.
> - Gebruik een ander mechanisme voor het activeren van de blob verwerken, zoals een wachtrijbericht met de blob-naam. Zie voor een voorbeeld [wachtrij trigger met blob invoer binding](functions-bindings-storage-blob.md#input-sample).

### <a name="runtime-scaling"></a>Runtime-schaling

Azure Functions maakt gebruik van een onderdeel genaamd de *scale controller* om te controleren van de snelheid van gebeurtenissen en bepalen of u wilt uitbreiden of omlaag schalen. De scale-controller gebruikt methodiek voor elk triggertype. Bijvoorbeeld, wanneer u een Azure Queue storage-trigger, schalen het op basis van de lengte van de wachtrij en de leeftijd van oudste bericht uit de wachtrij.

De eenheid van de schaal is de functie-app. Wanneer de functie-app is uitgebreid, worden meer bronnen toegewezen aan meerdere exemplaren van de Azure Functions-host uitvoeren. Als u daarentegen, zoals Reken-aanvraag wordt verlaagd, de controller scale functie host worden exemplaren verwijderd. Het aantal exemplaren wordt uiteindelijk geschaald naar beneden op nul wanneer er geen functies worden uitgevoerd binnen een functie-app.

![Schaal controller controle van gebeurtenissen en het maken van exemplaren](./media/functions-scale/central-listener.png)

### <a name="billing-model"></a>Factureringsmodel

Financieel voor het verbruik plan wordt in detail beschreven op de [Azure Functions pagina met prijzen]. Gebruik op het niveau van de functie-app wordt geaggregeerd en alleen de tijd waarop de functiecode wordt geteld. Hier volgen de eenheden voor facturering: 
* **Brongebruik in gigabyte (GB-s) seconden**. Berekend als een combinatie van de grootte van het systeemgeheugen en de uitvoeringstijd voor alle functies binnen een functie-app. 
* **Uitvoeringen**. Geteld telkens wanneer een functie wordt uitgevoerd in reactie op een gebeurtenis geactiveerd door een binding.

[Azure Functions pagina met prijzen]: https://azure.microsoft.com/pricing/details/functions
