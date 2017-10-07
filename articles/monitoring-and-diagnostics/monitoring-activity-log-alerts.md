---
title: aaaCreate activiteit logboek waarschuwingen | Microsoft Docs
description: Een melding via SMS, webhook en e-mailbericht wanneer bepaalde in het gebeurtenissenlogboek Hallo gebeurtenissen.
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Logboek waarschuwingen voor de activiteit maken

## <a name="overview"></a>Overzicht
Activiteit logboek waarschuwingen zijn waarschuwingen die worden geactiveerd wanneer er een nieuwe activiteit logboekgebeurtenis optreedt die overeenkomt met de Hallo condities die zijn opgegeven in Hallo waarschuwing. Ze zijn Azure-resources, zodat ze kunnen worden gemaakt met behulp van een Azure Resource Manager-sjabloon. Ze kunnen ook worden gemaakt, bijgewerkt of verwijderd in hello Azure-portal. In dit artikel bevat Hallo concepten achter activiteit logboek waarschuwingen. Deze vervolgens ziet u hoe toouse hello Azure portal tooset van een waarschuwing op activiteit logboekgebeurtenissen.

Normaal gesproken u activiteitswaarschuwingen logboek tooreceive meldingen maken als:

* Specifieke wijzigingen optreden voor bronnen in uw Azure-abonnement, vaak bereik tooparticular resourcegroepen of bronnen. U kunt bijvoorbeeld toobe gewaarschuwd wanneer een virtuele machine in myProductionResourceGroup wordt verwijderd. Of u wellicht toobe melding als er geen nieuwe rollen tooa gebruiker in uw abonnement zijn toegewezen.
* Er treedt een gebeurtenis van de health service op. Gebeurtenissen van de health service omvatten melding van incidenten en het onderhoud van gebeurtenissen die van toepassing zijn tooresources in uw abonnement.

In beide gevallen controleert de activiteit logboek waarschuwing alleen voor gebeurtenissen in het Hallo-abonnement in welke Hallo waarschuwing is gemaakt.

U kunt een activiteit logboek waarschuwing op basis van een eigenschap op het hoogste niveau in JSON-object voor een activiteit van het gebeurtenislogboek Hallo configureren. Hallo portal ziet u echter Hallo meest voorkomende opties:

