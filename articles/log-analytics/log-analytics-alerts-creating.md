---
title: aaaCreating waarschuwingen in OMS Log Analytics | Microsoft Docs
description: Waarschuwingen in logboekanalyse belangrijke informatie in de OMS-opslagplaats te identificeren en op de proactief kunnen zullen u informeren over problemen of acties tooattempt toocorrect aanroepen ze.  Dit artikel wordt beschreven hoe een waarschuwingsregel toocreate en details Hallo verschillende acties kunnen nemen.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a>Werken met regels voor waarschuwingen in Log Analytics
Waarschuwingen worden gemaakt door regels voor waarschuwingen die automatisch logboek zoekopdrachten met regelmatige tussenpozen worden uitgevoerd.  Ze maken een waarschuwing record als Hallo resultaten aan bepaalde criteria voldoen.  Hallo regel kan automatisch voert vervolgens een of meer acties tooproactively zullen u informeren over Hallo waarschuwing of aanroepen van een ander proces.   

In dit artikel beschrijft Hallo processen toocreate en waarschuwingsregels Hallo OMS-portal met bewerken.  Zie voor meer informatie over verschillende Hallo-instellingen en over hoe tooimplement logica [inzicht-waarschuwingen in logboekanalyse](log-analytics-alerts.md).

>[!NOTE]
> U kunt momenteel maken of wijzigen van een waarschuwingsregel hello Azure-portal met. 

## <a name="create-an-alert-rule"></a>Een waarschuwingsregel maken

Hallo-records die moeten worden aangeroepen Hallo waarschuwing zoeken toocreate een waarschuwingsregel met Hallo OMS-portal, die u start een logboek te maken.  Hallo **waarschuwing** knop kan vervolgens worden zodat u kunt maken en configureren van de waarschuwingsregel Hallo.

>[!NOTE]
> Maximaal 250 waarschuwingsregels kan momenteel worden gemaakt in een OMS-werkruimte. 

