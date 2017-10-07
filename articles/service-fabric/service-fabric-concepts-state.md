---
title: aaaDefinine en beheren van de status in Azure microservices | Microsoft Docs
description: Hoe toodefine en beheren van de status in Service Fabric-service
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f5e618a5-3ea3-4404-94af-122278f91652
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 4a24696da71753d0f343a86df3556b5b7c964834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-state"></a>Servicestatus
**Status service** toohello in het geheugen of op dat een service toofunction vereist schijfgegevens verwijst. Deze omvatten, bijvoorbeeld Hallo gegevensstructuren en lidvariabelen die Hallo-service leest en schrijft toodo werk. Afhankelijk van hoe Hallo-service is ontworpen, kan deze ook bestanden of andere bronnen die zijn opgeslagen op schijf bevatten. Bijvoorbeeld Hallo bestanden voor een database toostore gegevens en transactie-logboeken zou gebruiken.

Als een service voorbeeld laten we eens een rekenmachine. Een service basisrekenmachine neemt twee getallen en retourneert de som. Uitvoeren van deze berekening omvat geen lidvariabelen of andere informatie.

Bekijk nu dezelfde Rekenmachine hello, maar met een aanvullende methode voor het opslaan en retourneren van de laatste som Hallo het berekend. Deze service is nu stateful. Stateful betekent dat deze bevat een aantal met toowhen deze wordt een nieuwe som berekend en leest uit wanneer u deze tooreturn Hallo laatste berekende som vraagt worden geschreven.

In de Azure Service Fabric Hallo eerste service een stateless service genoemd. Hallo tweede service wordt een stateful service genoemd.

## <a name="storing-service-state"></a>Opslaan van de status van service
Status worden ofwel externalized of CO-locaties met Hallo-code die is Hallo status bewerken. Externalization van staat gewoonlijk wordt uitgevoerd met behulp van een externe database of ander gegevensarchief dat wordt uitgevoerd op verschillende computers via Hallo netwerk of buiten het proces op dezelfde machine Hallo. In ons voorbeeld Rekenmachine Hallo gegevensarchief mogelijk een SQL-database of een exemplaar van Azure Table-Store. Elke aanvraag toocompute Hallo som voert een update op deze gegevens en toohello service tooreturn Hallo waarde resultaat in de huidige Hallo-waarde wordt opgehaald uit de store Hallo-aanvragen. 

Status kan ook worden geplaatst met Hallo-code die Hallo status bewerkt. Stateful services in Service Fabric zijn doorgaans gebouwd met behulp van dit model. Service Fabric bevat Hallo infrastructuur tooensure dat deze status maximaal beschikbaar, consistent en duurzame is en dat Hallo-services op deze manier opgebouwd eenvoudig kunt schalen.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Service Fabric-concepten Hallo artikelen te volgen:

* [Beschikbaarheid van Service Fabric-services](service-fabric-availability-services.md)
* [Schaalbaarheid van Service Fabric-services](service-fabric-concepts-scalability.md)
* [Partitionering Service Fabric-services](service-fabric-concepts-partitioning.md)
* [Service Fabric Reliable Services](service-fabric-reliable-services-introduction.md)
