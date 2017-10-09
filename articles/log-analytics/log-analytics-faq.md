---
title: aaaLog Veelgestelde vragen over Analytics | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over hello Azure Log Analytics-service.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a>Veelgestelde vragen over Log Analytics
Dit Microsoft-FAQ is een lijst met veelgestelde vragen over logboekanalyse in Microsoft Operations Management Suite (OMS). Als u aanvullende vragen over Log Analytics hebt, gaat u toohello [discussieforum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) en stel uw vragen. Wanneer een vraag vaak wordt gevraagd, wordt deze toegevoegd toothis artikel zodat snel en eenvoudig kunnen worden gevonden.

## <a name="general"></a>Algemeen

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a>Q. Log Analytics maakt gebruik Hallo dezelfde agent als Azure Security Center?

A. In eerdere juni 2017 begon Azure Security Center met behulp van toocollect en store-gegevens van Microsoft Monitoring Agent Hallo. toolearn meer, Zie [Azure Security Center-Platform migratie Veelgestelde vragen over](../security-center/security-center-platform-migration-faq.md).

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a>Q. Welke controles worden uitgevoerd door Hallo AD en beoordeling van de SQL-oplossingen?

A. Hallo ziet volgende query u een beschrijving van alle controles die momenteel worden uitgevoerd:

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

Hallo kunnen resultaten vervolgens worden geëxporteerde tooExcel voor verder onderzoek.

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a>V: Waarom zie ik iets anders dan *OMS* in System Center Operations Manager-console?

A: afhankelijk van welke Update Rollup van Operations Manager u zich bevindt, ziet u een knooppunt voor *System Center Advisor*, *Operational Insights*, of *logboekanalyse*.

tekst tekenreeks update te Hallo*OMS* is opgenomen in een management pack, die toobe handmatig wordt geïmporteerd moet. toosee hello huidige tekst en functionaliteit, instructies Hallo op Hallo nieuwste System Center Operations Manager Update Rollup KB-artikel en vernieuw Hallo-console.

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a>V: is er een *lokale* versie van Log Analytics?

A: Nee. Log Analytics verwerkt en grote hoeveelheden gegevens worden opgeslagen. Als een cloudservice logboekanalyse kunnen tooscale-up als nodig is en elke omgeving prestaties impact tooyour voorkomen.

Aanvullende voordelen:
- Microsoft uitvoert Hallo Log Analytics-infrastructuur, zodat u kosten
- Normale implementatie van de functie-updates en oplossingen.

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a>Q. Hoe los ik logboekanalyse is niet meer gegevens verzamelen

A: als u zich op Hallo gratis prijscategorie en meer dan 500 MB aan gegevens in een dag hebt verzonden, stopt het verzamelen van gegevens voor Hallo rest van de dag Hallo. Bereikt Hallo dagelijkse limiet is een veelvoorkomende reden die logboekanalyse stopt het verzamelen van gegevens of gegevens worden weergegeven toobe ontbreekt.

Log Analytics maakt een gebeurtenis van het type *bewerking* wanneer gegevensverzameling wordt gestart en gestopt. 

Voer Hallo query in de zoekopdracht toocheck volgen als u Hallo dagelijkse limiet is bereikt en er ontbreken gegevens:`Type=Operation OperationCategory="Data Collection Status"`

Wanneer verzamelen van gegevens stopt, hello *OperationStatus* is **waarschuwing**. Als gegevensverzameling wordt gestart, hello *OperationStatus* is **geslaagd**. 

Hallo volgende tabel beschrijft oorzaken waardoor het verzamelen van gegevens stopt en een voorgestelde actie tooresume gegevens verzamelen:

| Hiermee stopt u de gegevensverzameling reden                       | gegevensverzameling tooresume |
| -------------------------------------------------- | ----------------  |
| Dagelijkse limiet van beschikbare gegevens bereikt<sup>1</sup>       | Wacht totdat de Hallo na dag voor verzameling tooautomatically opnieuw starten, of<br> Wijziging tooa betaald prijscategorie |
| Azure-abonnement is een onderbroken vanwege: <br> Gratis proefversie is beëindigd <br> Verlopen van Azure op te geven <br> Maandelijks uitgavenlimiet bereikt (bijvoorbeeld op een abonnement met MSDN of Visual Studio)                          | Converteren van tooa betaald abonnement <br> Converteren van tooa betaald abonnement <br> Limiet verwijderen of wacht u totdat de limiet wordt opnieuw ingesteld |

