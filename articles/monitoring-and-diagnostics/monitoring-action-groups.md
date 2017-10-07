---
title: aaaCreate en beheren van actiegroepen in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe toocreate actiegroepen in hello Azure-portal en beheren.
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
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Actiegroepen in hello Azure-portal maken en beheren
## <a name="overview"></a>Overzicht ##
Dit artikel ziet u hoe toocreate actiegroepen in hello Azure-portal en beheren.

U kunt een lijst van acties met actiegroepen configureren. Deze groepen kunnen vervolgens worden gebruikt wanneer u activiteitswaarschuwingen logboekbestand definieert. Deze groepen kunnen vervolgens worden hergebruikt door elke activiteit logboek waarschuwing die u hebt gedefinieerd, waarbij u ervoor zorgt dat Hallo dezelfde acties worden uitgevoerd elke keer Hallo activiteit logboek waarschuwing wordt geactiveerd.

Een actiegroep kan up too10 van elk actietype hebben. Elke actie bestaat uit Hallo volgende eigenschappen:

* **Naam**: een unieke id binnen Hallo actiegroep.  
* **Actietype**: een SMS-bericht verzenden, e-mailbericht verzenden of een webhook aanroepen.  
* **Details**: Hallo overeenkomende telefoonnummer of e-mailadres webhook URI.

Voor meer informatie over toouse Azure Resource Manager-sjablonen tooconfigure actiegroepen, Zie [actie groep Resource Manager-sjablonen](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Een actiegroep maken met behulp van hello Azure-portal ##
1. In Hallo [portal](https://portal.azure.com), selecteer **Monitor**. Hallo **Monitor** blade consolideert alle controle-instellingen en gegevens in één weergave.

    ![Hallo 'Monitor'-service](./media/monitoring-action-groups/home-monitor.png)
2. In Hallo **activiteitenlogboek** sectie **actiegroepen**.

    ![tabblad van Hallo 'actiegroepen'](./media/monitoring-action-groups/action-groups-blade.png)
3. Selecteer **actie-groep toevoegen**, en vul Hallo velden.

    ![opdracht 'actiegroep toevoegen' Hallo](./media/monitoring-action-groups/add-action-group.png)
4. Voer een naam in Hallo **actie groepsnaam** vak en voer een naam in Hallo **afkorting** vak. Hallo korte naam wordt gebruikt in plaats van een volledige groep actienaam wanneer meldingen worden verzonden met behulp van deze groep.

      ![groepsdialoogvenster van Hallo toevoegen actie'](./media/monitoring-action-groups/action-group-define.png)

5. Hallo **abonnement** vak autofills met uw huidige abonnement. Dit abonnement wordt Hallo een welke actie Hallo groep wordt opgeslagen.

6. Selecteer Hallo **resourcegroep** in welke actie u Hallo groep wordt opgeslagen.

7. Een lijst van acties door te geven van de actie definiëren:

    a. **Naam**: Voer een unieke id voor deze actie.

    b. **Actietype**: Selecteer SMS, e-mail of webhook.

    c. **Details**: op basis van actietype hello, voer een telefoonnummer, e-mailadres of webhook URI.

8. Selecteer **OK** toocreate Hallo actiegroep.

## <a name="manage-your-action-groups"></a>Actiegroepen beheren ##
Nadat u een actiegroep maakt, is zichtbaar in Hallo **actiegroepen** sectie Hallo **Monitor** blade. Selecteer een Hallo actiegroep toomanage naar:

* Toevoegen, bewerken of verwijderen van acties.
* Hallo actiegroep verwijderen.

## <a name="next-steps"></a>Volgende stappen ##
* Meer informatie over [SMS waarschuwing gedrag](monitoring-sms-alert-behavior.md).  
* Krijgen een [begrip van Hallo activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).  
* Meer informatie over [snelheidsbeperking](monitoring-alerts-rate-limiting.md) van waarschuwingen. 
* Ophalen van een [overzicht van de activiteit logboek waarschuwingen](monitoring-overview-alerts.md), en meer informatie over hoe tooreceive waarschuwingen.  
* Meer informatie over hoe te[waarschuwingen configureren wanneer een melding van de health service wordt geboekt](monitoring-activity-log-alerts-on-service-notifications.md).
