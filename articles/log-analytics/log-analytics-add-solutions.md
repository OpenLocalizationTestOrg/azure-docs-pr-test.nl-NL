---
title: oplossingen voor het beheer van Azure-logboekanalyse aaaAdd | Microsoft Docs
description: Operations Management Suite (OMS) / Log Analytics beheeroplossingen zijn een verzameling logica, visualiseren en gegevens overname regels waarmee de metrische gegevens om een bepaald probleemgebied wordt gedraaid.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f029dd6d-58ae-42c5-ad27-e6cc92352b3b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5a232d20e144b800387b09adb5248505d801944
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-azure-log-analytics-management-solutions-tooyour-workspace"></a>Azure Log Analytics management oplossingen tooyour werkruimte toevoegen

Log Analytics-oplossingen voor beheer zijn een verzameling **logica**, **visualisatie**, en **gegevens overname regels** die metrische gegevens om een bepaalde gedraaid bieden probleemgebied. In dit artikel bevat oplossingen voor het beheer wordt ondersteund door Log Analytics en ziet u hoe Hallo tooadd en verwijderen voor een werkruimte met behulp van Azure-portal. U kunt ook oplossingen op Hallo OMS-portal met Hallo oplossingen galerie toevoegen.

Oplossingen voor toestaan meer inzicht te:

* Te onderzoeken en oplossen van operationele problemen sneller
* Verzamelen en verschillende soorten gegevens van de machine correleren
* Kunt u actie moet ondernemen met activiteiten die Hallo oplossing beschrijft.

> [!NOTE]
> Log Analytics bevat logboek zoekfunctionaliteit, dus u een solution management tooenable tooinstall hoeft deze. Echter, krijgt u gegevensvisualisaties, voorgestelde zoekopdrachten en inzichten door management oplossingen tooyour werkruimte toe te voegen.

Met dit artikel toevoegen u management oplossingen tooa werkruimte met hello Azure-portal Marketplace. Nadat u een oplossing hebt toegevoegd, worden gegevens verzameld van servers in uw infrastructuur Hallo en toohello OMS-service verzonden. Verwerking door Hallo OMS-service normaal gesproken een paar minuten tooan uur duurt. Nadat de service Hallo Hallo gegevens verwerkt, kunt u deze bekijken in OMS.

Wanneer deze niet langer nodig is, kunt u eenvoudig een oplossing voor het beheer verwijderen. Wanneer u een oplossing voor het beheer verwijdert, wordt de gegevens niet tooOMS verzonden. Als u van de gratis prijscategorie hello gebruikmaakt, kunt verwijderen van een oplossing Hallo hoeveelheid gegevens die worden gebruikt, zodat u kunt blijven onder dagelijkse quotum van de gegevens beperken.

## <a name="view-available-management-solutions"></a>Weergave beschikbaar oplossingen

Hello Azure marketplace bevat Hallo lijst met [beheeroplossingen voor logboekanalyse](https://azuremarketplace.microsoft.com/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

U kunt beheeroplossingen vanuit Azure marketplace installeren door te klikken op Hallo **nu downloaden** koppeling onderin Hallo van elke oplossing.

## <a name="add-a-management-solution"></a>Toevoegen van een beheeroplossing
1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com) met behulp van uw Azure-abonnement.
2. In Hallo **nieuw** blade onder **Marketplace**, selecteer **bewaking + management**.
3. In Hallo **bewaking + management** blade, klikt u op **alle**.  
    ![Bewaking + beheerblade](./media/log-analytics-add-solutions/monitoring-management-blade.png)  
4. toohello rechts van **beheeroplossingen**, klikt u op **meer**.
5. In Hallo **beheeroplossingen** blade, selecteert u een oplossing die u wilt dat tooadd tooa werkruimte.  
    ![Bewaking + beheerblade](./media/log-analytics-add-solutions/management-solutions.png)  