1. Klik op de pagina overzicht van OMS Hallo **logboek zoeken**.
2. Maak een nieuw logboekbestand zoekquery of Selecteer een zoekbewerking opgeslagen logboek. 
3. Klik op **waarschuwing** bovenaan Hallo Hallo pagina tooopen hello **waarschuwingsregel toevoegen** scherm.
4. Configureren van de waarschuwingsregel Hallo met informatie in [Details van waarschuwingsregels](#details-of-alert-rules) hieronder.
6. Klik op **opslaan** toocomplete Hallo waarschuwingsregel.  Begint onmiddellijk uitgevoerd.


## <a name="edit-an-alert-rule"></a>Een waarschuwingsregel bewerken
U kunt een lijst met alle waarschuwingsregels krijgen in Hallo **waarschuwingen** menu van logboekanalyse **instellingen**.  

![Waarschuwingen beheren](./media/log-analytics-alerts/configure.png)

1. In Hallo OMS-console selecteert Hallo **instellingen** tegel.
2. Selecteer **waarschuwingen**.

U kunt meerdere acties uitvoeren vanuit deze weergave.

* Een regel uitschakelen door het selecteren van **uit** volgende tooit.
* Een waarschuwingsregel bewerken door te klikken op Hallo pen pictogram volgende tooit.
* Verwijderen van een waarschuwingsregel door te klikken op Hallo **X** volgende tooit pictogram. 

## <a name="details-of-alert-rules"></a>Details van regels voor waarschuwingen
Wanneer u maakt of een waarschuwingsregel in Hallo OMS-portal bewerkt, werkt u met de Hallo **waarschuwingsregel toevoegen** of **waarschuwingsregel bewerken** pagina.  Hallo volgende tabellen beschrijven Hallo velden in dit scherm.

![Waarschuwingsregel](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a>Informatie over waarschuwingen
Dit zijn de basisinstellingen voor Hallo waarschuwingsregel en Hallo waarschuwingen die wordt gemaakt.

| Eigenschap | Beschrijving |
|:--- |:---|
| Naam | De unieke naam tooidentify Hallo waarschuwingsregel. Deze naam is opgenomen in alle waarschuwingen die zijn gemaakt door Hallo regel.  |
| Beschrijving | Optionele beschrijving van de waarschuwingsregel Hallo. |
| Ernst |Ernst van eventuele waarschuwingen die door deze regel wordt gemaakt. |

### <a name="search-query-and-time-window"></a>De query en het tijdstip zoekvenster
Hallo query en het tijdstip zoekvenster retourneren die Hallo-records die geëvalueerd toodetermine zijn als er waarschuwingen moeten worden gemaakt.

| Eigenschap | Beschrijving |
|:--- |:---|
| Zoekopdracht | Dit is Hallo-query die wordt uitgevoerd.  Hallo-records geretourneerd door deze query worden gebruikte toodetermine of een waarschuwing wordt gemaakt.<br><br>Selecteer **huidige zoekquery gebruiken** toouse Hallo huidige query of Selecteer een bestaande opgeslagen zoekopdracht uit Hallo-lijst.  Hallo-querysyntaxis wordt vermeld in het tekstvak Hallo waar u kunt deze desgewenst wijzigen. |
| Tijdvenster |Hiermee geeft u een tijdsbereik Hallo voor Hallo-query.  Hallo query retourneert alleen de records die zijn gemaakt binnen dit bereik Hallo huidige tijd.  Dit kan een waarde tussen 5 minuten en 24 uur zijn.  Deze moet groter dan of gelijk toohello frequentie van waarschuwingen.  <br><br> Bijvoorbeeld, als hello tijd ingesteld too60 minuten en Hallo query wordt uitgevoerd om 1:15 uur, wordt alleen de records die zijn gemaakt tussen 12:15 uur en 1:15 uur geretourneerd. |

Wanneer u Hallo tijdvenster voor Hallo waarschuwingsregel opgeeft, wordt het aantal bestaande records die overeenkomen met de zoekcriteria Hallo voor dat tijdvenster Hallo weergegeven.  Hiermee kunt u bepalen Hallo frequentie waarmee u Hallo aantal resultaten die u verwacht.

### <a name="schedule"></a>Planning
Hiermee definieert u hoe vaak hello zoekopdracht wordt uitgevoerd.

| Eigenschap | Beschrijving |
|:--- |:---|
| Frequentie van waarschuwingen | Hiermee geeft u op hoe vaak hello query moet worden uitgevoerd. Is een waarde tussen 5 minuten en 24 uur. Moet gelijk tooor kleiner is dan Hallo tijdvenster.  Als het Hallo-waarde groter is dan het tijdvenster hello, risico u records wordt overgeslagen.<br><br>Neem bijvoorbeeld een tijdvenster van 30 minuten en een frequentie van 60 minuten.  Als het Hallo-query wordt uitgevoerd om 1:00 uur, wordt er records tussen 12:30 en 13:00 uur.  Hallo is Hallo query wordt uitgevoerd zodra 2:00 wanneer er records tussen 1:30 en 2:00 zou geretourneerd.  Alle records gemaakt tussen de 1:00 en 1:30 zou nooit worden geëvalueerd. |


### <a name="generate-alert-based-on"></a>Op basis van de waarschuwing wordt gegenereerd
Hiermee definieert u Hallo criteria die wordt geëvalueerd tegen Hallo resultaten van Hallo zoeken query toodetermine als er een waarschuwing moeten worden gemaakt.  Deze gegevens zullen afwijken, afhankelijk van Hallo type waarschuwingsregel die u selecteert.  U kunt details ophalen voor Hallo waarschuwingsregel verschillende typen uit [inzicht-waarschuwingen in logboekanalyse](log-analytics-alerts.md).

| Eigenschap | Beschrijving |
|:--- |:---|
| Waarschuwingen onderdrukken | Wanneer u de onderdrukking voor de waarschuwingsregel Hallo inschakelt, worden de acties voor Hallo regel uitgeschakeld gedurende een gedefinieerde periode na het maken van een nieuwe waarschuwing. Hallo regel nog steeds actief is en waarschuwing records maakt als Hallo criteria wordt voldaan. Dit is tooallow u toocorrect Hallo probleem tijd zonder dubbele acties worden uitgevoerd. |

#### <a name="number-of-results-alert-rules"></a>Aantal resultaten waarschuwingsregels

| Eigenschap | Beschrijving |
|:--- |:---|
| Aantal resultaten |Een waarschuwing wordt gemaakt als het aantal records dat wordt geretourneerd door de query Hallo Hallo **groter is dan** of **minder dan** Hallo waarde die u opgeeft.  |

#### <a name="metric-measurement-alert-rules"></a>Waarschuwingsregels metrische meting

| Eigenschap | Beschrijving |
|:--- |:---|
| Cumulatieve waarde | Drempelwaarde voor dat elke cumulatieve waarde in de resultaten van de Hallo toobe moet overschrijden beschouwd als een schending. |
| Op basis van de trigger-waarschuwing | Hallo aantal schendingen voor een waarschuwing toobe gemaakt.  U kunt opgeven **totaal aantal schendingen** voor elke combinatie van inbreuk op Hallo resultaten ingesteld of **opeenvolgende schendingen** toorequire die schendingen Hallo moet plaatsvinden in opeenvolgende steekproeven. |

### <a name="actions"></a>Acties
Waarschuwingsregels maakt altijd een [waarschuwing record](#alert-records) wanneer Hallo drempelwaarde wordt voldaan.  Ook kunt u een of meer antwoorden toobe uitvoeren zoals het verzenden van een e-mailbericht of een runbook starten.



#### <a name="email-actions"></a>E-acties
E-acties Stuur een e-mail met Hallo details van de waarschuwing tooone Hallo of meer geadresseerden.

| Eigenschap | Beschrijving |
|:--- |:---|
| E-mailmelding |Geef **Ja** als u wilt dat een e-toobe verzonden wanneer Hallo waarschuwing wordt geactiveerd. |
| Onderwerp |Onderwerpen in Hallo e-mailbericht.  U kunt Hallo hoofdtekst van e-mail Hallo niet wijzigen. |
| ontvangers |De adressen van alle e-mailgeadresseerden.  Als u meer dan één adres vervolgens afzonderlijke hello-mailadressen opgeven met een puntkomma (;). |

#### <a name="webhook-actions"></a>Webhookacties
Webhookacties kunnen u tooinvoke een extern proces via één HTTP POST-aanvraag.

| Eigenschap | Beschrijving |
|:--- |:---|
| Webhook |Geef **Ja** als u wilt dat een webhook toocall wanneer Hallo waarschuwing wordt geactiveerd. |
| Webhook-URL |Hallo-URL van de webhook Hallo. |
| Aangepaste JSON-nettolading opnemen |Selecteer deze optie als u wilt dat tooreplace Hallo standaard nettolading met een aangepaste nettolading. |
| Voer de aangepaste JSON-nettolading |Hallo aangepaste nettolading voor Hallo webhook.  Zie de vorige sectie voor meer informatie. |

#### <a name="runbook-actions"></a>Runbook-acties
Runbook-acties starten van een runbook in Azure Automation. 

>[!NOTE]
> Hallo Automation-oplossing is geïnstalleerd in de werkruimte voor deze actie toobe ingeschakeld, moet u hebben. 


| Eigenschap | Beschrijving |
|:--- |:---|
| Runbook | Geef **Ja** als u een Azure Automation-runbook toostart wilt wanneer Hallo waarschuwing wordt geactiveerd.  |
| Automation-account | Hiermee geeft u Hallo Automation-account dat runbooks zijn geselecteerd uit.  Dit is Hallo actie-account dat is gekoppeld toohello werkruimte. |
| Selecteer een runbook | Selecteer Hallo runbook dat het gewenste toostart wanneer een waarschuwing wordt gemaakt. |
| Voer op | Selecteer **Azure** toorun hello runbook in de cloud Hallo.  Selecteer **hybride worker** toorun hello runbook op een agent met [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) geïnstalleerd.  |




## <a name="next-steps"></a>Volgende stappen
* Hallo installeren [waarschuwing beheeroplossing](log-analytics-solution-alert-management.md) tooanalyze waarschuwingen die zijn gemaakt in logboekanalyse samen met waarschuwingen van System Center Operations Manager (SCOM) verzameld.
* Lees meer over [Meld zoekopdrachten](log-analytics-log-searches.md) kunnen die waarschuwingen genereren.
* Een stapsgewijze Kennismaking voltooien [configureren van een webook](log-analytics-alerts-webhooks.md) met een waarschuwingsregel.  
* Meer informatie over hoe toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problemen geïdentificeerd met waarschuwingen.

