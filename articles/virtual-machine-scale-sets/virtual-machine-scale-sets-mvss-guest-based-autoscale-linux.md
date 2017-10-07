---
title: Gebruik Azure automatisch schalen met gast metrische gegevens in een sjabloon van Linux scale set | Microsoft Docs
description: Meer informatie over hoe tooautoscale met behulp van de Gast metrische gegevens in een sjabloon van Linux virtuele-Machineschaalset
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: na
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: negat
ms.openlocfilehash: 7afbef943a5f15c7a72dcf7114f46d521c504424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a>Met behulp van de Gast metrische gegevens in een sjabloon van Linux scale set voor automatisch schalen

Er zijn twee soorten metrische gegevens in Azure die worden verzameld uit de virtuele machines en schalen sets: sommige afkomstig zijn uit Hallo host VM en anderen afkomstig zijn van Hallo Gast-VM. Host metrische gegevens vereisen geen aanvullende instellingen omdat ze zijn verzameld door Hallo host, VM, terwijl de Gast metrische gegevens vereisen ons tooinstall hello [Windows Azure Diagnostics extensie](../virtual-machines/windows/extensions-diagnostics-template.md) of Hallo [Linux Azure Diagnostics extensie](../virtual-machines/linux/diagnostic-extension.md) in Hallo Gast-VM. Een veelvoorkomende reden toouse Gast metrische gegevens in plaats van de host metrische gegevens is dat Gast metrische gegevens bestaan uit een grotere selectie van metrische gegevens dan host metrische gegevens. Een voorbeeld is geheugenverbruik hoger metrische gegevens, die alleen beschikbaar via de Gast metrische gegevens. Hallo ondersteund host metrische gegevens worden vermeld [hier](../monitoring-and-diagnostics/monitoring-supported-metrics.md), en veelgebruikte Gast metrische gegevens staan [hier](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md). Dit artikel laat zien hoe toomodify hello [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) toouse automatisch schalen regels op basis van de Gast metrische gegevens voor Linux-schaalsets.

## <a name="change-hello-template-definition"></a>Hallo Sjabloondefinitie wijzigen

Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor de implementatie van Hallo Linux schaal instelt met automatisch schalen op basis van een gast zichtbaar [hier](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json). Behandeld Hallo diff gebruikt toocreate deze sjabloon (`git diff minimum-viable-scale-set existing-vnet`) stuk door stuk:

Voeg eerst we parameters voor `storageAccountName` en `storageAccountSasToken`. Hallo diagnostics agent wordt metrische gegevens opslaan in een [tabel](../cosmos-db/table-storage-how-to-use-dotnet.md) in dit opslagaccount. Vanaf Hallo Linux Diagnostics Agent versie 3.0, met behulp van een toegangssleutel voor opslag is niet langer ondersteund. We gebruiken moet een [SAS-Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

```diff
     },
     "adminPassword": {
       "type": "securestring"
+    },
+    "storageAccountName": {
+      "type": "string"
+    },
+    "storageAccountSasToken": {
+      "type": "securestring"
     }
   },
```

Vervolgens wijzigt u Hallo schaalset `extensionProfile` tooinclude Hallo: extensie voor diagnostische gegevens. In deze configuratie we Hallo resource-ID van de schaal Hallo ingesteld toocollect metrische gegevens van opgeven, evenals Hallo storage-account en SAS-token toouse toostore Hallo metrische gegevens. We ook opgeven hoe vaak Hallo metrische gegevens zijn samengevoegd (in dit geval wordt elke minuut) en welke tootrack metrische gegevens (in dit geval percentage gebruikt geheugen). Zie voor meer informatie over deze configuratie gedetailleerde en metrische gegevens dan percentage geheugen gebruikt, [deze documentatie](../virtual-machines/linux/diagnostic-extension.md).

```diff
                 }
               }
             ]
+          },
+          "extensionProfile": {
+            "extensions": [
+              {
+                "name": "LinuxDiagnosticExtension",
+                "properties": {
+                  "publisher": "Microsoft.Azure.Diagnostics",
+                  "type": "LinuxDiagnostic",
+                  "typeHandlerVersion": "3.0",
+                  "settings": {
+                    "StorageAccount": "[parameters('storageAccountName')]",
+                    "ladCfg": {
+                      "diagnosticMonitorConfiguration": {
+                        "performanceCounters": {
+                          "sinks": "WADMetricJsonBlob",
+                          "performanceCounterConfiguration": [
+                            {
+                              "unit": "percent",
+                              "type": "builtin",
+                              "class": "memory",
+                              "counter": "percentUsedMemory",
+                              "counterSpecifier": "/builtin/memory/percentUsedMemory",
+                              "condition": "IsAggregate=TRUE"
+                            }
+                          ]
+                        },
+                        "metrics": {
+                          "metricAggregation": [
+                            {
+                              "scheduledTransferPeriod": "PT1M"
+                            }
+                          ],
+                          "resourceId": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]"
+                        }
+                      }
+                    }
+                  },
+                  "protectedSettings": {
+                    "storageAccountName": "[parameters('storageAccountName')]",
+                    "storageAccountSasToken": "[parameters('storageAccountSasToken')]",
+                    "sinksConfig": {
+                      "sink": [
+                        {
+                          "name": "WADMetricJsonBlob",
+                          "type": "JsonBlob"
+                        }
+                      ]
+                    }
+                  }
+                }
+              }
+            ]
           }
         }
       }
```

Ten slotte we voegen een `autoscaleSettings` resource tooconfigure automatisch schalen op basis van deze metrische gegevens. Deze bron heeft een `dependsOn` component die verwijst naar Hallo scale ingesteld tooensure die Hallo scale set bestaat voordat u probeert tooautoscale deze. Als er een andere metrische tooautoscale op kiest, zouden we hello gebruiken `counterSpecifier` van Hallo diagnostics extensie configuratie als Hallo `metricName` in Hallo automatisch schalen configuratie. Zie voor meer informatie over automatisch schalen configuratie Hallo [aanbevolen procedures voor automatisch schalen](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) en Hallo [Azure Monitor REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn931928.aspx).

```diff
+    },
+    {
+      "type": "Microsoft.Insights/autoscaleSettings",
+      "apiVersion": "2015-04-01",
+      "name": "guestMetricsAutoscale",
+      "location": "[resourceGroup().location]",
+      "dependsOn": [
+        "Microsoft.Compute/virtualMachineScaleSets/myScaleSet"
+      ],
+      "properties": {
+        "name": "guestMetricsAutoscale",
+        "targetResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+        "enabled": true,
+        "profiles": [
+          {
+            "name": "Profile1",
+            "capacity": {
+              "minimum": "1",
+              "maximum": "10",
+              "default": "3"
+            },
+            "rules": [
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "GreaterThan",
+                  "threshold": 60
+                },
+                "scaleAction": {
+                  "direction": "Increase",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              },
+              {
+                "metricTrigger": {
+                  "metricName": "/builtin/memory/percentUsedMemory",
+                  "metricNamespace": "",
+                  "metricResourceUri": "[resourceId('Microsoft.Compute/virtualMachineScaleSets', 'myScaleSet')]",
+                  "timeGrain": "PT1M",
+                  "statistic": "Average",
+                  "timeWindow": "PT5M",
+                  "timeAggregation": "Average",
+                  "operator": "LessThan",
+                  "threshold": 30
+                },
+                "scaleAction": {
+                  "direction": "Decrease",
+                  "type": "ChangeCount",
+                  "value": "1",
+                  "cooldown": "PT1M"
+                }
+              }
+            ]
+          }
+        ]
+      }
     }
   ]
 }
```





## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
