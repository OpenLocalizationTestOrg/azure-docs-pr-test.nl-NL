---
title: aaaOverview van meerdere tenants achtergrond eindigt op Azure Application Gateway | Microsoft Docs
description: Deze pagina bevat een overzicht van Hallo Application Gateway ondersteuning voor back-ends van meerdere tenants.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: 
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: b7da8c9c68e34bd83ad2b828fab62c00caea354a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-support-for-multi-tenant-back-ends"></a>Application Gateway-ondersteuning voor back-ends met meerdere tenants

Azure Application Gateway biedt ondersteuning voor virtuele-machineschaalsets, netwerkinterfaces, openbare en persoonlijke IP-adressen en volledig gekwalificeerde domeinnamen (FQDN) als onderdeel van de back-endpools. Standaard application gateway verandert niet Hallo binnenkomende HTTP host-header van de client Hallo en verzendt Hallo header ongewijzigde toohello back-end. Er zijn veel services zoals [Azure Web Apps](../app-service-web/app-service-web-overview.md) en [API Management](../api-management/api-management-key-concepts.md) multitenant structuur bent en die afhankelijk zijn van een specifieke host-header of de SNI-extensie tooresolve toohello juiste eindpunt. Application Gateway ondersteunt nu Hallo mogelijkheid voor gebruikers toooverwrite Hallo binnenkomende HTTP host-header op basis van Hallo back-end van HTTP-instellingen. Dankzij deze mogelijkheid is er ondersteuning voor Azure-web-apps en API-beheer met back-ends met meerdere tenants. Deze functie is beschikbaar voor zowel Hallo standaard en WAF SKU. Multitenant back-endnetwerk ondersteuning ook werkt met SSL-beëindiging en end tooend SSL scenario's.

![web-app-scenario](./media/application-gateway-web-app-overview/scenario.png)

Hallo mogelijkheid toospecify een host onderdrukking is gedefinieerd op Hallo HTTP-instellingen en kan worden toegepast tooany terug eindigen groep tijdens het maken van de regel. Multitenant terug eindigt ondersteuning Hallo volgende twee manieren van het host-header en SNI-extensie te overschrijven.

1. Hallo mogelijkheid tooset Hallo host naam tooa vaste waarde in Hallo HTTP-instellingen. Deze mogelijkheid zorgt ervoor dat Hallo host-header wordt overschreven toothis waarde voor alle verkeer toohello back-end-pool waarop Hallo HTTP-instellingen worden toegepast. Als u end tooend SSL gebruikt, wordt deze overschreven hostnaam in Hallo SNI-extensie gebruikt. Deze mogelijkheid kunt scenario's waarbij een farm van de groep back-end van een host-header die verschilt van binnenkomende klant host-header Hallo verwacht.

2. Hallo mogelijkheid tooderive Hallo hostnaam van Hallo IP of FQDN-naam van back-end-groepsleden Hallo. HTTP-instellingen bieden ook een optie toopick Hallo-hostnaam van een back-end-poollid FQDN als geconfigureerd met Hallo optie tooderive-hostnaam van een afzonderlijke back-end-pool-lid. Als u end tooend SSL gebruikt, wordt deze hostnaam is afgeleid van Hallo FQDN-naam en wordt gebruikt in Hallo SNI-extensie. Deze mogelijkheid kunt scenario's waarbij een back-end-pool kan twee of meer multitenant PaaS-services zoals Azure-web-apps hebben en lid zijn van Hallo aanvraag host-header tooeach bevat Hallo-hostnaam die is afgeleid van de FQDN.

> [!NOTE]
> In beide gevallen voorgaande Hallo Hallo instellingen alleen van invloed op Hallo live verkeer gedrag en niet Hallo health test gedrag. Custom probes al ondersteuning Hallo mogelijkheid toospecify een host-header in Hallo test configuratie. Aangepaste tests ondersteunen nu ook Hallo mogelijkheid tooderive Hallo host-header gedrag van Hallo momenteel zodanig geconfigureerd dat de HTTP-instellingen. Deze configuratie kan worden opgegeven met behulp van Hallo `PickHostNameFromback endAddress` parameter in configuratie van de test Hallo. Voor end tooend functionaliteit toowork moet zowel Hallo test en Hallo HTTP-instellingen gewijzigde tooreflect Hallo juiste configuratie.

Met deze mogelijkheid Geef klanten toohello juiste configuratie-opties Hallo Hallo HTTP-instellingen en aangepaste tests. Deze instelling is vervolgens gekoppeld tooa listener en een back-end van toepassingen met behulp van een regel.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooset van een toepassingsgateway met een web-app als een back-poollid beëindigen in via: [configureren App Service-web-apps met Application Gateway](application-gateway-web-app-powershell.md)
