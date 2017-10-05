---
title: Implementatie van toepassingen in Azure App Service
description: Meer informatie over het implementeren van toepassingen met App Service-werk
keywords: App service, azure app service implementeren, implementatie
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: 
ms.assetid: de12cd6e-e124-4e48-90bc-c3a3801305da
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 347e8b5177eac8e08ab0dea701b736b86d23904a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-deployment-overview"></a>Overzicht van de Azure App Service-implementatie
Azure App Service biedt een uitgebreide en geïntegreerde functie ingesteld voor het maken van werkstromen voor de implementatie van krachtige en flexibele. Opties, zoals continue integratie of lokale broncodebeheer publiceert, WebDeploy en FTP kan gebruikmaken van App-implementatie. De aanbevolen methode voor productie-app-implementatie is implementatiesleuf wisselen. Implementatiesites vertegenwoordigen faserings- en integratie omgevingen die zijn gekoppeld aan apps die productie. Implementatiesites kunnen worden geconfigureerd en toegepast op webverkeer voor validatie en verkeer worden ingewisseld op aanvraag voor implementatie naar de productieomgeving geen uitvaltijd en geautomatiseerde opgewarmd. De stappen van een werkstroom voor de implementatie kunnen eenvoudig via release management producten zoals Visual Studio Release Management worden geautomatiseerd. Dit is handig voor coördinatie met een andere oplossing resources (bijvoorbeeld gegevens opslaan), terugkeerpatroon en replicatie over meerdere van de implementatie. 

[!INCLUDE [app-service-blueprint-deployment](../../includes/app-service-blueprint-deployment.md)]

