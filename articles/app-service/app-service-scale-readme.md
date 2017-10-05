---
title: 'Azure App Service: Schalen App Service-toepassingen'
description: Lees alles van toepassing schalen in App Service.
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
ms.openlocfilehash: 4ebaafe69fc1f91c7890611b14e8600df5c40cde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Azure App Service: Schalen App Service-toepassingen
Toepassingen die worden gehost in Azure App Service kunnen [bereiken grootschalige](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Een toepassing schalen is echter een complex probleem dat u beschikt niet over een oplossing 'één maat alle'. Uw toepassing er zijn correct schaal 3 sleutelgebieden's dragen bij aan uw succes toepassingen:

1. Informatie over de toepassingsarchitectuur van uw en de zwakke punten.
   * Is de Stateful van uw toepassing? Staatloze?
   * Wat zijn de onderdelen van uw toepassing?
     * Waar worden de knelpunten in de toepassing?
   * Bij het laden naar uw app wordt toegepast, wat verbreekt de eerste?
2. Informatie over de verwachte vereisten van load en prestaties.
   * Moet de toepassing fungeren 1000 gebruikers? of een miljoen?
   * Wordt met verkeer afkomstig zijn uit één geografische locatie of globaal?
   * Zijn er seizoensgebonden variaties? verkeer pieken?
   * Hoe snel moet de app reageren 1 seconde? 1 milliseconde?
3. Meer informatie over en correct gebruikmaken van het platform voor het hosten van uw app.
   * Welke functies moet ik gebruiken voor het bereiken van Mijn doelen schaal

Deze sectie helpt u begrijpen van de factoren en hulp bij het opstellen van een strategie wordt gebruikgemaakt van de benodigde App Service-functies om uw schaalbaarheidsdoelstellingen te realiseren.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

