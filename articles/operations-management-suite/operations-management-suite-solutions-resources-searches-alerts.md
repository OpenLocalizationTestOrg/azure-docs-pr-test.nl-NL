---
title: aaaSaved zoekopdrachten en waarschuwingen in de OMS-oplossingen | Microsoft Docs
description: "Oplossingen in OMS omvatten meestal opgeslagen zoekopdrachten in logboekanalyse tooanalyze gegevens verzameld door Hallo-oplossing.  Ze kunnen ook waarschuwingen toonotify Hallo-gebruiker definiëren of automatisch actie ondernemen in het antwoord tooa Kritiek probleem.  Dit artikel wordt beschreven hoe toodefine logboekanalyse opgeslagen zoekopdrachten en waarschuwingen in een ARM-sjabloon zodat ze kunnen worden opgenomen beheersystemen."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Zoekopdrachten en waarschuwingen tooOMS beheeroplossing (Preview) toe te voegen logboekanalyse opgeslagen

> [!NOTE]
> Dit is voorlopige documentatie voor het maken van oplossingen voor het beheer in OMS die zich momenteel in preview. De hieronder beschreven schema is onderwerp toochange.   


[Oplossingen voor het beheer in OMS](operations-management-suite-solutions.md) omvatten meestal [opgeslagen zoekopdrachten](../log-analytics/log-analytics-log-searches.md) in logboekanalyse tooanalyze gegevens verzameld door Hallo-oplossing.  Ze kunnen ook definiëren [waarschuwingen](../log-analytics/log-analytics-alerts.md) toonotify Hallo gebruiker of automatisch actie ondernemen in het antwoord tooa Kritiek probleem.  Dit artikel wordt beschreven hoe toodefine logboekanalyse opgeslagen zoekopdrachten en waarschuwingen in een [Resource Management-sjabloon](../resource-manager-template-walkthrough.md) zodat ze kunnen worden opgenomen [beheeroplossingen](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Hallo voorbeelden in dit artikel gebruiken parameters en variabelen die zijn beide vereist of algemene toomanagement oplossingen en wordt beschreven in [beheeroplossingen maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u al bekend met het te bent[maken van een beheeroplossing](operations-management-suite-solutions-creating.md) en Hallo-structuur van een [ARM-sjabloon](../resource-group-authoring-templates.md) en oplossingsbestand.


## <a name="log-analytics-workspace"></a>Log Analytics-werkruimte
Alle resources in logboekanalyse zijn opgenomen in een [werkruimte](../log-analytics/log-analytics-manage-access.md).  Zoals beschreven in [OMS werkruimte en de Automation-account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) Hallo-werkruimte niet is opgenomen in de oplossing voor het beheer van hello, maar moet bestaan voordat het Hallo-oplossing is geïnstalleerd.  Als het is niet beschikbaar, mislukken Hallo oplossing installatie.

Hallo-naam van Hallo werkruimte is in Hallo-naam van elke resource logboekanalyse.  Dit wordt gedaan Hallo-oplossing met Hallo **werkruimte** parameter zoals in het volgende voorbeeld van een resource savedsearch Hallo.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Opgeslagen zoekopdrachten
Omvatten [opgeslagen zoekopdrachten](../log-analytics/log-analytics-log-searches.md) in een oplossing tooallow gebruikers tooquery gegevens verzameld door uw oplossing.  Opgeslagen zoekopdrachten worden weergegeven onder **Favorieten** in Hallo OMS-portal en **opgeslagen zoekacties** in hello Azure-portal.  Een opgeslagen zoekopdracht is ook vereist voor elke waarschuwing.   

[Log Analytics opgeslagen zoekopdracht](../log-analytics/log-analytics-log-searches.md) resources zijn een type `Microsoft.OperationalInsights/workspaces/savedSearches` en hebben Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Elk van de eigenschappen van een opgeslagen zoekopdracht Hallo worden beschreven in de volgende tabel Hallo. 

| Eigenschap | Beschrijving |
|:--- |:--- |
| category | Hallo categorie voor Hallo opgeslagen zoekopdracht.  Alle opgeslagen zoekopdrachten in Hallo dezelfde oplossing vaak delen één categorie zodat ze samen worden gegroepeerd in Hallo-console. |
| weergavenaam | Naam toodisplay voor Hallo opgeslagen zoekopdracht in Hallo-portal. |
| query | Query toorun. |

> [!NOTE]
> Mogelijk moet u toouse escape-tekens in Hallo-query als deze tekens bevat die kunnen worden geïnterpreteerd als JSON.  Bijvoorbeeld, als de query is **Type: AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write '**, deze worden geschreven in het oplossingsbestand Hallo als **Type: AzureActivity OperationName:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Waarschuwingen
[Meld u Analytics waarschuwingen](../log-analytics/log-analytics-alerts.md) zijn gemaakt door regels voor waarschuwingen die een opgeslagen zoekopdracht op een vast interval uitvoert.  Hallo-resultaten van Hallo query aan opgegeven criteria voldoen, een waarschuwing wordt vastgelegd als een of meer acties worden uitgevoerd.  

Waarschuwingsregels in een beheersysteem bestaan Hallo na drie verschillende bronnen.

- **Opgeslagen zoekopdracht.**  Hiermee definieert u Hallo logboek zoeken die worden uitgevoerd.  Meerdere regels voor waarschuwingen kunnen een enkele opgeslagen zoekopdracht delen.
- **Plannen.**  Hiermee definieert u hoe vaak hello logboek zoekopdracht wordt uitgevoerd.  Elke waarschuwingsregel wordt slechts één schema hebben.
- **Actie van de waarschuwing.**  Elke waarschuwingsregel heeft een actie-resource met een type **waarschuwing** Hallo details van de waarschuwing Hallo zoals Hallo criteria voor wanneer een record voor een waarschuwing wordt gemaakt en de ernst van waarschuwing Hallo te definiëren.  Hallo actie resource definieert eventueel een e-mail en runbook-antwoord.
- **De actie van de Webhook is (optioneel).**  Als Hallo waarschuwingsregel wordt een webhook aanroepen, wordt een actie van extra resource met een type vereist **Webhook**.    

Opgeslagen zoekopdracht resources hierboven zijn beschreven.  Hallo worden andere resources hieronder beschreven.


### <a name="schedule-resource"></a>Schema-resource

Een opgeslagen zoekopdracht kan een of meer schema's met het schema voor een afzonderlijke waarschuwingsregel hebben. Hallo bepaalt planning hoe vaak hello zoekopdracht wordt uitgevoerd en Hallo tijdsinterval via welke Hallo gegevens worden opgehaald.  Planning resources zijn een type `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` en hebben Hallo structuur te volgen. Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



Hallo-eigenschappen voor schema-bronnen worden beschreven in de volgende tabel Hallo.

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| ingeschakeld       | Ja | Hiermee geeft u op of Hallo waarschuwing is ingeschakeld wanneer deze wordt gemaakt. |
| interval      | Ja | Hoe vaak hello query wordt uitgevoerd in minuten. |
| QueryTimeSpan | Ja | De lengte van de tijd in minuten over welke tooevaluate resultaten. |

Hallo planning resource dient is afhankelijk van Hallo opgeslagen zoekopdracht zodat deze gemaakt voordat het Hallo-schema.


### <a name="actions"></a>Acties
Er zijn twee soorten actie resource die is opgegeven door Hallo **Type** eigenschap.  Een planning vereist één **waarschuwing** actie waarmee wordt gedefinieerd Hallo details van de waarschuwingsregel Hallo en welke acties worden uitgevoerd wanneer een waarschuwing wordt gemaakt.  Het kan ook betekenen dat een **Webhook** actie als een webhook moet worden aangeroepen vanuit Hallo waarschuwing.  

Actie resources zijn een type `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Waarschuwingsacties

Elke planning heeft een **waarschuwing** in te grijpen.  Hiermee definieert u Hallo details van Hallo waarschuwing en eventueel acties melding en herstel.  Een melding verzendt een e-tooone of meer adressen.  Een herstel wordt een runbook in Azure Automation tooattempt tooremediate Hallo gedetecteerd probleem gestart.

Waarschuwing acties hebben Hallo structuur te volgen.  Dit omvat de algemene variabelen en parameters zodat u kunt kopiëren en plak dit codefragment in uw oplossingsbestand en Hallo parameternamen wijzigen. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

Hallo-eigenschappen voor de actie waarschuwing resources worden beschreven in Hallo tabellen te volgen.

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| Type | Ja | Type Hallo actie.  Dit is **waarschuwing** voor meldingen. |
| Naam | Ja | Weergavenaam voor Hallo waarschuwing.  Dit is Hallo-naam die wordt weergegeven in de console Hallo voor Hallo waarschuwingsregel. |
| Beschrijving | Nee | Optionele beschrijving van waarschuwing Hallo. |
| Ernst | Ja | Ernst van waarschuwing Hallo-record van Hallo volgende waarden:<br><br> **Kritieke**<br>**Waarschuwing**<br>**Informatief** |


##### <a name="threshold"></a>Drempelwaarde
Deze sectie is vereist.  Het definieert Hallo-eigenschappen voor Hallo waarschuwingsdrempel.

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| Operator | Ja | De operator voor vergelijking van de volgende waarden Hallo Hallo:<br><br>**gt = groter is dan<br>lt = kleiner dan** |
| Waarde | Ja | Hallo waarde toocompare Hallo resultaten. |


##### <a name="metricstrigger"></a>MetricsTrigger
Deze sectie is optioneel.  Op te nemen voor een waarschuwing metrische meting.

> [!NOTE]
> Metrische maateenheids waarschuwingen zijn momenteel in de openbare preview. 

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| TriggerCondition | Ja | Hiermee bepaalt u of Hallo drempelwaarde voor het totale aantal schendingen of opeenvolgende schendingen van Hallo volgende waarden:<br><br>**Totaal aantal<br>opeenvolgende** |
| Operator | Ja | De operator voor vergelijking van de volgende waarden Hallo Hallo:<br><br>**gt = groter is dan<br>lt = kleiner dan** |
| Waarde | Ja | Aantal Hallo tijden Hallo criteria moet zijn voldaan tootrigger Hallo waarschuwing. |

##### <a name="throttling"></a>Beperking
Deze sectie is optioneel.  Deze sectie bevatten als u wilt dat waarschuwingen van de toosuppress van Hallo dezelfde regel voor een bepaalde hoeveelheid tijd nadat een waarschuwing is gemaakt.

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| DurationInMinutes | Ja als u beperking van element opgenomen | Het aantal minuten de waarschuwingen toosuppress na één van Hallo dezelfde waarschuwingsregel wordt gemaakt. |

##### <a name="emailnotification"></a>EmailNotification
 Deze sectie is optioneel opnemen als u wilt dat Hallo waarschuwing toosend mail tooone of meer geadresseerden.

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| ontvangers | Ja | Door komma's gescheiden lijst met e-mailadres adressen toosend melding wanneer een waarschuwing wordt gemaakt, zoals in Hallo voorbeeld te volgen.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Onderwerp | Ja | De onderwerpregel van Hallo e-mail. |
| Bijlage | Nee | Bijlagen worden momenteel niet ondersteund.  Als dit element is opgenomen, worden deze **geen**. |


##### <a name="remediation"></a>Herstel
Deze sectie is optioneel als u een runbook toostart in antwoord toohello waarschuwing wilt opnemen. |

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| RunbookName | Ja | Naam van Hallo runbook toostart. |
| WebhookUri | Ja | De URI van de webhook Hallo voor Hallo runbook. |
| Verloopdatum | Nee | Datum en tijd waarop het herstel Hallo verloopt. |

#### <a name="webhook-actions"></a>Webhookacties

Een proces starten webhookacties door het aanroepen van een URL en het eventueel geven een nettolading toobe verzonden. Ze zijn vergelijkbaar tooRemediation acties maar ze zijn bedoeld voor webhooks die van processen dan Azure Automation-runbooks gebruikmaken mogelijk. Ze bieden ook een extra optie Hallo van het bieden van een nettolading toobe bezorgd toohello extern proces.

Als de waarschuwing wordt een webhook aanroepen, dan deze een actie-resource met een type moet **Webhook** in toevoeging toohello **waarschuwing** actie resource.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

Hallo-eigenschappen voor Webhook actie resources worden beschreven in Hallo tabellen te volgen.

| Elementnaam | Vereist | Beschrijving |
|:--|:--|:--|
| type | Ja | Type Hallo actie.  Dit is **Webhook** voor webhookacties. |
| naam | Ja | Weergavenaam voor Hallo actie.  Dit wordt niet weergegeven in Hallo-console. |
| wehookUri | Ja | De URI voor Hallo webhook. |
| CustomPayload | Nee | Aangepaste nettolading toobe toohello webhook verzonden. Hallo-indeling afhankelijk van welke webhook hello wordt verwacht. |




## <a name="sample"></a>Voorbeeld

Hier volgt een voorbeeld van een oplossing die bevatten die Hallo resources te volgen:

- Opgeslagen zoekopdracht
- Planning
- Actie waarschuwing
- Webhook-actie

voorbeeld gebruikt Hallo [standaardoplossing parameters](operations-management-suite-solutions-solution-file.md#parameters) variabelen die meestal in een oplossing als gebruikt wordt toohardcoding waarden in de resourcedefinities Hallo geboden.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Hallo na parameterbestand biedt voorbeelden van waarden voor deze oplossing.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Volgende stappen
* [Weergaven toevoegen](operations-management-suite-solutions-resources-views.md) tooyour-beheeroplossing.
* [Automation-runbooks en andere resources toevoegen](operations-management-suite-solutions-resources-automation.md) tooyour-beheeroplossing.

