---
title: aaaAzure gebeurtenis raster concepten
description: Beschrijving van Azure Event raster en de concepten. Hiermee definieert u enkele belangrijke onderdelen van gebeurtenis raster.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Concepten in Azure Event raster

belangrijkste concepten in Azure gebeurtenis raster Hallo zijn:

## <a name="events"></a>Gebeurtenissen

Een gebeurtenis is Hallo kleinste hoeveelheid informatie die iets volledig beschrijft die hebben plaatsgevonden in Hallo-systeem.  Elke gebeurtenis heeft een algemene informatie, zoals: bron van gebeurtenis hello, tijd Hallo gebeurtenis heeft plaatsgevonden en de unieke id.  Elke gebeurtenis heeft ook specifieke informatie die is alleen relevant toohello specifieke gebeurtenis. Bijvoorbeeld, bevat een gebeurtenis over een nieuw bestand wordt gemaakt in Azure Storage meer informatie over het Hallo-bestand, zoals Hallo lastTimeModified waarde. Of een gebeurtenis over een virtuele machine opnieuw opstarten Hallo naam bevat van Hallo virtuele machine en Hallo reden voor het opnieuw opstarten.

## <a name="event-sourcespublishers"></a>Gebeurtenisuitgevers bronnen

Een gebeurtenisbron is waarbij Hallo gebeurtenis gebeurt. Azure Storage is bijvoorbeeld de gebeurtenisbron Hallo voor blob gemaakt van gebeurtenissen. Azure VM-infrastructuur is Hallo gebeurtenisbron voor gebeurtenissen van de virtuele machine. Bronnen van gebeurtenissen zijn verantwoordelijk voor het publiceren van gebeurtenissen tooEvent raster.

## <a name="topics"></a>Onderwerpen

Uitgevers categoriseren gebeurtenissen in onderwerpen. Hallo onderwerp bevat een eindpunt waar Hallo publisher gebeurtenissen verzendt. toorespond toocertain typen gebeurtenissen, abonnees bepalen welke toosubscribe onderwerpen aan. Onderwerpen bevatten ook een gebeurtenis schema zodat abonnees hoe Hallo tooconsume gebeurtenissen op de juiste wijze kunnen detecteren.

Systeemonderwerpen zijn ingebouwde onderwerpen die worden geleverd door de Azure-services. Aangepaste onderwerpen zijn toepassing en onderwerpen van derden.

## <a name="event-subscriptions"></a>Gebeurtenisabonnementen

Een abonnement geïnstrueerd gebeurtenis raster op welke gebeurtenissen op een onderwerp een abonnee geïnteresseerd in ontvangst is.  Een abonnement bevat ook informatie over hoe gebeurtenissen moeten worden geleverd toohello abonnee.

## <a name="event-handlers"></a>Gebeurtenis-handlers

Een gebeurtenis-handler is vanuit het perspectief van een gebeurtenis raster wordt Hallo plaats waar het Hallo-gebeurtenis wordt verzonden. Hallo-handler duurt enkele verdere actie tooprocess Hallo-gebeurtenis.  Raster gebeurtenis biedt ondersteuning voor meerdere Abonneetypen. Afhankelijk van het type Hallo van abonnee volgt gebeurtenis raster verschillende mechanismen tooguarantee Hallo levering van Hallo-gebeurtenis.  Voor HTTP-webhook gebeurtenis-handlers Hallo gebeurtenis is vaak herhaald totdat Hallo handler statuscode retourneert `200 – OK`. Voor Azure-Opslagwachtrij worden Hallo gebeurtenissen opnieuw geprobeerd totdat Hallo Queue-service kunnen toosuccessfully proces Hallo-bericht push in Hallo wachtrij.

## <a name="filters"></a>Filters

Als u zich abonneert tooa onderwerp, kunt u filteren op Hallo-gebeurtenissen die worden verzonden toohello eindpunt. U kunt filteren op gebeurtenistype of onderwerp patroon. Zie voor meer informatie [gebeurtenis raster abonnement schema](subscription-creation-schema.md).

## <a name="security"></a>Beveiliging

Gebeurtenis biedt beveiliging voor tootopics abonneren en publiceren van onderwerpen. Als u zich abonneert, moet u voldoende machtigingen op Hallo bron of onderwerp hebben. Wanneer u publiceert, moet u een SAS-token of sleutelverificatie voor Hallo onderwerp hebben. Zie voor meer informatie [gebeurtenis raster beveiligings- en verificatie](security-authentication.md).

## <a name="failed-delivery"></a>Mislukte bezorging

Wanneer gebeurtenis raster kan niet bevestigen dat een gebeurtenis is ontvangen door Hallo-abonnee eindpunt, redelivers het Hallo-gebeurtenis. Zie voor meer informatie [gebeurtenis raster berichtbezorging en probeer het opnieuw](delivery-and-retry.md).

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding-tooEvent raster [over gebeurtenis raster](overview.md).
* tooquickly aan de slag met Event raster, Zie [maken en route aangepaste gebeurtenissen met Azure Event raster](custom-event-quickstart.md).
