---
title: aaaWhat zijn Servicestatusmeldingen | Microsoft Docs
description: Servicestatusmeldingen kunnen dat u berichten van health service tooview publiceren door Microsoft Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Servicestatusmeldingen
## <a name="overview"></a>Overzicht

Dit artikel laat zien hoe tooview servicestatusmeldingen met hello Azure-portal.

Servicestatusmeldingen kunnen u tooview health serviceberichten gepubliceerd door hello Azure team dat Hallo resources in uw abonnement kan beïnvloeden. Deze meldingen zijn een subklasse zijn van de activiteit logboekgebeurtenissen en kunnen worden gevonden op Hallo activiteit logboek blade. Servicestatusmeldingen zijn informatief of actie worden uitgevoerd, afhankelijk van het Hallo-klasse.

Er zijn vijf soorten servicestatusmeldingen:  

- **De actie is vereist:** van tijd tootime we merkt ongewone activiteit optreden op uw account. We kunnen toowork met tooremedy u deze nodig. We sturen u een melding ofwel met gedetailleerde informatie over acties Hallo moet u tootake of met meer informatie over het toocontact Azure engineering of ondersteunen.  
- **Assisted Recovery:** een gebeurtenis heeft plaatsgevonden en engineers hebt bevestigd dat u nog steeds gevolgen ondervindt. Engineering toowork met u moet rechtstreeks toobring uw toorestoration services.  
- **Incident:** een service die van invloed op de gebeurtenis is momenteel die betrekking hebben op een of meer van de Hallo resources in uw abonnement.  
- **Onderhoud:** dit is een melding van een gepland onderhoud-activiteit die mogelijk van invloed op een of meer van de Hallo resources in uw abonnement.  
- **Gegevens:** van tijd tootime we sturen u mogelijk dat een tooyou communiceren over potentiële optimalisaties die kan helpen uw Resourcegebruik verbeteren meldingen.  
- **Beveiliging:** urgente beveiliging gerelateerde informatie met betrekking tot uw oplossing(en) uitgevoerd op Azure.

Elke melding van de health service zal details uitvoeren op Hallo bereik en de invloed tooyour bronnen. Bevat de details:

De naam van eigenschap | Beschrijving
-------- | -----------
kanalen | Is een van de volgende waarden Hallo: 'Admin', 'Operation'
correlationId | Is meestal een GUID in de indeling van tekenreeks Hallo. Gebeurtenissen met die deel uitmaken van dezelfde uber actie meestal delen toohello dezelfde correlationId Hallo.
eventDataId | Hallo unieke id van een gebeurtenis is
EventName | Titel van de gebeurtenis Hallo Hallo is
niveau | Niveau van het Hallo-gebeurtenis. Een van de volgende waarden Hallo: 'Kritiek', 'Fout', 'Waarschuwing', 'Ter informatie' en 'Verbose'
resourceProviderName | Naam van de resourceprovider Hallo voor Hallo beïnvloed resource
resourceType| Hallo type resource Hallo beïnvloed resource
subStatus | Meestal Hallo HTTP-statuscode van de bijbehorende REST-aanroep hello, maar kan ook andere tekenreeksen met een beschrijving van een substatus, zoals deze algemene waarden bevatten: OK (HTTP-statuscode: 200), gemaakt (HTTP-statuscode: 201), geaccepteerde (HTTP-statuscode: 202), geen inhoud (HTTP Statuscode: 204), onjuiste aanvraag (HTTP-statuscode: 400), niet is gevonden (HTTP-statuscode: 404), Conflict (HTTP-statuscode: 409), interne serverfout (HTTP-statuscode: 500), Service niet beschikbaar (HTTP-statuscode: 503), time-out van Gateway (HTTP-statuscode: 504).
eventTimestamp | Tijdstempel wanneer het Hallo-gebeurtenis is gegenereerd door hello Azure-service verwerken Hallo aanvragen overeenkomende Hallo-gebeurtenis.
submissionTimestamp |   Tijdstempel wanneer het Hallo-gebeurtenis beschikbaar voor het uitvoeren van query's zijn geworden.
subscriptionId | Hallo Azure-abonnement in waarmee deze gebeurtenis is vastgelegd
status | Tekenreeks die Hallo status van Hallo-bewerking. Sommige algemene waarden zijn: In voortgang, geslaagd, mislukt, actief, opgelost gestart.
operationName | Naam van Hallo-bewerking.
category | 'ServiceHealth'
resourceId | Bron-id van Hallo beïnvloed resource.
Properties.title | Hallo gelokaliseerd titel in voor deze communicatie. Engels is de standaardtaal Hallo.
Properties.Communication | Hallo gelokaliseerd details Hallo communicatie met de HTML-opmaak. Engels is standaard Hallo.
Properties.incidentType | Mogelijke waarden: AssistedRecovery, ActionRequired, informatie, Incident-, onderhoud, beveiliging
Properties.trackingId | Identificeert Hallo incident die deze gebeurtenis is gekoppeld. Gebruik dit incident toocorrelate Hallo-gebeurtenissen gerelateerde tooan.
Properties.impactedServices | Een escape-teken JSON-blob waarin Hallo services en regio's die worden beïnvloed door Hallo incident worden beschreven. Een lijst met Services, die allemaal een servicenaam en een lijst met ImpactedRegions, die allemaal een RegionName.
Properties.defaultLanguageTitle | Hallo-communicatie in het Engels
Properties.defaultLanguageContent | Hallo-communicatie in het Engels als HTML-indeling of tekst zonder opmaak
Properties.Stage | Mogelijke waarden voor AssistedRecovery, ActionRequired, informatie, Incident-, beveiliging: actief, zijn opgelost. Ze zijn voor onderhoud: actief, gepland, InProgress, geannuleerd, Rescheduled, opgelost, voltooid
Properties.communicationId | Hallo communicatie deze gebeurtenis is gekoppeld.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Uw servicestatusmeldingen weergeven in hello Azure-portal
1.  In Hallo [portal](https://portal.azure.com), navigeer toohello **Monitor** service

    ![Bewaken](./media/monitoring-service-notifications/home-monitor.png)
2.  Klik op Hallo **Monitor** optie tooopen up Hallo Monitor blade. In deze blade zijn al uw controle-instellingen en -gegevens bijeengebracht in één geconsolideerde weergave. Het eerst wordt geopend toohello **activiteitenlogboek** sectie.

3.  Klik nu op **servicemeldingen** sectie

    ![Bewaken](./media/monitoring-service-notifications/service-health-summary.png)
4.  Klik op een van de Hallo artikelen tooview meer informatie

5. Klik op Hallo **+ activiteit logboek waarschuwing toevoegen** bewerking tooreceive meldingen tooensure u wordt gewaarschuwd voor toekomstige servicemeldingen van dit type. meer informatie over het configureren van waarschuwingen op servicemeldingen toolearn [Klik hier](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Volgende stappen
Ontvangen [meldingen wanneer een melding van de health service](monitoring-activity-log-alerts-on-service-notifications.md) wordt gepost  
Meer informatie over [activiteit logboek waarschuwingen](monitoring-activity-log-alerts.md)
