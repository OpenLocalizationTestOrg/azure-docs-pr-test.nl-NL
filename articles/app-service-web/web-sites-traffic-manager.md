---
title: aaaControlling verkeer van Azure-web-app met Azure Traffic Manager
description: Dit artikel bevat samenvattingsinformatie voor Azure Traffic Manager, omdat deze zich tooAzure web-apps verhoudt.
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Verkeer van web-apps in Azure beheren met Traffic Manager
> [!NOTE]
> Dit artikel bevat samenvattingsinformatie voor Microsoft Azure Traffic Manager, omdat deze zich tooAzure App Service Web Apps verhoudt. Via koppelingen naar Hallo op Hallo einde van dit artikel vindt meer informatie over Azure Traffic Manager zelf.
> 
> 

## <a name="introduction"></a>Inleiding
U kunt Azure Traffic Manager toocontrol hoe aanvragen van de webserver en webclients gedistribueerde tooweb apps in Azure App Service zijn. Als eindpunten voor web-app worden toegevoegd tooa Azure Traffic Manager-profiel, Azure Traffic Manager houdt van Hallo status van uw web-apps (actief, gestopt of verwijderd) zodat u deze kunt bepalen welke van deze eindpunten verkeer ontvangt.

## <a name="load-balancing-methods"></a>Load Balancing methoden
Azure Traffic Manager maakt gebruik van drie verschillende load balancing methoden. Deze worden beschreven in Hallo lijst zoals ze betrekking tooAzure web-apps hebben te volgen.

* **Failover**: als u web-app klonen in verschillende regio's hebt, u kunt gebruiken deze methode tooconfigure één web app tooservice alle web-clientverkeer en configureert u een andere web-app in een andere regio tooservice die verkeer in case Hallo eerste web-app niet beschikbaar.
* **Round Robin**: als u web-app klonen in verschillende regio's hebt, kunt u deze methode toodistribute verkeer gelijkmatig over Hallo web-apps in verschillende regio's.
* **Prestaties**: Hallo prestaties methode verkeer op basis van Hallo kortste round trip time tooclients distribueert. Hallo prestaties methode kan worden gebruikt voor web-apps binnen Hallo dezelfde regio of in verschillende regio's.

## <a name="web-apps-and-traffic-manager-profiles"></a>Web-Apps en Traffic Manager-profielen
tooconfigure hello beheer van verkeer voor web-app, u een profiel maken in Azure Traffic Manager die gebruikmaakt van een van drie Hallo taakverdelingsmethoden hierboven en voeg vervolgens Hallo-eindpunten (in dit geval web-apps) waarvoor u toocontrol verkeer toohello wilt profiel. De status van uw web-app (actief, gestopt of verwijderd) wordt regelmatig wordt gecommuniceerd toohello profiel zodat Azure Traffic Manager kunt dienovereenkomstig verkeer omleiden.

Als u Azure Traffic Manager met Azure, houd er rekening mee Hallo volgende punten:

* Voor web-app alleen implementaties binnen Hallo biedt dezelfde regio, Web-Apps al failover- en round-robin functionaliteit zonder inachtneming tooweb app-modus.
* Voor implementaties in dezelfde regio die Web-Apps gebruiken in combinatie met een andere Azure-cloudservice Hallo, kunt u beide typen eindpunten tooenable hybride scenario's combineren.
* U kunt slechts één eindpunt van web-app per regio opgeven in een profiel. Wanneer u een web-app als een eindpunt voor één regio selecteert, Hallo resterende web-apps in deze regio niet beschikbaar voor selectie voor dit profiel.
* Hallo web-app-eindpunten die u in een Azure Traffic Manager-profiel opgeeft wordt weergegeven onder Hallo **domeinnamen** sectie op Hallo configureren pagina voor de web-app Hallo in Hallo-profiel, maar wordt er niet zijn geconfigureerd.
* Nadat u een profiel voor een web-app tooa toevoegt, Hallo **Site-URL** op Hallo Dashboard van Hallo web van app-portalpagina Hallo aangepast domein-URL van Hallo web-app wordt weergegeven als u een hebt ingesteld. Anders Hallo Traffic Manager-profiel-URL wordt weergegeven (bijvoorbeeld `contoso.trafficmgr.com`). Beide direct domeinnaam van de web-app Hallo Hallo en Hallo Traffic Manager-URL is zichtbaar op Hallo van web-app configureren pagina onder Hallo **domeinnamen** sectie.
* Uw aangepaste domeinnamen werkt zoals verwacht, maar in toevoeging tooadding ze tooyour web-apps, moet u ook uw DNS-kaart toopoint toohello Traffic Manager-URL configureren. Voor informatie over het tooset van een aangepast domein voor een Azure-web-app Zie [configureren van een aangepaste domeinnaam voor een Azure-website](app-service-web-tutorial-custom-domain.md).
* U kunt alleen web-apps die zich in de modus standard of premium tooa Azure Traffic Manager-profiel toevoegen.

## <a name="next-steps"></a>Volgende stappen
Zie voor een conceptuele en technisch overzicht van Azure Traffic Manager, [Traffic Manager-overzicht](../traffic-manager/traffic-manager-overview.md).

Zie voor meer informatie over het gebruik van Traffic Manager met Web-Apps Hallo blogberichten [met behulp van Azure Traffic Manager met Azure websites](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) en [Azure Traffic Manager kan nu worden geïntegreerd met Azure websites](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

