---
title: 'Azure App Service: Schalen App Service-toepassingen'
description: Meer informatie over Hallo alles over toepassing schalen in App Service.
keywords: App Service, Azure App Service, schaal, schaalbaar, App Service-abonnement, kosten App Service
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure App Service: Schalen App Service-toepassingen
Toepassingen die worden gehost in Azure App Service kunnen [bereiken grootschalige](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Een toepassing schalen is echter een complex probleem dat u beschikt niet over een oplossing 'één maat alle'. toocorrectly uw toepassing schalen er zijn 3 sleutelgebieden waarmee tooyour toepassingen geslaagd:

1. Informatie over de toepassingsarchitectuur van uw en de zwakke punten.
   * Is de Stateful van uw toepassing? Staatloze?
   * Wat zijn alle Hallo onderdelen van uw toepassing?
     * Waar zijn Hallo knelpunten in de toepassing hello?
   * Wanneer de belasting wordt toegepaste tooyour app, wat verbreekt de eerste?
2. Understanding Hallo verwacht laden en prestaties.
   * Hoeft de toepassing hello tooserve 1000 gebruikers? of een miljoen?
   * Wordt met verkeer afkomstig zijn uit één geografische locatie of globaal?
   * Zijn er seizoensgebonden variaties? verkeer pieken?
   * Hoe snel moet Hallo app reageren 1 seconde? 1 milliseconde?
3. Meer informatie over en correct hefboomwerking Hallo-platform die als host fungeert voor uw app.
   * Wat functies moeten ik mijn doelstellingen scale tooachieve gebruiken?

Deze sectie wordt informatie over alle Hallo factoren en ontwerpen van een strategie wordt gebruikgemaakt van Hallo nodig App Service functies tooachieve uw schaalbaarheidsdoelstellingen help.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