6. Lees de informatie over de oplossing voor het beheer van Hallo Hallo management oplossing blade en klik vervolgens op **maken**.
7. In Hallo *management oplossingsnaam* blade, selecteert u een werkruimte die u tooassociate met Hallo-beheeroplossing wilt.
8. Wijzig eventueel de werkruimte-instellingen voor hello Azure-abonnement, resourcegroep en locatie. U kunt ook **automatiseringsopties**. Klik op **Create**.  
    ![werkruimte voor de oplossing](./media/log-analytics-add-solutions/solution-workspace.png)  
9. Gebruik Hallo beheeroplossing dat u hebt toegevoegd aan tooyour werkruimte toostart te navigeren**logboekanalyse** > **abonnementen** > ***Werkruimtenaam ***  >  **Overzicht**. Een nieuwe tegel voor uw beheeroplossing wordt weergegeven. Klik op Hallo tegel tooopen deze en start met behulp van Hallo oplossing nadat de gegevens voor Hallo oplossing zijn verzameld.

## <a name="remove-a-management-solution"></a>Een oplossing voor het beheer verwijderen

1. In Hallo [Azure-portal](https://portal.azure.com), te navigeren**logboekanalyse** > **abonnementen** > ***Werkruimtenaam*** en klik vervolgens in Hallo ***Werkruimtenaam*** blade, klikt u op **oplossingen**.
2. Selecteer in lijst Hallo van oplossingen voor Hallo-oplossing die u tooremove wilt.
3. Klik op Hallo oplossing blade voor uw werkruimte **verwijderen**.  
    ![oplossing verwijderen](./media/log-analytics-add-solutions/solution-delete.png)  
4. Klik in het dialoogvenster voor het bevestigen van Hallo op **Ja**.

## <a name="offers-and-pricing-tiers"></a>Aanbiedingen en Prijscategorieën

Hallo volgende tabel identificeert welke beheeroplossingen tooeach Operations Management Suite aanbieding behoren.
Hallo tabel identificeert ook Hallo Prijscategorieën die beschikbaar voor elk beheersysteem zijn.
Alle oplossingen in de volgende tabel hello, beschikbaar vanuit hello Azure portal en Hallo oplossingen-galerie in Hallo Log Analytics-portal.

| Oplossing voor het beheer                                                                       | Aanbieding                                                                     | Prijscategorieën<sup>1</sup>                                                 | Opmerkingen |
| ---                                                                                       | ---                                                                       | ---                                                                                                       | ---   |
| [Activity Log Analytics](log-analytics-activity.md)                                                                   | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | negentig dagen aan gegevens beschikbaar zijn gratis<br>Gegevens niet zijn onderworpen toohello gratis laag cap |
| [AD-evaluatie](log-analytics-ad-assessment.md)                                           | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [AD-replicatiestatus](log-analytics-ad-replication-status.md)                           | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [Status van agent](../operations-management-suite/oms-solution-agenthealth.md)                                                                                | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Gegevens niet zijn onderworpen toohello gratis laag cap<br> Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [Waarschuwingsbeheer](log-analytics-solution-alert-management.md)                            | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [Application Insights-Connector (Preview)](log-analytics-app-insights-connector.md)                                               | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Automation Hybrid Worker](../automation/automation-hybrid-runbook-worker.md)                                                                     | <ul><li>Automation en Control</li></ul>                                  | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | Uw logboekanalyse werkruimte toobe gekoppeld tooan Automation-account vereist |
| [Azure Application Gateway Analytics](log-analytics-azure-networking-analytics.md)    | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Netwerkbeveiligingsgroep Azure Analytics](log-analytics-azure-networking-analytics.md)     | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Azure SQL Analytics (Preview)](log-analytics-azure-sql.md)                                                       | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br>Per&nbsp;knooppunt&nbsp;(OMS)                                                                          | Uw logboekanalyse werkruimte toobe gekoppeld tooan Automation-account vereist|
| [Azure Web Apps-analyse](log-analytics-azure-web-apps-analytics.md)     | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
|[Een back-up maken](../backup/backup-introduction-to-azure-backup.md)                                                                                 | <ul><li>Inzicht en analyses</li></ul>                                   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                       | Vereist een klassieke Backup-kluis.<br> Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [Capaciteit en prestaties (Preview)](log-analytics-capacity.md)                                                   | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Tracering wijzigen](log-analytics-change-tracking.md)                                       | <ul><li>Automation en Control</li></ul>                                  | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | Uw logboekanalyse werkruimte toobe gekoppeld tooan Automation-account vereist |
| [Containers](log-analytics-containers.md)                                                 | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [IT Service Management-Connector (Preview)](log-analytics-itsmc-overview.md)                                              | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)     | |
| HDInsight HBase bewaking <br>(Preview)                                                  | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Key Vault-analyse](log-analytics-azure-key-vault.md)                   | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Logic Apps B2B](../logic-apps/logic-apps-track-b2b-messages-omsportal.md)                    | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [Malware-evaluatie](log-analytics-malware.md)                                            | <ul><li>Beveiliging en naleving</li></ul>                                 | Gratis<br> Zelfstandig<br>Per&nbsp;knooppunt&nbsp;(OMS)                                                                           | Als u de beveiliging en naleving oplossingen Hallo na 19 juni 2017 toevoegt [facturering per knooppunt is](https://azure.microsoft.com/pricing/details/security-compliance/), ongeacht van Hallo werkruimte prijscategorie. Hallo zijn eerste 60 dagen gratis.  |
| [Netwerkprestatiemeter](log-analytics-network-performance-monitor.md) <br>  | <ul><li>Inzicht en analyses</li></ul>                                   | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | |
| [Office 365 Analytics (Preview)](../operations-management-suite/oms-solution-office-365.md)                                                       | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Beveiliging en controle](../operations-management-suite/oms-security-getting-started.md)      | <ul><li>Beveiliging&nbsp;en&nbsp;naleving</li></ul>                       | Gratis<br> Zelfstandig<br>Per&nbsp;knooppunt&nbsp;(OMS)                                                                           | Deze oplossing vereist voor het verzamelen van gebeurtenislogboeken<br>Als u de beveiliging en naleving oplossingen Hallo na 19 juni 2017 toevoegt [facturering per knooppunt is](https://azure.microsoft.com/pricing/details/security-compliance/), ongeacht van Hallo werkruimte prijscategorie. Hallo zijn eerste 60 dagen gratis. |
| [Service Fabric Analytics (Preview)](log-analytics-service-fabric.md)                     | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Serviceoverzicht (Preview)](../operations-management-suite/operations-management-suite-service-map.md) | <ul><li>Inzicht en analyses</li></ul>                      | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | Beschikbaar in VS-Oost, West-Europa en West-Centraal VS    |
| [Site Recovery](../site-recovery/site-recovery-overview.md)                                                                               | <ul><li>Inzicht en analyses</li></ul>                                   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                       | Vereist een klassieke Site Recovery-kluis.<br> Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [SQL-evaluatie](log-analytics-sql-assessment.md)                                         | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| VM's starten/stoppen buiten kantooruren<br>(Preview)                                              | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | Uw logboekanalyse werkruimte toobe gekoppeld tooan Automation-account vereist |
| [SurfaceHub](log-analytics-surface-hubs.md)                                               | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [System Center Operations Manager Assessment (Preview)](log-analytics-scom-assessment.md)  | <ul><li>Inzicht en analyses</li><li>Log Analytics</li></ul>        | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Updatebeheer](../operations-management-suite/oms-solution-update-management.md)                                                                         | <ul><li>Automation en Control</li></ul>                                  | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | Uw logboekanalyse werkruimte toobe gekoppeld tooan Automation-account vereist |
| [Updatevereisten (Preview)](https://docs.microsoft.com/windows/deployment/update/update-compliance-get-started)                                                             | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Geen kosten voor gegevens of knooppunten<br>Gegevens niet zijn onderworpen toohello gratis laag cap.<br> Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [Gereedheid voor upgrade](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started)                                                          | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | Geen kosten voor gegevens of knooppunten<br>Gegevens niet zijn onderworpen toohello gratis laag cap.<br> Niet beschikbaar tooadd vanuit Azure portal/marketplace. |
| [VMware Monitoring (Preview)](log-analytics-vmware.md)                                | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Standard<br> Premium&nbsp;(OMS)<br> Per&nbsp;GB&nbsp;(zelfstandig)<br> Per&nbsp;knooppunt&nbsp;(OMS)   | |
| [Draadgegevens worden geleverd 2.0 (Preview)](log-analytics-wire-data.md)                                                                 | <ul><li>Inzicht en analyses</li></ul>                                   | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)                                                                         | Beschikbaar in VS-Oost, West-Europa en West-Centraal VS |

