---
title: aaaOverview Hallo Azure Activity Log | Microsoft Docs
description: Informatie over welke hello Azure Activity Log is en hoe u kunt deze toounderstand gebeurtenissen binnen uw Azure-abonnement.
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: johnkem
ms.openlocfilehash: cba79b7f6dc0833ef588382e763761fd77d43307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-subscription-activity-with-hello-azure-activity-log"></a>Abonnement activiteitsbewaking Hello Azure Activity Log
Hallo **Azure Activity Log** is een abonnementlogboek die biedt inzicht in het abonnement op gebeurtenissen die hebben plaatsgevonden in Azure. Dit omvat een bereik van gegevens van Azure Resource Manager operationele gegevens tooupdates op Service Health-gebeurtenissen. Hallo activiteitenlogboek heette vroeger 'Controlelogboeken' of 'Operationele Logs' sinds Hallo beheercategorie rapporten besturingselement vlak gebeurtenissen voor uw abonnementen. Hallo activiteitenlogboek gebruikt, u kunt bepalen Hallo ' wat, wie, en wanneer ' voor een (PUT, POST, verwijderen schrijfbewerkingen) die zijn gemaakt op Hallo van resources in uw abonnement. U kunt ook Hallo status Hallo-werking en andere relevante eigenschappen begrijpen. Hallo activiteitenlogboek bevat geen leesbewerkingen (GET) en bewerkingen voor resources die gebruikmaken van Hallo klassieke / 'RDFE' model.