- **Categorie**: beheer-, status, automatisch schalen en aanbeveling. Zie voor meer informatie [overzicht van hello Azure activiteitenlogboek](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). toolearn meer informatie over gebeurtenissen van de health service, Zie [activiteit logboek meldingen ontvangen over servicemeldingen](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Resourcegroep**
- **Resource**
- **Brontype**
- **Naam van de bewerking**: naam van de bewerking Hallo Resource Manager-rollen gebaseerd toegangsbeheer.
- **Niveau**: Hallo ernst van gebeurtenis hello (uitgebreid, ter Info, waarschuwing, fout of kritiek).
- **Status**: Hallo status van de Hallo gebeurtenis, doorgaans gestart, is mislukt of geslaagd.
- **De gebeurtenis wordt gestart door**: ook wel bekend als Hallo "aanroeper." Hallo e-mailadres of Azure Active Directory-id van Hallo-gebruiker die Hallo bewerking uitgevoerd.

>[!NOTE]
>U moet ten minste twee Hallo criteria in de waarschuwing met één wordt vóór opgeven Hallo categorie. U kunt een waarschuwing die wordt geactiveerd telkens wanneer een gebeurtenis wordt gemaakt in Hallo activiteitenlogboeken niet maken.
>
>

Wanneer een activiteit logboek waarschuwing is geactiveerd, wordt een actie toogenerate acties of meldingen groeperen. Een actiegroep is een herbruikbare reeks melding ontvangers, zoals e-mailadressen, telefoonnummers webhook-URL's of SMS-bericht. Hallo ontvangers kunnen worden verwezen vanuit meerdere waarschuwingen toocentralize en groepeer de meldingskanalen. Wanneer u uw logboek activiteit waarschuwing definieert, hebt u twee opties. U kunt:

* Gebruik een bestaande actiegroep in de activiteit logboek-waarschuwing. 
* Maak een nieuwe actiegroep. 

toolearn meer informatie over het actiegroepen, Zie [maken en beheren van actiegroepen in hello Azure-portal](monitoring-action-groups.md).

toolearn meer informatie over servicestatusmeldingen, Zie [activiteit logboek meldingen ontvangen op servicestatusmeldingen](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Een waarschuwing op het gebeurtenislogboek van een activiteit met een nieuwe actiegroep maken met behulp van hello Azure-portal
1. In Hallo [portal](https://portal.azure.com), selecteer **Monitor**.

    ![Hallo 'Monitor'-service](./media/monitoring-activity-log-alerts/home-monitor.png)
2. In Hallo **activiteitenlogboek** sectie **waarschuwingen**.

    ![Hallo 'Waarschuwingen' tabblad](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Selecteer **toevoegen activiteit logboek waarschuwing**, en vul Hallo velden.

4. Voer een naam in Hallo **waarschuwing logboeknaam activiteit** vak en selecteer een **beschrijving**.

    ![opdracht 'Activiteit logboek waarschuwing toevoegen' Hallo](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Hallo **abonnement** vak autofills met uw huidige abonnement. Dit abonnement wordt Hallo een welke actie Hallo groep wordt opgeslagen. Waarschuwing Hallo-bron is geïmplementeerde toothis abonnement en monitors activiteit logboekgebeurtenissen uit.

    ![Hallo 'Activiteit logboek waarschuwing toevoegen' in het dialoogvenster](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Selecteer Hallo **resourcegroep** in welke Hallo waarschuwing resource is gemaakt. Dit is geen resourcegroep Hallo die wordt bewaakt door Hallo waarschuwing. Het is in plaats daarvan Hallo resourcegroep waar Hallo waarschuwing bron zich bevindt.

7. Selecteer desgewenst een **gebeurteniscategorie** toomodify Hallo meer filters die worden weergegeven. Voor administratieve gebeurtenissen Hallo filters omvatten **resourcegroep**, **Resource**, **brontype**, **bewerkingsnaam**, **Niveau**, **Status**, en **gebeurtenis wordt gestart door**. Deze waarden bepalen welke gebeurtenissen moet worden gecontroleerd door deze waarschuwing.

    >[!NOTE]
    >U moet ten minste één van de voorgaande criteria in de waarschuwing Hallo opgeven. U kunt een waarschuwing die wordt geactiveerd telkens wanneer een gebeurtenis wordt gemaakt in Hallo activiteitenlogboeken niet maken.
    >
    >

8. Voer een naam in Hallo **actie groepsnaam** vak en voer een naam in Hallo **afkorting** vak. Hallo korte naam wordt gebruikt in plaats van een volledige groep actienaam wanneer meldingen worden verzonden met behulp van deze groep.

9.  Een lijst van acties door te geven van de actie Hallo definiëren:

    a. **Naam**: Voer de naam, de alias of de id van Hallo actie.

    b. **Actietype**: Selecteer SMS, e-mail of webhook.

    c. **Details**: op basis van actietype hello, voer een telefoonnummer, e-mailadres of webhook URI.

10. Selecteer **OK** toocreate Hallo waarschuwing.

Hallo waarschuwing duurt een paar minuten toofully doorvoeren en vervolgens worden geactiveerd. Deze wordt geactiveerd wanneer nieuwe gebeurtenissen van het signaal Hallo vergelijkingscriteria.

Zie voor meer informatie [Understand Hallo webhook schema gebruikt in een logboek activiteitswaarschuwingen](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>Hallo actiegroep is gedefinieerd in deze stappen is herbruikbare als een bestaande actiegroep voor alle toekomstige definities van de waarschuwing.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Maken van een waarschuwing op het gebeurtenislogboek van een activiteit voor een bestaande actiegroep via hello Azure-portal
1. De stappen 1 tot en met 7 in de vorige sectie toocreate Hallo uw logboek activiteit waarschuwing.

2. Onder **melden**, selecteer Hallo **bestaande** actieknop groep. Selecteer een bestaande actiegroep in Hallo-lijst.

3. Selecteer **OK** toocreate Hallo waarschuwing.

Hallo waarschuwing duurt een paar minuten toofully doorvoeren en vervolgens worden geactiveerd. Deze wordt geactiveerd wanneer nieuwe gebeurtenissen van het signaal Hallo vergelijkingscriteria.

## <a name="manage-your-alerts"></a>Waarschuwingen beheren

Nadat u een waarschuwing gemaakt, is deze zichtbaar in Hallo in de sectie waarschuwingen van Hallo Monitor blade. Hallo waarschuwing die u wilt dat toomanage te selecteren:

* Bewerken.
* Verwijder de groep.
* - Of uitschakelen, als u stoppen tootemporarily wilt of ontvangen van meldingen voor Hallo waarschuwing hervat.

## <a name="next-steps"></a>Volgende stappen
- Ophalen van een [overzicht van waarschuwingen](monitoring-overview-alerts.md).
- Meer informatie over [melding snelheidsbeperking](monitoring-alerts-rate-limiting.md).
- Bekijk Hallo [activiteit logboek waarschuwing webhook schema](monitoring-activity-log-alerts-webhook.md).
- Meer informatie over [actiegroepen](monitoring-action-groups.md).  
- Meer informatie over [service health meldingen](monitoring-service-notifications.md).
- Maak een [activiteit Meld waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Maak een [activiteit Meld waarschuwing toomonitor alle mislukte automatisch schalen scale-in/scale-out-bewerkingen op uw abonnement](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