<sup>1</sup> hello *standaard* en *Premium (OMS)* Prijscategorieën zijn alleen beschikbaar voor klanten die hun logboekanalyse werkruimte voorafgaande tooSeptember 21 2016 gemaakt.

### <a name="community-provided-management-solutions"></a>Opgegeven beheeroplossingen community

Community opgegeven oplossingen beschikbaar zijn op Hallo [Azure sjablonengalerie](https://azure.microsoft.com/resources/templates/?term=Per&nbsp;Node&nbsp;(OMS)) en direct van Hallo auteurs.

| Oplossing voor het beheer               | Aanbieding                                                                     | Prijscategorieën                         | Opmerkingen |
| ---                               | ---                                                                       | ---                                   | ---   |
| Alle community opgegeven oplossingen  | <ul><li>Inzicht&nbsp;en&nbsp;Analytics</li><li>Log Analytics</li></ul>   | Gratis<br> Per&nbsp;knooppunt&nbsp;(OMS)     |   Uw logboekanalyse werkruimte toobe gekoppeld tooan Automation-account vereist |




## <a name="data-collection-details"></a>Details van de verzameling gegevens
Hallo volgende tabellen bevatten gegevens verzameling methoden en andere informatie over hoe gegevens worden verzameld voor Log Analytics management oplossingen en gegevensbronnen. Hallo tabellen worden ingedeeld in verschillende oplossing-aanbiedingen neer te[abonnement Prijscategorieën](https://go.microsoft.com/fwlink/?linkid=827926). Hallo activiteit Log Analytics-oplossing is beschikbaar tooall prijscategorie gratis.

Hallo Log Analytics Windows-agent en System Center Operations Manager agent zijn in feite Hallo dezelfde. Hallo Windows agent bevat aanvullende functionaliteit tooallow het tooconnect toohello OMS werkruimte en doorsturen via een proxy. Als u een Operations Manager-agent gebruikt, moet u deze als een OMS-agent toocommunicate met OMS gericht. Operations Manager-agenten in deze tabel zijn de OMS-agents die verbonden tooOperations Manager zijn. Zie [verbinding maken met Operations Manager tooLog Analytics](log-analytics-om-agents.md) voor informatie over het verbinden van uw bestaande tooOMS voor Operations Manager-omgeving.

> [!NOTE]
> Hallo-type van de agent die u gebruikt bepaalt hoe gegevens worden verzonden voor tooOMS, hello volgende voorwaarden:
> - U gebruikmaken van Windows-agent hello of een Operations Manager-attached OMS-agent.
> - Als Operations Manager vereist is, gegevens in Operations Manager-agent voor Hallo oplossing tooOMS Hallo Operations Manager-beheergroep met altijd verzonden. Bovendien, als Operations Manager vereist is, wordt alleen Hallo Operations Manager-agent gebruikt door Hallo oplossing.
> - Wanneer Operations Manager is niet vereist en Hallo tabel ziet u dat gegevens in Operations Manager-agent tooOMS met Hallo-beheergroep, wordt de gegevens in Operations Manager-agent wordt verzonden met behulp van beheergroepen tooOMS altijd verzonden. Windows-agents overslaan Hallo-beheergroep en verzenden van hun gegevens rechtstreeks tooOMS.
> - Wanneer gegevens in Operations Manager-agent niet met behulp van een beheergroep verzonden is, gegevens worden dan Hallo verzonden rechtstreeks tooOMS: omzeilen Hallo-beheergroep.

### <a name="insight--analytics--log-analytics"></a>Inzicht & Analytics / Log Analytics

| Oplossing voor het beheer | Platform | Microsoft monitoring agent | Operations Manager-agent | Azure-opslag | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Analyse van activiteitenlogboek | Azure |   |   |   |   |   | op de melding |
| AD-evaluatie |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dagen |
| AD-replicatiestatus |Windows |&#8226; |&#8226; |  |  |&#8226; |Er zijn vijf dagen |
| Status van agent | Windows- en Linux | &#8226; | &#8226; |   |   | &#8226; | 1 minuut |
| Beheer van waarschuwingen (Nagios) |Linux |&#8226; |  |  |  |  |bij ontvangst |
| Beheer van waarschuwingen (Zabbix) |Linux |&#8226; |  |  |  |  |1 minuut |
| Beheer van waarschuwingen (Operations Manager) |Windows |  |&#8226; |  |&#8226; |&#8226; |3 minuten |
| Application Insights-Connector (Preview) | Azure |   |   |   |   |   | op de melding |
| Azure Application Gateway Analytics | Azure |   |   |   |   |   | op de melding |
| Netwerkbeveiligingsgroep Azure Analytics | Azure |   |   |   |   |   | op de melding |
| Azure SQL Analytics (Preview) |Windows |  |  |  |  |  | 10 minuten |
| Capaciteitsbeheer |Windows |&#8226; |&#8226; |  |  |&#8226; |bij ontvangst |
| Containers | Windows- en Linux | &#8226; | &#8226; |   |   |   | 3 minuten |
| Sleutelkluis Analytics |Windows |  |  |  |  |  |op de melding |
| Netwerkprestatiemeter | Windows | &#8226; | &#8226; |   |   |   | TCP-handshakes om de vijf seconden gegevens verzonden om de 3 minuten |
| Office 365 Analytics (Preview) |Windows |  |  |  |  |  |op de melding |
| Service Fabric Analytics |Windows |  |  |&#8226; |  |  |5 minuten |
| Serviceoverzicht | Windows- en Linux | &#8226; | &#8226; |   |   |   | 15 seconden |
| SQL-evaluatie |Windows |&#8226; |&#8226; |  |  |&#8226; |7 dagen |
| SurfaceHub |Windows |&#8226; |  |  |  |  |bij ontvangst |
| System Center Operations Manager Assessment (Preview) | Windows | &#8226; | &#8226; |   |   | &#8226; | zeven dagen |
| Upgrade Analytics (Preview) | Windows | &#8226; |   |   |   |   | 2 dagen |
| VMware Monitoring (Preview) | Linux | &#8226; |   |   |   |   | 3 minuten |
| Bedradingsgegevens |Windows (2012 R2 / 8.1 of hoger) |&#8226; |&#8226; |  |  |  | 1 minuut |


### <a name="automation--control"></a>Automation en besturing

| Oplossing voor het beheer | Platform | Microsoft monitoring agent | Operations Manager-agent | Azure-opslag | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Automation Hybrid Worker | Windows | &#8226; | &#8226; |   |   |   | N.v.t. |
| Tracering wijzigen |Windows |&#8226; |&#8226; |  |  |&#8226; |elk uur |
| Tracering wijzigen |Linux |&#8226; |  |  |  |  |elk uur |
| Updatebeheer | Windows |&#8226; |&#8226; |  |  |&#8226; |ten minste 2 keer per dag en 15 minuten nadat u een update installeert |

### <a name="security--compliance"></a>Beveiliging en naleving

| Oplossing voor het beheer | Platform | Microsoft monitoring agent | Operations Manager-agent | Azure-opslag | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Evaluatie van Antimalware |Windows |&#8226; |&#8226; |  |  |&#8226; |elk uur |
| Beveiliging en Audit<sup>1</sup> | Windows- en Linux | gedeeltelijke | gedeeltelijke | gedeeltelijke |   | gedeeltelijke | verschillende |

<sup>1</sup> Hallo beveiliging en Audit-oplossing kunt verzamelen van Logboeken van Windows-, Operations Manager- en Linux-agents. Zie [gegevensbronnen](#data-sources) voor gegevens verzamelen informatie over:

- Syslog
- Windows-beveiligingslogboek
- Windows firewall-Logboeken
- Windows-gebeurtenislogboeken



### <a name="protection--recovery"></a>Beveiliging en herstel

| Oplossing voor het beheer | Platform | Microsoft monitoring agent | Operations Manager-agent | Azure-opslag | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Back-up | Azure |   |   |   |   |   | N.v.t. |
| Azure Site Recovery | Azure |   |   |   |   |   | N.v.t. |


### <a name="data-sources"></a>Gegevensbronnen


| Gegevensbron | Platform | Microsoft monitoring agent | Operations Manager-agent | Azure-opslag | Operations Manager is vereist? | Operations Manager-agent gegevens verzonden via de beheergroep | Verzamelingsfrequentie |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Azure activiteitenlogboeken |Windows |  |  |  |  |  |op de melding |
| Azure diagnostische logboeken |Windows |  |  |  |  |  |op de melding |
| Azure diagnostische metrische gegevens |Windows |  |  |  |  |  |op de melding |
| ETW |Windows |  |  |&#8226; |  |  |5 minuten |
| IIS-logboeken |Windows |&#8226; |&#8226; |&#8226; |  |  |5 minuten |
| Prestatiemeteritems |Windows |&#8226; |&#8226; |  |  |  |Als gepland, minimaal 10 seconden |
| Prestatiemeteritems |Linux |&#8226; |  |  |  |  |Als gepland, minimaal 10 seconden |
| Syslog |Linux |&#8226; |  |  |  |  |naar Azure storage: 10 minuten. Agent: bij ontvangst |
| Windows-beveiligingslogboek |Windows |&#8226; |&#8226; |&#8226; |  |  |voor Azure storage: 10 minuten; voor de agent Hallo: bij ontvangst |
| Windows firewall-Logboeken |Windows |&#8226; |&#8226; |  |  |  |bij ontvangst |
| Windows-gebeurtenislogboeken |Windows |&#8226; |&#8226; |&#8226; |  |&#8226; |voor Azure storage: 10 minuten; voor de agent Hallo: bij ontvangst |



## <a name="preview-management-solutions-and-features"></a>Preview oplossingen en functies
Door een service wordt uitgevoerd en devops procedures te volgen, zijn we kunnen toopartner met klanten toodevelop functies en oplossingen.

Tijdens de Preview-versie voor de private we een kleine groep klanten toegang tooan vroege uitvoering van Hallo functie of oplossing toogain feedback geven en verbeteringen. Deze vroege implementatie heeft minimale functies en operationele mogelijkheden.

Ons doel is snel tootry dingen zodat we vinden kunnen wat werkt en wat niet werkt. We doorlopen dit proces totdat Hallo feedback van Hallo private preview klanten ons meldt dat we klaar zijn voor een openbare preview.

Tijdens de openbare preview hello, we Hallo functie of oplossing beschikbaar maken voor alle gebruikers tooget meer feedback en valideren van onze schalen en efficiëntie. Tijdens deze fase:

* Preview-functies weergegeven in het tabblad Hallo-instellingen en kunnen worden ingeschakeld door een gebruiker.
* Preview-oplossingen worden toegevoegd via Hallo galerie of met een script.

### <a name="what-should-i-know-about-preview-features-and-solutions"></a>Wat moet ik weten over de Preview-functies en oplossingen
We zijn blij met nieuwe functies en oplossingen voor het beheer en we graag werken met toodevelop u ze.

Zijn niet geschikt is voor iedereen Preview-functies en oplossingen. Toojoin waarin wordt gevraagd Controleer een Preview-versie private of het inschakelen van een openbare preview voordat u OK werkt met iets dat nog in ontwikkeling.

Bij het inschakelen van een preview-functie via de portal hello, ziet u een waarschuwing om eraan te herinneren dat de functie Hallo is Preview-versie.

#### <a name="for-both-private-and-public-preview"></a>Voor beide *persoonlijke* en *openbare* preview
Hallo volgende informatie is van toepassing tooboth openbare en persoonlijke previews:

* Dingen werken niet altijd correct.
  * Bereik van een secundaire hinder via toosomething werkt niet op alle wordt verstrekt.
* Er is mogelijk voor Hallo preview toohave een negatieve invloed op uw systemen / omgeving.
  * We proberen tooavoid negatieve dingen gebeurt toohello systemen die u met OMS, maar soms onverwachte dingen optreden.
* Gegevensverlies / beschadigd raken.
* We kunnen vragen u toocollect diagnostische logboeken of andere gegevens toohelp oplossen van problemen.
* Hallo-onderdeel of deze oplossing kan worden verwijderd (tijdelijk of permanent).
  * Op basis van onze geleerde lessen tijdens Hallo preview besluiten we toonot release Hallo functie of oplossing.
* Voorbeelden werkt mogelijk niet of niet getest met alle configuraties en we kunnen beperken:
  * Hallo besturingssystemen die kunnen worden gebruikt (bijvoorbeeld, een functie kan alleen van toepassing tooLinux in de preview).
  * Hallo-type van de agent (MMA, Operations Manager) die kan worden gebruikt (bijvoorbeeld, een functie werkt niet met Operations Manager in de preview).  
* Preview-oplossingen en functies zijn niet wordt gedekt door Hallo Service Level Agreement.
* Gebruikskosten leidt ertoe dat gebruik van de preview-functies.
* Functies en mogelijkheden die u nodig hebt voor de functie Hallo / oplossing toobe nuttig mogelijk ontbreken of zijn onvolledig.
* Functies / oplossingen mogelijk niet beschikbaar in alle regio's.
* Functies / oplossingen kunnen niet worden gelokaliseerd.
* Functies / oplossingen mogelijk een limiet op Hallo aantal klanten of apparaten die kunnen worden gebruikt.
* Mogelijk moet u toouse scripts tooperform configuratie en tooenable Hallo oplossing of onderdeel.
* Hallo-gebruikersinterface (UI) is onvolledig en kan worden gewijzigd van dag tooday.
* Openbare previews mogelijk niet geschikt is voor uw productie / kritieke systemen.

#### <a name="for-private-preview"></a>Voor *persoonlijke* preview
Hallo volgende informatie is in toevoeging toohello genoemde items specifieke tooprivate previews:

* We verwachten tooprovide ons feedback over uw ervaringen zodat kunnen we Hallo functie/oplossing beter.
* We kunnen contact met u voor feedback met enquêtes, telefoongesprekken of e-mail.
* Dingen werken niet altijd goed.
* We kunnen vertrouwelijke inhoud bevatten of mogelijk niet vrijgeven overeenkomst (geheimhoudingsverklaring) voor deelname.
  * Voordat u weblog, tweeting of anders communicatie met externe partijen, neem contact op met Hallo Program Manager die verantwoordelijk is voor Hallo preview toounderstand eventuele beperkingen van de openbaarmaking.
* Niet worden uitgevoerd voor productie- / kritieke systemen.

### <a name="how-do-i-get-access-tooprivate-preview-features-and-solutions"></a>Hoe krijg ik toegang tooprivate preview-functies en oplossingen
We nodigen klanten tooprivate previews via verschillende manieren, afhankelijk van het Hallo-preview.

* Hallo maandelijkse Klantenenquête te beantwoorden en geeft ons toestemming toofollow met u verbetert de kans op uitgenodigde tooa private preview wordt.
* Uw Microsoft-accountteam hebt ontvangen, kunt u wijst.
* U kunt zich aanmelden op basis van details gepost op twitter [msopsmgmt](https://twitter.com/msopsmgmt).
* U kunt zich aanmelden op basis van gebeurtenissen voor details gedeelde community – kijken we voldoen aan ups, vergaderingen en in de online-community's.

## <a name="next-steps"></a>Volgende stappen
* [Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde informatie verzameld met oplossingen voor het beheer.
