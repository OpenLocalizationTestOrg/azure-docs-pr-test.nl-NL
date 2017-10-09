---
title: aaaReceive activiteit logboek waarschuwingen op servicemeldingen | Microsoft Docs
description: Blijf op de hoogte via SMS of e-mail webhook wanneer Azure service optreedt.
author: johnkemnetz
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
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Het maken van de activiteit logboek waarschuwingen op servicemeldingen
## <a name="overview"></a>Overzicht
Dit artikel laat zien hoe tooset up activiteitenlogboek van waarschuwingen voor servicestatusmeldingen met behulp van hello Azure-portal.  

U kunt een waarschuwing ontvangt wanneer Azure service health meldingen tooyour Azure-abonnement verzendt. U kunt op basis van Hallo-waarschuwing configureren:

- Hallo-klasse van service health melding (incident, onderhoud, gegevens, enzovoort).
- Hallo dienst(en) is van invloed op.
- Hallo regio('s) is van invloed op.
- de status van de Hallo Hallo melding (actieve versus opgelost).
- Hallo-niveau van het Hallo-meldingen (informatief, waarschuwing, fout).

Ook kunt u configureren die Hallo waarschuwing moet worden verzonden naar:

- Selecteer een bestaande actiegroep.
- Maak een nieuwe actiegroep (die kan worden gebruikt voor toekomstige waarschuwingen).

toolearn meer informatie over het actiegroepen, Zie [maken en beheren van actiegroepen](monitoring-action-groups.md).

Zie voor informatie over hoe tooconfigure service health mailmelding waarschuwingen met behulp van Azure Resource Manager-sjablonen, [Resource Manager-sjablonen](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Een waarschuwing op een melding van de health service voor een nieuwe actiegroep maken met behulp van hello Azure-portal
1. In Hallo [portal](https://portal.azure.com), selecteer **Monitor**.

    ![Hallo 'Monitor'-service](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. In Hallo **activiteitenlogboek** sectie **waarschuwingen**.

    ![Hallo 'Waarschuwingen' tabblad](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Selecteer **toevoegen activiteit logboek waarschuwing**, en vul Hallo velden.

    ![opdracht 'Activiteit logboek waarschuwing toevoegen' Hallo](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Voer een naam in Hallo **waarschuwing logboeknaam activiteit** vak en geef een **beschrijving**.

    ![Hallo 'Activiteit logboek waarschuwing toevoegen' in het dialoogvenster](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Hallo **abonnement** vak autofills met uw huidige abonnement. Dit abonnement is gebruikte toosave Hallo activiteit logboek waarschuwing. Waarschuwing Hallo-bron is geïmplementeerde toothis abonnement en monitors gebeurtenissen in Hallo activiteitenlogboek voor.

6. Selecteer Hallo **resourcegroep** in welke Hallo waarschuwing resource is gemaakt. Dit is niet Hallo resourcegroep die wordt bewaakt door Hallo waarschuwing. Het is in plaats daarvan Hallo resourcegroep waar Hallo waarschuwing bron zich bevindt.

7. In Hallo **gebeurteniscategorie** de optie **servicestatus**. Selecteer desgewenst Hallo **Service**, **regio**, **Type**, **Status**, en **niveau** van service Health-meldingen die u tooreceive wilt.

8. Onder **waarschuwing via**, selecteer Hallo **nieuw** actieknop groep. Voer een naam in Hallo **actie groepsnaam** vak en voer een naam in Hallo **afkorting** vak. de korte naam Hello wordt verwezen in Hallo-meldingen die worden verzonden wanneer deze waarschuwing wordt geactiveerd.

9. Een lijst met ontvangers door te geven van de ontvanger Hallo definiëren:

    a. **Naam**: Geef de naam, alias of id van de ontvanger Hallo.

    b. **Actietype**: Selecteer SMS, e-mail of webhook.

    c. **Details**: op basis van Hallo actietype gekozen, voer een telefoonnummer, e-mailadres of webhook URI.

10. Selecteer **OK** toocreate Hallo waarschuwing.

Binnen een paar minuten Hallo waarschuwing actief is en op basis van Hallo voorwaarden die u hebt opgegeven tijdens het maken van tootrigger begint.

Zie voor meer informatie over Hallo webhook schema voor de activiteit logboek waarschuwingen [Webhooks voor Azure activiteit waarschuwingen melden](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>Hallo actiegroep is gedefinieerd in deze stappen is herbruikbare als een bestaande actiegroep voor alle toekomstige definities van de waarschuwing.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Een waarschuwing op een melding van de health service voor een bestaande actiegroep maken met behulp van hello Azure-portal

1. De stappen 1 tot en met 7 in de vorige sectie toocreate Hallo de melding van de health service. 

2. Onder **waarschuwing via**, selecteer Hallo **bestaande** actieknop groep. Hallo gepaste actiegroep selecteren.

3. Selecteer **OK** toocreate Hallo waarschuwing.

Binnen een paar minuten Hallo waarschuwing actief is en op basis van Hallo voorwaarden die u hebt opgegeven tijdens het maken van tootrigger begint.

## <a name="manage-your-alerts"></a>Waarschuwingen beheren

Nadat u een waarschuwing gemaakt, is het zichtbaar in Hallo **waarschuwingen** sectie Hallo **Monitor** blade. Hallo waarschuwing die u wilt dat toomanage te selecteren:

* Bewerken.
* Verwijder de groep.
* - Of uitschakelen, als u stoppen tootemporarily wilt of ontvangen van meldingen voor Hallo waarschuwing hervat.

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [service health meldingen](monitoring-service-notifications.md).
- Meer informatie over [melding snelheidsbeperking](monitoring-alerts-rate-limiting.md).
- Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).
- Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over hoe tooreceive waarschuwingen. 
- Meer informatie over [actiegroepen](monitoring-action-groups.md).
