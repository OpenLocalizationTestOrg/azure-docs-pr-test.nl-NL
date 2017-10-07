---
title: aaaConfigure webhooks op waarschuwingen van Azure metrische | Microsoft Docs
description: Waarschuwingen van Azure tooother niet-Azure-systemen worden omgeleid.
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Configureren van een webhook op een Azure metrische waarschuwing
Webhooks kunt u een Azure tooroute melding tooother systemen voor na verwerking of aangepaste acties een waarschuwing. U kunt een webhook gebruiken op een waarschuwing tooroute het tooservices die verzenden SMS, meld bugs, melding van een team via chat/berichtenservices of komen een aantal andere acties. Dit artikel wordt beschreven hoe tooset een webhook op een Azure metrische waarschuwing en welke Hallo nettolading voor Hallo HTTP POST tooa webhook eruit ziet. Voor informatie over het Hallo-installatie en het schema voor een waarschuwing Azure Activity Log (waarschuwing van gebeurtenissen) [deze pagina vindt u in plaats daarvan](insights-auditlog-to-webhook-email.md).

Schema gedefinieerd hieronder tooa webhook URI die u opgeeft bij het maken van de waarschuwing hello Azure waarschuwingen HTTP POST Hallo inhoud van waarschuwing in JSON-indeling. Deze URI moet een geldige HTTP of HTTPS-eindpunt. Azure boekt één vermelding per aanvraag wanneer een waarschuwing is geactiveerd.

## <a name="configuring-webhooks-via-hello-portal"></a>Configureren van webhooks via Hallo-portal.
U kunt toevoegen of bijwerken Hallo webhook URI in Create/Update waarschuwingen welkomstscherm in Hallo [portal](https://portal.azure.com/).

![Een waarschuwingsregel toevoegen](./media/insights-webhooks-alerts/Alertwebhook.png)

U kunt ook een waarschuwing toopost tooa webhook URI configureren met behulp van Hallo [Azure PowerShell-Cmdlets](insights-powershell-samples.md#create-metric-alerts), [platformoverschrijdende CLI](insights-cli-samples.md#work-with-alerts), of [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Hallo webhook verifiëren
Hallo webhook kunt verifiëren met behulp van verificatie op basis van tokens. Hallo webhook URI wordt opgeslagen met een token ID, bijv. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>De nettolading van schema
Hallo POST-bewerking bevat Hallo volgende JSON-nettolading en het schema voor alle metriek op basis van waarschuwingen.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Veld | Verplicht | Vaste Set van waarden | Opmerkingen |
|:--- |:--- |:--- |:--- |
| status |J |'Geactiveerd', 'Opgelost' |Status voor Hallo waarschuwing gebaseerd op voorwaarden Hallo u hebt ingesteld. |
| Context |J | |Hallo waarschuwingscontext. |
| tijdstempel |J | |Hallo tijd op welke Hallo waarschuwing is geactiveerd. |
| id |J | |Elke waarschuwingsregel heeft een unieke id. |
| naam |J | |Hallo naam van waarschuwing. |
| description |J | |Beschrijving van waarschuwing Hallo. |
| conditionType |J |'Metrische', 'Gebeurtenis' |Twee typen waarschuwingen worden ondersteund. Een op basis van een voorwaarde metrische en andere op basis van een gebeurtenis in Hallo activiteitenlogboek Hallo. Gebruik deze waarde toocheck als Hallo waarschuwing is gebaseerd op metriek of gebeurtenis. |
| Voorwaarde |J | |Hallo specifieke velden toocheck voor gebaseerd op Hallo conditionType. |
| metricName |voor metrische waarschuwingen | |Hallo-naam van het Hallo-metric die welke regel Hallo definieert bewaakt. |
| metricUnit |voor metrische waarschuwingen |'Bytes', 'BytesPerSecond', 'Count', 'CountPerSecond', 'Percentage', 'Seconds' |Hallo-eenheid is toegestaan in Hallo metrische gegevens. [Toegestane waarden worden hier vermeld](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |voor metrische waarschuwingen | |Hallo werkelijke waarde van Hallo-metric die Hallo waarschuwing heeft veroorzaakt. |
| Drempelwaarde |voor metrische waarschuwingen | |Hallo-drempelwaarde in te stellen welke Hallo waarschuwing is geactiveerd. |
| Venstergrootte |voor metrische waarschuwingen | |Hallo periode die is gebruikt toomonitor waarschuwing activiteit op basis van Hallo drempelwaarde. Moet tussen 5 minuten en 1 dag. ISO 8601-duurnotatie. |
| TimeAggregation van |voor metrische waarschuwingen |'Gemiddeld', 'Laatste', 'Maximum', 'Minimale', 'None', 'Totaal' |Hoe moeten Hallo-gegevens die worden verzameld worden gecombineerd gedurende een bepaalde periode. Hallo-standaardwaarde is de gemiddelde. [Toegestane waarden worden hier vermeld](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| Operator |voor metrische waarschuwingen | |Hallo-operator gebruikt toocompare Hallo huidige metrische gegevens toohello ingestelde drempelwaarde. |
| subscriptionId |J | |Azure-abonnement-ID. |
| resourceGroupName |J | |Naam van de resourcegroep Hallo voor Hallo beïnvloed resource. |
| resourceName |J | |Resourcenaam Hallo beïnvloed resource. |
| resourceType |J | |Brontype Hallo beïnvloed resource. |
| resourceId |J | |Bron-ID van Hallo beïnvloed resource. |
| resourceRegion |J | |Regio of de locatie van Hallo beïnvloed resource. |
| portalLink |J | |Directe koppeling toohello portal resource overzichtspagina. |
| properties |N |Optioneel |Een set `<Key, Value>` paren (dat wil zeggen `Dictionary<String, String>`) die bevat details over Hallo-gebeurtenis. Hallo eigenschappenveld is optioneel. In een aangepaste UI of de logische app op basis van een werkstroom, kunnen gebruikers de sleutel en-waarden die kunnen worden doorgegeven via Hallo nettolading invoeren. Hallo alternatieve manier toopass aangepaste eigenschappen back toohello webhook is via Hallo webhook uri zelf (als queryparameters) |

> [!NOTE]
> Hallo eigenschappenveld kan alleen worden ingesteld met Hallo [REST-API van Azure-Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over waarschuwingen van Azure en webhooks in Hallo video [Azure waarschuwingen integreren met PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Azure Automation-scripts (Runbooks) op waarschuwingen van Azure uitvoeren](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Gebruik van de logische App toosend een SMS-bericht via Twilio door een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Gebruik van de logische App toosend een toegestane bericht van een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Gebruik toosend logische App een bericht tooan Azure Queue door een Azure-waarschuwing](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
