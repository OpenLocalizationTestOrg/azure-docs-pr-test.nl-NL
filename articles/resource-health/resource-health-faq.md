---
title: aaaAzure resourcestatus Veelgestelde vragen | Microsoft Docs
description: Overzicht van Azure-resourcestatus
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: 5c5cfa116340094ffb1d6d5b206a11d389a0305a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a>Azure resourcestatus Veelgestelde vragen
Meer informatie over Hallo antwoorden toocommon vragen over Azure resourcestatus.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen
* [Wat is Azure Resource Health?](#what-is-azure-resource-health)
* [Wat is de resourcestatus Hallo bedoeld?](#what-is-the-resource-health-intended-for)
* [Welke controles worden uitgevoerd door de resourcestatus?](#what-health-checks-are-performed-by-resource-health)
* [Wat betekent elk van de gezondheidsstatus Hallo?](#what-does-each-of-the-health-status-mean)
* [Wat onbekende status gemiddelde Hallo? Er is iets mis met mijn resource?](#what-does-the-unknown-status-mean-is-something-wrong-with-my-resource)
* [Hoe krijg hulp voor een resource die niet beschikbaar is?](#how-can-i-get-help-for-a-resource-that-is-unavailable)
* [Resourcestatus onderscheid maken tussen niet beschikbaar zijn geïntegreerd met problemen versus iets die ik deed-platform?](#does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did)
* [Kan ik resourcestatus worden geïntegreerd met mijn controleprogramma's?](#can-i-integrate-resource-health-with-my-monitoring-tools)
* [Waar vind ik resourcestatus](#where-do-i-find-resource-health)
* [Resourcestatus beschikbaar is voor alle brontypen?](#is-resource-health-available-for-all-resource-types)
* [Wat moet ik doen als mijn resource wordt weergegeven als beschikbaar, maar ik zijn ervan overtuigd dat het niet?](#what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not)
* [Resourcestatus beschikbaar is voor alle Azure-regio's?](#is-resource-health-available-for-all-azure-regions)
* [Hoe verschilt resourcestatus van Hallo Service Health Dashboard of hello Azure portal servicemeldingen?](#how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications)
* [Moet ik de resourcestatus tooactivate voor elke resource?](#do-i-need-to-activate-resource-health-for-each-resource)
* [Hebben we de resourcestatus tooenable nodig voor mijn organisatie?](#do-we-need-to-enable-resource-health-for-my-organization)
* [Resourcestatus beschikbaar is gratis?](#is-resource-health-available-free-of-charge)
* [Wat zijn Hallo aanbevelingen die resourcestatus biedt?](#what-are-the-recommendations-that-resource-health-provides)


## <a name="what-is-azure-resource-health"></a>Wat is Azure-resourcestatus?
Resource Health helpt u bij het diagnosticeren en krijgen van ondersteuning wanneer een Azure-probleem van invloed is op uw resources. Dit biedt u informatie over de huidige en eerdere status Hallo van uw resources en helpt u problemen verhelpen. Resource Health biedt technische ondersteuning als u hulp nodig heeft bij problemen met Azure-services.  

## <a name="what-is-hello-resource-health-intended-for"></a>Wat is de resourcestatus Hallo bedoeld?
Zodra er een probleem met een bron is gedetecteerd, kunt resourcestatus u Hallo hoofdoorzaak onderzoeken. Biedt help toomitigate Hallo probleem en de technische ondersteuning als u meer hulp nodig bij problemen met de Azure-service.

## <a name="what-health-checks-are-performed-by-resource-health"></a>Welke controles worden uitgevoerd door de resourcestatus?
Resourcestatus voert diverse controles op basis van Hallo [brontype](resource-health-checks-resource-types.md). Deze controles worden ontworpen tooimplement drie typen problemen: 
1. Niet-geplande gebeurtenissen, bijvoorbeeld een onverwachte host opnieuw worden opgestart
2. Geplande gebeurtenissen, zoals geplande hostbesturingssysteem updates
3. Gebeurtenissen die worden geactiveerd door acties van gebruikers, bijvoorbeeld een gebruiker een virtuele machine opnieuw opstarten

## <a name="what-does-each-of-hello-health-status-mean"></a>Wat betekent elk van de gezondheidsstatus Hallo?
Er zijn drie verschillende health-statussen:
1. Beschikbaar: Er zijn geen bekende problemen in hello Azure-platform die kan van invloed op deze bron
2. Niet beschikbaar: Resourcestatus heeft gevonden problemen die van invloed zijn op de Hallo resource
3. Onbekende: Resourcestatus kan niet bepalen Hallo status van een resource omdat deze informatie over deze ontvangst is gestopt. 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a>Wat onbekende status gemiddelde Hallo? Er is iets mis met mijn resource?
Hallo gezondheidsstatus ingesteld toounknown wanneer resourcestatus ontvangt geen informatie over een specifieke bron. Terwijl deze status is niet een definitieve indicatie van Hallo status van Hallo-bron, in gevallen waar zich problemen voordoen, kan dit duiden dat er is een probleem met Azure.

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a>Hoe krijg hulp voor een resource die niet beschikbaar is?
U kunt een ondersteuningsaanvraag vanaf de resourceblade health Hallo verzenden. U hoeft niet een support-overeenkomst met Microsoft tooopen een aanvraag wanneer Hallo resource niet beschikbaar is omdat de platform-gebeurtenissen.

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a>Resourcestatus onderscheid maken tussen niet beschikbaar zijn geïntegreerd met problemen versus iets die ik deed-platform?
Ja, wanneer een bron niet beschikbaar is, identificeert resourcestatus Hallo hoofdoorzaak binnen één van deze categorieën: 
1.  Gebruiker gestarte actie
2.  Geplande gebeurtenis 
3.  Niet-geplande gebeurtenis

Acties van de gebruiker gestarte worden weergegeven met een blauw pictogram tijdens geplande en ongeplande gebeurtenissen worden weergegeven met behulp van een rood waarschuwingspictogram in Hallo-portal. Meer informatie vindt u in Hallo [health Bronnenoverzicht](Resource-health-overview.md).  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a>Kan ik resourcestatus worden geïntegreerd met mijn controleprogramma's?
De resourcestatus is een service die is ontworpen toohelp u onderzoeken en verhelpen van problemen met de Azure-service die invloed zijn op uw resources. Hoewel u gebruik kunt maken Hallo resource health API tooprogrammatically Hallo gezondheidsstatus verkrijgen, is het raadzaam dat u metrische gegevens toomonitor uw resources gebruiken. Zodra er een probleem is gedetecteerd, resourcestatus kunt u beter bepalen van de hoofdoorzaak Hallo en leidt u door acties tooaddress ze. Ga naar [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn meer informatie over het gebruik van metrische gegevens toocheck uw resources.

## <a name="where-do-i-find-resource-health"></a>Waar vind ik resourcestatus
Nadat u zich aanmeldt toohello Azure-portal, zijn er meerdere manieren u toegang hebt tot resourcestatus:
1. Navigeer tooyour resource. Klik in de linkernavigatiebalk hello, **resourcestatus**.
2. Ga toohello Azure Monitor blade.  Klik in de linkernavigatiebalk hello, **resourcestatus**.
3. Open Hallo **Help + ondersteuning** blade door te klikken op Hallo vraagteken in Hallo rechtsboven Hallo-portal en vervolgens te klikken op **Help + ondersteuning**. Zodra het Hallo-blade wordt geopend, klikt u op **resourcestatus**

U kunt ook de resourcestatus Hallo API tooobtain informatie over Hallo status van uw resources gebruiken.

## <a name="is-resource-health-available-for-all-resource-types"></a>Resourcestatus beschikbaar is voor alle brontypen?
Hallo lijst van statuscontroles en resourcetypen ondersteund via resourcestatus vindt [hier](resource-health-checks-resource-types.md)

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a>Wat moet ik doen als mijn resource wordt weergegeven als beschikbaar, maar ik zijn ervan overtuigd dat het niet?"
Hallo-status van een bron wordt gecontroleerd, direct onder de gezondheidsstatus Hallo kunt u **rapporteren onjuist gezondheidsstatus**. Vóór het Hallo-rapport verzenden, hebt u Hallo mogelijkheid biedt aanvullende details over waarom u denkt dat met het huidige status van Hallo is onjuist.

## <a name="is-resource-health-available-for-all-azure-regions"></a>Resourcestatus beschikbaar is voor alle Azure-regio's? 
De resourcestatus is beschikbaar in over alle Azure geografische gebieden behalve Hallo gebieden te volgen:
* VS (overheid) - Virginia
* VS (overheid) - Iowa
* US DoD - oost
* US DoD - centraal
* Duitsland - centraal
* Duitsland - noordoost
* China - oost
* China - noord

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a>Hoe verschilt resourcestatus van Hallo Service Health Dashboard of hello Azure portal servicemeldingen?
Hallo-informatie die door de resourcestatus is specifieker dan is opgegeven door hello Azure Service Health Dashboard.

Terwijl [Azure Status](https://status.azure.com) en Hallo portal servicemeldingen u wordt geïnformeerd over problemen met de service die invloed hebben op een uitgebreide reeks klanten (bijvoorbeeld een Azure-regio), resourcestatus beschrijft gedetailleerdere gebeurtenissen die alleen relevant zijn toohello bepaalde resource. Als een host onverwacht opnieuw wordt opgestart waarschuwingen resourcestatus alleen klanten waarvan virtuele machines zijn uitgevoerd op die host.

Het is belangrijk toonotice die tooprovide voltooien van de zichtbaarheid van gebeurtenissen die invloed hebben op uw resources, resourcestatus geeft ook weer gebeurtenissen die zijn gepubliceerd in servicemeldingen en Hallo Service Health Dashboard.

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a>Moet ik de resourcestatus tooactivate voor elke resource?
Nee, de statusgegevens zijn beschikbaar voor alle resourcetypen beschikbaar via de resourcestatus. 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a>Hebben we de resourcestatus tooenable nodig voor mijn organisatie?
Nee.  Status van de Azure-resource is toegankelijk vanuit hello Azure-portal zonder eventuele installatievereisten.

## <a name="is-resource-health-available-free-of-charge"></a>Resourcestatus beschikbaar is gratis?
Ja.  De status van de Azure-resource is gratis.

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a>Wat zijn Hallo aanbevelingen die resourcestatus biedt?
Op basis van de gezondheidsstatus van hello, biedt resourcestatus u aanbevelingen met Hallo doel van verminderde Hallo u besteed aan het oplossen van problemen. Voor de beschikbare bronnen richt Hallo aanbevelingen u op hoe toosolve Hallo meest voorkomende problemen klanten optreden. Als het Hallo-bron is niet beschikbaar vanwege tooan Azure niet-geplande gebeurtenis, Hallo focus worden uitgevoerd in die u helpt tijdens en na het herstelproces Hallo. 

## <a name="next-steps"></a>Volgende stappen

Bekijk deze resources toolearn meer informatie over de resourcestatus:
-  [Overzicht van Azure-resource-status](Resource-health-overview.md)
-  [Brontypen en statuscontroles beschikbaar via Azure Resource Health](resource-health-checks-resource-types.md)