![Activiteit logboeken tegenover andere typen logboeken ](./media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

Afbeelding 1: Activiteitenlogboeken tegenover andere typen logboeken

Hallo activiteitenlogboek verschilt van [diagnostische logboeken](monitoring-overview-of-diagnostic-logs.md). Activiteitenlogboeken bevatten gegevens over Hallo-bewerkingen op een resource van Hallo buiten (Hallo 'besturingselement vlak'). Logboeken met diagnostische gegevens worden gegenereerd door een resource en bevatten informatie over het Hallo-bewerking van de bron ('gegevens vlak' hello).

Kunt u gebeurtenissen ophalen uit uw activiteitenlogboek met hello Azure-portal CLI, PowerShell-cmdlets en REST-API van Azure-Monitor.


> [!WARNING]
> Hello Azure Activity Log is voornamelijk bedoeld voor activiteiten die in Azure Resource Manager optreden. Resources met behulp van Hallo-Classic/RDFE-model worden niet bijgehouden. Sommige klassieke resource-typen hebben een proxy-resourceprovider in Azure Resource Manager (bijvoorbeeld Microsoft.ClassicCompute). Als u met een resourcetype klassieke via Azure Resource Manager met behulp van deze proxy-resourceproviders werken, wordt Hallo operations in Hallo activiteitenlogboek weergegeven. Als u met communiceren een klassiek brontype in Hallo-Classic-portal of anders buiten hello Azure Resource Manager-proxy's, uw acties worden alleen vastgelegd in Hallo bewerkingslogboek. Hallo bewerkingslogboek is alleen beschikbaar in Hallo-Classic-portal.
>
>

Weergave hello video introducing Hallo activiteitenlogboek te volgen.
> [!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]
> 
>

## <a name="categories-in-hello-activity-log"></a>Categorieën in Hallo Activity Log
Hallo activiteitenlogboek bevat verschillende categorieën van gegevens. Voor volledige informatie over Hallo schema's uit deze categorieën [Raadpleeg dit artikel](monitoring-activity-log-schema.md). Deze omvatten:
* **Beheerdersrechten** -deze categorie bevat Hallo-record van alle maken, update, delete en actie bewerkingen uitgevoerd via Resource Manager. Voorbeelden van Hallo soorten gebeurtenissen u in deze categorie ziet zijn 'virtuele machine maken' en 'verwijderen netwerkbeveiligingsgroep' elke actie op die door een gebruiker of toepassing die met Resource Manager is gemodelleerd als een bewerking op een bepaald resourcetype. Als Hallo bewerkingstype schrijven, verwijderen of actie Hallo-records van zowel Hallo start en het slagen of mislukken van die bewerking worden vastgelegd in Hallo beheercategorie. Hallo beheercategorie bevat ook eventuele wijzigingen toorole toegangsbeheer op basis van een abonnement.
* **Servicestatus** -deze categorie bevat Hallo record service health incidenten die hebben plaatsgevonden in Azure. Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "SQL Azure in VS-Oost ondervindt uitvaltijd." Gebeurtenissen van de health service in vijf soorten komen: actie vereist, ondersteunde herstel, Incident, onderhoud, gegevens of beveiliging, en worden alleen weergegeven als u hebt een resource in het Hallo-abonnement dat zou worden beïnvloed door het Hallo-gebeurtenis.
* **Waarschuwing** -deze categorie bevat Hallo-record van alle activeringen van waarschuwingen van Azure. Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "CPU-percentage op myVM is meer dan 80 voor Hallo afgelopen vijf minuten." Een verscheidenheid aan Azure systemen hebben een waarschuwingsmethoden concept--u kunt een regel bepaalde hardwaresleutel definiëren en een melding ontvangen wanneer voorwaarden overeenkomen met die regel. Elke keer dat een ondersteunde Azure Waarschuwingstype 'wordt geactiveerd,' of hello voorwaarden wordt voldaan toogenerate een melding, toothis categorie Hallo activiteitenlogboek wordt ook doorgeschoven, is een record van Hallo activering.
* **Automatisch schalen** -deze categorie bevat Hallo-record van een bewerking van de gerelateerde toohello gebeurtenissen van Hallo automatisch schalen-engine op basis van de instellingen voor automatisch schalen die u hebt gedefinieerd in uw abonnement. Een voorbeeld van Hallo type gebeurtenis u in deze categorie ziet is "Automatisch schalen opschaling van de actie is mislukt." Met automatisch schalen, kunt u automatisch geschaald uitbreiden of schalen in Hallo aantal exemplaren in een ondersteunde brontype op basis van tijd van de dag en/of laden (metrische) gegevens met behulp van een instelling voor automatisch schalen. Wanneer Hallo voorwaarden wordt voldaan worden tooscale omhoog of omlaag, Hallo-begin- en geslaagd of mislukt gebeurtenissen vastgelegd in deze categorie.
* **Aanbeveling** -deze categorie bevat gebeurtenissen die aanbeveling van bepaalde brontypen, zoals websites en SQL-servers. Deze gebeurtenissen bieden aanbevelingen voor hoe toobetter gebruiken voor uw resources. U ontvangt alleen gebeurtenissen van dit type als u hebt resources die aanbevelingen verzenden.
* **Beleid, beveiliging en resourcestatus** -deze categorieën bevatten niet alle gebeurtenissen; ze zijn gereserveerd voor toekomstig gebruik.

## <a name="event-schema-per-category"></a>Schema van de gebeurtenis per categorie
[Raadpleeg dit artikel toounderstand Hallo activiteitenlogboek gebeurtenis schema per categorie.](monitoring-activity-log-schema.md)

## <a name="what-you-can-do-with-hello-activity-log"></a>Wat u kunt doen met Hallo Activity Log
Hier volgen enkele Hallo dingen die u met Hallo activiteitenlogboek doen kunt:

![Azure Activity log](./media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* Opvragen en weergeven in Hallo **Azure-portal**.
* [Maak een waarschuwing op een activiteit van het gebeurtenislogboek.](monitoring-activity-log-alerts.md)
* [Deze tooan stream **Event Hub** ](monitoring-stream-activity-logs-event-hubs.md) voor opname door een service van derden of aangepaste analytics-oplossing zoals Power BI.
* Analyseren in Power BI met Hallo [ **Power BI-inhoudspakket**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).
* [Sla het tooa **Opslagaccount** voor archivering of handmatig inspectie](monitoring-archive-activity-log.md). U kunt opgeven dat Hallo bewaartijd (in dagen) met behulp van Hallo **logboek profiel**.
* Deze query's uitvoeren via PowerShell-Cmdlet, CLI of REST-API.

## <a name="query-hello-activity-log-in-hello-azure-portal"></a>Query Hallo activiteitenlogboek in hello Azure-portal
U kunt uw activiteitenlogboek bekijken op verschillende plaatsen binnen hello Azure-portal:
* Hallo **activiteitenlogboek blade**, die u kunt openen door te zoeken naar Hallo activiteitenlogboek onder 'Meer Services' in hello links navigatiedeelvenster.
* Hallo **Monitor blade**, die standaard in Hallo links navigatiedeelvenster wordt weergegeven. Hallo activiteitenlogboek is een gedeelte van deze blade Azure Monitor.
* Een resource **resourceblade**, bijvoorbeeld Hallo configuratie blade voor een virtuele Machine. Hallo activiteitenlogboek is een van de secties Hallo op de meeste van deze resourceblades worden en automatisch te klikken op het Hallo-gebeurtenissen gefilterd toothose gerelateerde toothat bepaalde resource.

In hello Azure-portal, kunt u uw activiteitenlogboek door deze velden te filteren:
* TimeSpan - Hallo begin- en -tijd voor gebeurtenissen.
* Categorie - Hallo gebeurteniscategorie zoals hierboven is beschreven.
* Abonnement - een of meer namen van de Azure-abonnement.
* Resourcegroep - een of meer resourcegroepen binnen deze abonnementen.
* Bron (naam) - Hallo-naam van een specifieke bron.
* Brontype - Hallo type resource, bijvoorbeeld Microsoft.Compute/virtualmachines.
* Naam van de bewerking - Hallo-naam van een Azure Resource Manager-bewerking, bijvoorbeeld Microsoft.SQL/servers/Write.
* Ernst: Hallo ernst van gebeurtenis hello (ter informatie, waarschuwing, fout, kritiek).
* De gebeurtenis wordt gestart door - Hallo 'beller' of de gebruiker die Hallo bewerking uitgevoerd.
* Open search - dit is een open zoeken in het tekstvak waarin wordt gezocht naar de tekenreeks die tussen alle velden in alle gebeurtenissen.

Wanneer u een verzameling filters hebt gedefinieerd, kunt u deze opslaan als een query die over de sessies worden bewaard als je ooit tooperform moet dezelfde query met deze filters opnieuw toegepast in toekomstige Hallo Hallo. U kunt ook een query tooyour Azure-dashboard tooalways behouden gaten vastmaken van specifieke gebeurtenissen.

Te klikken op 'Toepassing' uw query wordt uitgevoerd en alle overeenkomende gebeurtenissen tonen. Te klikken op een gebeurtenis in Hallo lijst geeft samenvatting van die gebeurtenis Hallo evenals Hallo volledige onbewerkte JSON van die gebeurtenis.

Voor nog meer stroom, klikt u op Hallo **logboek zoeken** pictogram dat uw gegevens activiteitenlogboek in hello wordt [Log Analytics activiteit Log Analytics-oplossing](../log-analytics/log-analytics-activity.md). Hallo activiteitenlogboek blade biedt een eenvoudige filter/bladeren op de logboeken, maar Log Analytics kunt u toopivot opvragen en visualiseren van uw gegevens op krachtige manieren.

## <a name="export-hello-activity-log-with-a-log-profile"></a>Hallo activiteitenlogboek met een logboek profiel exporteren
Een **logboek profiel** bepaalt hoe uw activiteitenlogboek wordt geëxporteerd. Een logboek-profiel gebruikt, kunt u configureren:

* Waar Hallo activiteitenlogboek moet worden verzonden (Storage-Account of Event Hubs)
* Welke gebeurteniscategorieën (schrijven, verwijderen, actie) moeten worden verzonden. *Hallo betekenis van 'categorie' in het logboek profielen en logboekgebeurtenissen activiteit verschilt. In het logboek profiel hello vertegenwoordigt 'Categorie' Hallo bewerkingstype (schrijven, verwijderen, actie). In een gebeurtenis activiteitenlogboek vertegenwoordigt de eigenschap 'categorie' Hallo Hallo bron- of type gebeurtenis (bijvoorbeeld, beheer, ServiceHealth, waarschuwing en meer).*
* Welke regio's (locaties) moeten worden geëxporteerd. Zorg ervoor dat tooinclude 'global', zoals veel gebeurtenissen in Hallo activiteitenlogboek algemene gebeurtenissen zijn.
* Hoe lang Hallo activiteitenlogboek worden bewaard in een Opslagaccount.
    - Een bewaartermijn van nul dagen betekent logboeken permanent worden bewaard. Hallo-waarden zijn anders wordt een willekeurig aantal dagen tussen 1 en 2147483647.
    - Als bewaarbeleid worden ingesteld, maar Logboeken opslaan in een Opslagaccount is uitgeschakeld (bijvoorbeeld, als er alleen Event Hubs of OMS-opties zijn geselecteerd), is het bewaarbeleid Hallo hebben geen effect.
    - Bewaarbeleid toegepaste per dag, zodat Hallo einde van een dag (UTC) wordt vastgelegd vanaf Hallo dag dat is nu voorbij Hallo bewaarbeleid worden verwijderd. Bijvoorbeeld, als u had een bewaarbeleid van één dag, zou aan Hallo begin van vandaag de dag voor de Hallo Hallo logboeken van Hallo dag voordat gisteren worden verwijderd.

U kunt een opslagaccount of event hub-naamruimte die zich niet in hetzelfde abonnement Hallo zoals Hallo een tekensetcodering Logboeken. Hallo-gebruiker die Hallo instelling configureert, moet Hallo juiste RBAC toegang tooboth abonnementen hebben.

Deze instellingen kunnen worden geconfigureerd via Hallo optie 'Exporteren' hello activiteitenlogboek blade in Hallo-portal. Ze kunnen ook programmatisch te worden geconfigureerd [Monitor REST-API van Azure met behulp van Hallo](https://msdn.microsoft.com/library/azure/dn931927.aspx), PowerShell-cmdlets of CLI. Een abonnement kan slechts één logboek profiel hebben.

### <a name="configure-log-profiles-using-hello-azure-portal"></a>Logboek-profielen met de Hallo Azure-portal configureren
U kunt Hallo activiteitenlogboek tooan Event Hub stream of op te slaan in een Opslagaccount met behulp van de optie 'Exporteren' hello in hello Azure-portal.

1. Navigeer toohello **activiteitenlogboek** blade met Hallo-menu op Hallo linkerkant van Hallo-portal.

    ![Navigeer tooActivity logboek in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Klik op Hallo **exporteren** knop Hallo boven aan het Hallo-blade.

    ![Knop exporteren in de portal](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Hallo-blade die wordt weergegeven, kunt u het volgende selecteren:  
  * regio's waarvoor u tooexport gebeurtenissen wilt
  * Hallo Opslagaccount toowhich gewenst toosave gebeurtenissen
  * Hallo aantal dagen dat u tooretain deze gebeurtenissen in de opslag wilt. Een instelling van 0 dagen behoudt Hallo logboeken permanent verloren.
  * Hallo Service Bus-Namespace waarin u een Event Hub toobe gemaakt wilt voor het streamen van deze gebeurtenissen.

     ![Activiteitenlogboek blade exporteren](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Klik op **opslaan** toosave deze instellingen. Hallo-instellingen zijn onmiddellijk toegepaste tooyour abonnement zijn.

### <a name="configure-log-profiles-using-hello-azure-powershell-cmdlets"></a>Configureren van logboek-profielen met de Hallo Azure PowerShell-Cmdlets
#### <a name="get-existing-log-profile"></a>Bestaande profiel voor het logboek ophalen
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a>Een profiel van het logboek toevoegen
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| Naam |Ja |Naam van uw logboek-profiel. |
| StorageAccountId |Nee |Bron-ID van Hallo Opslagaccount toowhich Hallo activiteitenlogboek moet worden opgeslagen. |
| serviceBusRuleId |Nee |Service Bus-regel-ID voor Service Bus-naamruimte Hallo dat toohave event hubs in hebt gemaakt. Is een tekenreeks met deze indeling: `{service bus resource ID}/authorizationrules/{key name}`. |
| Locaties |Ja |Door komma's gescheiden lijst met regio's waarvoor u toocollect activiteitenlogboek gebeurtenissen wilt. |
| RetentionInDays |Ja |Aantal dagen voor welke gebeurtenissen worden bewaard, tussen 1 en 2147483647. Een waarde van nul Hallo logboeken voor onbepaalde tijd opgeslagen (permanent). |
| Categorieën |Nee |Door komma's gescheiden lijst met categorieën van gebeurtenissen die moeten worden verzameld. Mogelijke waarden zijn schrijven, verwijderen en in te grijpen. |

#### <a name="remove-a-log-profile"></a>Een logboek-profiel verwijderen
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-hello-azure-cross-platform-cli"></a>Logboek profielen configureren met Hallo platformoverschrijdende CLI van Azure
#### <a name="get-existing-log-profile"></a>Bestaande profiel voor het logboek ophalen
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
Hallo `name` eigenschap moet Hallo-naam van uw logboek-profiel.

#### <a name="add-a-log-profile"></a>Een profiel van het logboek toevoegen
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| Eigenschap | Vereist | Beschrijving |
| --- | --- | --- |
| naam |Ja |Naam van uw logboek-profiel. |
| storageId |Nee |Bron-ID van Hallo Opslagaccount toowhich Hallo activiteitenlogboek moet worden opgeslagen. |
| serviceBusRuleId |Nee |Service Bus-regel-ID voor Service Bus-naamruimte Hallo dat toohave event hubs in hebt gemaakt. Is een tekenreeks met deze indeling: `{service bus resource ID}/authorizationrules/{key name}`. |
| Locaties |Ja |Door komma's gescheiden lijst met regio's waarvoor u toocollect activiteitenlogboek gebeurtenissen wilt. |
| RetentionInDays |Ja |Aantal dagen voor welke gebeurtenissen worden bewaard, tussen 1 en 2147483647. Een waarde van nul Hallo logboeken voor onbepaalde tijd opgeslagen (permanent). |
| Categorieën |Nee |Door komma's gescheiden lijst met categorieën van gebeurtenissen die moeten worden verzameld. Mogelijke waarden zijn schrijven, verwijderen en in te grijpen. |

#### <a name="remove-a-log-profile"></a>Een logboek-profiel verwijderen
```
azure insights logprofile delete --name my_log_profile
```

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Hallo activiteitenlogboek (voorheen controlelogboeken)](../azure-resource-manager/resource-group-audit.md)
* [Stream hello Azure Activity Log tooEvent Hubs](monitoring-stream-activity-logs-event-hubs.md)
