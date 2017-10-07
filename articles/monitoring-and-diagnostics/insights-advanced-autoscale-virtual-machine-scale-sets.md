---
title: aaaAdvanced automatisch schalen met behulp van Azure Virtual Machines | Microsoft Docs
description: Maakt gebruik van Resource Manager en VM-Schaalsets met meerdere regels en -profielen die e-mail verzenden en roept u webhook-URL's met de schaalacties.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Configuratie van geavanceerde automatisch schalen met Resource Manager-sjablonen voor VM-Schaalsets
U kunt de schaal in en scale-out in virtuele-Machineschaalsets op basis van drempelwaarden voor prestaties metrische door een terugkerend schema of door een bepaalde datum. U kunt ook e-mail en -webhook meldingen voor schaalacties configureren. Dit overzicht toont een voorbeeld van de configuratie van deze objecten die zijn met een Resource Manager-sjabloon op een VM-Schaalset.

> [!NOTE]
> Tijdens deze procedure worden de Hallo stappen uitgelegd voor VM-Schaalsets, hello dezelfde informatie is van toepassing tooautoscaling [Cloudservices](https://azure.microsoft.com/services/cloud-services/), en [App Service - Web-Apps](https://azure.microsoft.com/services/app-service/web/).
> Voor een eenvoudige schaal in/out-instelling op een VM-Schaalset gebaseerd op een eenvoudige prestaties metrische gegevens zoals CPU, Raadpleeg toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) en [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documenten
>
>

## <a name="walkthrough"></a>Walkthrough
In dit scenario, gebruiken we [Azure Resource Explorer](https://resources.azure.com/) tooconfigure en update Hallo instelling voor automatisch schalen voor een scale-set. Azure Resource Explorer is een eenvoudige manier toomanage Azure-resources via Resource Manager-sjablonen. Als u nieuwe tooAzure Resource Explorer hulpprogramma, lezen [deze inleiding](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Implementeer een nieuwe schaal ingesteld met een instelling voor automatisch schalen die basic. Dit artikel wordt Hallo uit de Snelstartgalerie Azure, met een Windows hello schaalset met een sjabloon basic automatisch schalen. Linux scale ingesteld werk Hallo dezelfde manier.
2. Na het Hallo-scale set wordt gemaakt, gaat u toohello scale set resource van Azure Resource Explorer. U ziet Hallo volgende onder het knooppunt Microsoft.Insights.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    Hallo sjabloon uitvoering een standaardinstelling voor automatisch schalen is gemaakt met de naam van de Hallo **'autoscalewad'**. U kunt aan de rechterkant hello, Hallo volledige definitie van deze instelling voor automatisch schalen weergeven. In dit geval de standaardinstelling voor automatisch schalen hello wordt geleverd met een regel CPU % op basis van scale-out en de schaal.  

3. U kunt nu meer regels op basis van Hallo planning of specifieke vereisten en -profielen toevoegen. We maken een instelling voor automatisch schalen met drie profielen. toounderstand profielen en regels in voor automatisch schalen, Bekijk [Best Practices voor automatisch schalen](insights-autoscale-best-practices.md).  

    | Profielen en regels | Beschrijving |
    |--- | --- |
    | **Profiel** |**Op basis van metrische gegevens en prestaties** |
    | Regel |Aantal berichten Service Bus-wachtrij > x |
    | Regel |Aantal berichten Service Bus-wachtrij < y |
    | Regel |CPU-percentage > n |
    | Regel |CPU-percentage < p |
    | **Profiel** |**Werkdag ochtend uur (geen regels)** |
    | **Profiel** |**Product starten dag (geen regels)** |

4. Hier volgt een hypothetische vergroten/verkleinen scenario dat we voor deze procedure gebruiken.

    * **Op basis van Load** -tooscale of op basis van Hallo belasting van de toepassing die wordt gehost op mijn set.* schaal wilt
    * **Grootte van de wachtrij bericht** -ik een Service Bus-wachtrij voor Hallo binnenkomende berichten toomy toepassing gebruiken. Ik gebruik aantal van de wachtrij van het Hallo-berichten en CPU-percentage en configureren van een standaard profiel tootrigger een schaalactie als het aantal berichten of CPU treffers threshold.* Hallo
    * **Tijd van de week en dag** -ik wil een wekelijks terugkerende 'tijd van de dag Hallo' op basis van profiel 'Hours werkdag ochtend' genoemd. Op basis van historische gegevens, weet ik is beter toohave bepaalde aantal VM-exemplaren toohandle laden van mijn toepassingen tijdens deze time.*
    * **Speciale datums** -ik heb een profiel 'Product starten dag' toegevoegd. Ik vooruit te plannen voor specifieke datums zodat de toepassing gereed toohandle Hallo laden vanwege marketing aankondigingen en wanneer er een nieuw product in Hallo application.* plaatsen
    * *de laatste twee profielen Hallo kunnen ook andere prestaties metrische gebaseerde regels binnen deze hebben. In dit geval ik niet toohave een besloten en in plaats daarvan toorely op Hallo standaard prestaties metriek op basis van regels. Regels zijn optioneel voor Hallo terugkerende en op basis van datum-profielen.*

    Prioriteitsaanduiding van Hallo profielen en regels voor automatisch schalen-engine wordt ook vastgelegd in Hallo [aanbevolen procedures voor automatisch schalen](insights-autoscale-best-practices.md) artikel.
    Raadpleeg voor een lijst met algemene metrische gegevens voor automatisch schalen, [algemene metrische gegevens voor automatisch schalen](insights-autoscale-common-metrics.md)

5. Zorg ervoor dat u zich op Hallo **lezen/schrijven** modus in Resource Explorer

    ![Autoscalewad, instelling standaard voor automatisch schalen](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Klik op bewerken. **Vervang** Hallo 'profielen'-element in de instelling voor automatisch schalen Hello volgende configuratie:

    ![Profielen](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    Zie voor ondersteunde velden en hun waarden [automatisch schalen REST API-documentatie](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). De instelling voor automatisch schalen bevat nu de drie profielen Hallo hierboven is uitgelegd.

7. Tot slot bekijkt hello automatisch schalen **melding** sectie. Meldingen over automatisch schalen kunt u de drie dingen toodo wanneer een scale-out of in actie met succes wordt geactiveerd.
   - Hallo beheerder en co-beheerders van uw abonnement
   - Een set gebruikers een e-mail
   - Activeren van een webhook-aanroep. Wanneer deze gebeurtenis wordt gestart, deze webhook stuurt de metagegevens over Hallo automatisch schalen voorwaarde en Hallo schaalset resource. toolearn meer informatie over het Hallo-nettolading van de webhook automatisch schalen, Zie [configureren Webhook & e-mailmeldingen voor automatisch schalen](insights-autoscale-to-webhook-email.md).

   Hallo na toohello automatisch schalen instelling vervangen toevoegen uw **melding** element waarvan de waarde null is

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   Klik op **plaatsen** knop in Resource Explorer tooupdate Hallo-instelling voor automatisch schalen.

U hebt bijgewerkt een instelling op een VM-Scale set tooinclude meerdere scale profielen voor automatisch schalen en schalen van meldingen.

## <a name="next-steps"></a>Volgende stappen
Gebruik deze koppelingen toolearn meer informatie over automatisch schalen.

[Problemen oplossen met virtuele-Machineschaalsets voor automatisch schalen](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Algemene metrische gegevens voor automatisch schalen](insights-autoscale-common-metrics.md)

[Aanbevolen procedures voor Azure automatisch schalen](insights-autoscale-best-practices.md)

[Beheren met behulp van PowerShell voor automatisch schalen](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Beheren met CLI voor automatisch schalen](insights-cli-samples.md#autoscale)

[Webhook & e-mailmeldingen voor automatisch schalen configureren](insights-autoscale-to-webhook-email.md)