<sup>1</sup> als uw werkruimte op Hallo gratis prijscategorie is, bent u beperkt toosending 500 MB aan gegevens per dag toohello service. Wanneer u Hallo dagelijkse limiet bereikt, stopt het verzamelen van gegevens tot Hallo volgende dag. Gegevens die worden verzonden tijdens het verzamelen van gegevens is gestopt, is niet geïndexeerd en is niet beschikbaar voor het zoeken. Als gegevensverzameling wordt hervat, vindt de verwerking alleen voor nieuwe gegevens die worden verzonden. 

Log Analytics gebruikt UTC-tijd en elke dag om middernacht UTC begint. Als de werkruimte Hallo Hallo dagelijkse limiet bereikt, hervat verwerking tijdens Hallo eerste uur Hallo volgende dag (UTC).

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a>Q. Hoe kan ik gewaarschuwd wanneer de gegevens verzamelen stoppen?

A: gebruik Hallo stappen in [een waarschuwingsregel maakt](log-analytics-alerts-creating.md#create-an-alert-rule) toobe een melding wanneer het verzamelen van gegevens stopt.

Bij het maken van Hallo-waarschuwing voor wanneer het verzamelen van gegevens stopt, stel de:
- **Naam** te*gegevensverzameling is gestopt*
- **Ernst** te*waarschuwing*
- **Zoekopdracht** te`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`
- **Tijdvenster** te*2 uur*.
- **Waarschuwing frequentie** toobe één uur nadat Hallo gebruiksgegevens updates slechts één keer per uur.
- **Op basis van de waarschuwing wordt gegenereerd** toobe *aantal resultaten*
- **Aantal resultaten** toobe *groter dan 0*

Gebruik Hallo stappen wordt beschreven in [acties tooalert regels toevoegen](log-analytics-alerts-actions.md) e-mail, webhook of runbook actie voor het Hallo-waarschuwingsregel configureren.


## <a name="configuration"></a>Configuratie
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a>Q. Kan ik Hallo naam wijzigen van Hallo tabel/blob-container gebruikt tooread van Azure Diagnostics (af)?

A. Nee, het is niet mogelijk tooread uit willekeurige tabellen of containers in Azure-opslag.

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a>Q. Welke IP-adressen, Hallo Log Analytics-service gebruiken? Hoe kan ik ervoor zorgen dat mijn firewall kan verkeer toohello Log Analytics-Services alleen?

A. Hallo Log Analytics-service is ingebouwd in Azure. Log Analytics IP-adressen zijn in Hallo [Microsoft Azure Datacenter IP-adresbereiken](http://www.microsoft.com/download/details.aspx?id=41653).

Als de service-implementaties worden gemaakt, wordt Hallo werkelijke IP-adressen van Hallo Log Analytics-service wijzigen. Hallo DNS-namen tooallow via de firewall zijn gedocumenteerd op [proxy- en firewall-instellingen configureren in logboekanalyse](log-analytics-proxy-firewall.md).

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a>Q. Ik ExpressRoute gebruiken voor het verbinden van tooAzure. Mijn verkeer Log Analytics maakt gebruik van mijn ExpressRoute-verbinding?

A. verschillende soorten verkeer ExpressRoute Hallo worden beschreven in Hallo [ExpressRoute-documentatie](../expressroute/expressroute-faqs.md#supported-services).

Verkeer tooLog Analytics maakt gebruik van ExpressRoute-circuit Hallo openbare peering.

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a>Q. Is er een eenvoudige en eenvoudige manier toomove een bestaande werkruimte Log Analytics-tooanother Log Analytics-werkruimte/Azure-abonnement?

A. Hallo `Move-AzureRmResource` cmdlet kunt u een werkruimte voor logboekanalyse en een Automation-account van een Azure-abonnement tooanother verplaatsen. Zie voor meer informatie [verplaatsen AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).

Deze wijziging kan ook worden gesteld in hello Azure-portal.

U kan niet verplaatsen van gegevens uit één Log Analytics-werkruimte tooanother of Hallo regio die Log Analytics-gegevens worden opgeslagen in wijzigen.

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a>V: hoe kan ik Log Analytics tooSystem Center Operations Manager toevoegen

A: bijwerken van de meest recente updatepakket toohello en importeren van management packs kunt u tooconnect Operations Manager tooLog Analytics.

>[!NOTE]
>Hallo Operations Manager verbinding tooLog Analytics is alleen beschikbaar voor System Center Operations Manager 2012 SP1 en hoger.

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a>V: hoe kan ik controleren of een agent kan toocommunicate met logboekanalyse is?

A: tooensure die Hallo-agent kan communiceren met OMS, gaat u naar: het Configuratiescherm, beveiliging en -instellingen, **Microsoft Monitoring Agent**.

Onder Hallo **Azure logboekanalyse (OMS)** tabblad, Controleer of er een groen vinkje. Een groen vinkje wordt bevestigd die agent Hallo kunnen toocommunicate Hello OMS-service.

Een geel waarschuwingspictogram betekent Hallo-agent heeft problemen communicatie met OMS. Een veelvoorkomende reden hiervoor is Hallo Microsoft Monitoring Agent-service is gestopt. Gebruik service control manager toorestart Hallo-service.

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a>V: hoe voorkom ik een agent niet communiceren met Log Analytics

A: In System Center Operations Manager, kunt u Hallo computer in Hallo Advisor beheerde computerlijst verwijderen. Operations Manager-updates Hallo configuratie van Hallo agent toono langer rapport tooLog Analytics. Voor agents tooLog Analytics die rechtstreeks zijn aangesloten, kunt u ze stopt vanaf communiceren via: het Configuratiescherm, beveiliging en -instellingen, **Microsoft Monitoring Agent**.
Onder **Azure logboekanalyse (OMS)**, verwijdert u alle werkruimten die worden vermeld.

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a>V: Waarom krijg ik een fout wanneer ik mijn werkruimte van één Azure-abonnement tooanother toomove proberen?

A: als u hello Azure-portal gebruikt, zorg er alleen Hallo werkruimte is geselecteerd voor Hallo verplaatsen. Selecteer niet Hallo oplossingen--ze automatisch verplaatst nadat het Hallo-werkruimte wordt verplaatst. 

Zorg ervoor dat u gemachtigd in beide Azure-abonnementen.

## <a name="agent-data"></a>Gegevens van agent
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a>Q. Hoeveel gegevens kan ik verzenden via Hallo agent tooLog Analytics? Is er een maximale hoeveelheid gegevens per klant?
A. Hallo gratis-plan Hiermee stelt u een dagelijkse limiet van 500 MB per werkruimte. Hallo standard en premium-plannen hebt geen limiet op Hallo hoeveelheid gegevens die is geüpload. Als een cloudservice Log Analytics is ontworpen tooautomatically scale toohandle Hallo volume afkomstig is van een klant – zelfs als deze TB per dag.

Hallo Log Analytics-agent is ontworpen tooensure heeft een kleine footprint. Een van onze klanten een blog over Hallo-tests ze die worden uitgevoerd op basis van de agent en hoe onder de indruk dat ze zijn geschreven. Hallo gegevensvolume varieert op basis van het Hallo-oplossingen die u inschakelt. U kunt gedetailleerde informatie op Hallo gegevensvolume en Hallo verdeling zien door oplossing in Hallo [gebruik](log-analytics-usage.md) pagina.

Voor meer informatie vindt u een [klant blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) over lage footprint Hallo van Hallo OMS-agent.

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a>Q. Hoeveel bandbreedte van het netwerk wordt gebruikt door Hallo Microsoft Management Agent (MMA) bij het verzenden van gegevens tooLog Analytics?

A. Bandbreedte is een functie van Hallo hoeveelheid gegevens die worden verzonden. Gegevens worden gecomprimeerd wanneer deze via Hallo-netwerk worden verzonden.

### <a name="q-how-much-data-is-sent-per-agent"></a>Q. Hoeveel gegevens per agent worden verzonden?

A. afhankelijk van Hallo en de hoeveelheid gegevens die zijn verzonden per agent:

* Hallo-oplossingen die u hebt ingeschakeld
* Hallo aantal logboeken en prestatiemeteritems worden verzameld
* Hallo volume aan gegevens in Logboeken Hallo

Hallo gratis prijscategorie is een uitstekende manier tooonboard verschillende servers en meet het Hallo typische gegevensvolume. Algemene informatie over het gebruik wordt weergegeven op Hallo [gebruik](log-analytics-usage.md) pagina.

Voor computers die zich kunnen toorun hello WireData-agent, gebruikt u Hallo na query toosee hoeveel gegevens worden verzonden:

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a>Volgende stappen
* [Aan de slag met logboekanalyse](log-analytics-get-started.md) toolearn meer over Log Analytics en get up-to-date en worden uitgevoerd in minuten.
