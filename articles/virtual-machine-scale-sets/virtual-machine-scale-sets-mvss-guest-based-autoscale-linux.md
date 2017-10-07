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
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="1b4bd-103">Met behulp van de Gast metrische gegevens in een sjabloon van Linux scale set voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="1b4bd-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="1b4bd-104">Er zijn twee soorten metrische gegevens in Azure die worden verzameld uit de virtuele machines en schalen sets: sommige afkomstig zijn uit Hallo host VM en anderen afkomstig zijn van Hallo Gast-VM.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from hello host VM and others come from hello guest VM.</span></span> <span data-ttu-id="1b4bd-105">Host metrische gegevens vereisen geen aanvullende instellingen omdat ze zijn verzameld door Hallo host, VM, terwijl de Gast metrische gegevens vereisen ons tooinstall hello [Windows Azure Diagnostics extensie](../virtual-machines/windows/extensions-diagnostics-template.md) of Hallo [Linux Azure Diagnostics extensie](../virtual-machines/linux/diagnostic-extension.md) in Hallo Gast-VM.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-105">Host metrics do not require additional setup because they are collected by hello host VM, whereas guest metrics require us tooinstall hello [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or hello [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in hello guest VM.</span></span> <span data-ttu-id="1b4bd-106">Een veelvoorkomende reden toouse Gast metrische gegevens in plaats van de host metrische gegevens is dat Gast metrische gegevens bestaan uit een grotere selectie van metrische gegevens dan host metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-106">One common reason toouse guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="1b4bd-107">Een voorbeeld is geheugenverbruik hoger metrische gegevens, die alleen beschikbaar via de Gast metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="1b4bd-108">Hallo ondersteund host metrische gegevens worden vermeld [hier](../monitoring-and-diagnostics/monitoring-supported-metrics.md), en veelgebruikte Gast metrische gegevens staan [hier](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="1b4bd-108">hello supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="1b4bd-109">Dit artikel laat zien hoe toomodify hello [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) toouse automatisch schalen regels op basis van de Gast metrische gegevens voor Linux-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-109">This article shows how toomodify hello [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) toouse autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-hello-template-definition"></a><span data-ttu-id="1b4bd-110">Hallo Sjabloondefinitie wijzigen</span><span class="sxs-lookup"><span data-stu-id="1b4bd-110">Change hello template definition</span></span>

<span data-ttu-id="1b4bd-111">Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor de implementatie van Hallo Linux schaal instelt met automatisch schalen op basis van een gast zichtbaar [hier](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="1b4bd-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying hello Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="1b4bd-112">Behandeld Hallo diff gebruikt toocreate deze sjabloon (`git diff minimum-viable-scale-set existing-vnet`) stuk door stuk:</span><span class="sxs-lookup"><span data-stu-id="1b4bd-112">Let's examine hello diff used toocreate this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="1b4bd-113">Voeg eerst we parameters voor `storageAccountName` en `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="1b4bd-114">Hallo diagnostics agent wordt metrische gegevens opslaan in een [tabel](../cosmos-db/table-storage-how-to-use-dotnet.md) in dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-114">hello diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="1b4bd-115">Vanaf Hallo Linux Diagnostics Agent versie 3.0, met behulp van een toegangssleutel voor opslag is niet langer ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-115">As of hello Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="1b4bd-116">We gebruiken moet een [SAS-Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="1b4bd-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="1b4bd-117">Vervolgens wijzigt u Hallo schaalset `extensionProfile` tooinclude Hallo: extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-117">Next, we modify hello scale set `extensionProfile` tooinclude hello diagnostics extension.</span></span> <span data-ttu-id="1b4bd-118">In deze configuratie we Hallo resource-ID van de schaal Hallo ingesteld toocollect metrische gegevens van opgeven, evenals Hallo storage-account en SAS-token toouse toostore Hallo metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-118">In this configuration, we specify hello resource ID of hello scale set toocollect metrics from, as well as hello storage account and SAS token toouse toostore hello metrics.</span></span> <span data-ttu-id="1b4bd-119">We ook opgeven hoe vaak Hallo metrische gegevens zijn samengevoegd (in dit geval wordt elke minuut) en welke tootrack metrische gegevens (in dit geval percentage gebruikt geheugen).</span><span class="sxs-lookup"><span data-stu-id="1b4bd-119">We also specify how frequently hello metrics are aggregated (in this case every minute) and which metrics tootrack (in this case percent used memory).</span></span> <span data-ttu-id="1b4bd-120">Zie voor meer informatie over deze configuratie gedetailleerde en metrische gegevens dan percentage geheugen gebruikt, [deze documentatie](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1b4bd-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="1b4bd-121">Ten slotte we voegen een `autoscaleSettings` resource tooconfigure automatisch schalen op basis van deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-121">Finally, we add an `autoscaleSettings` resource tooconfigure autoscale based on these metrics.</span></span> <span data-ttu-id="1b4bd-122">Deze bron heeft een `dependsOn` component die verwijst naar Hallo scale ingesteld tooensure die Hallo scale set bestaat voordat u probeert tooautoscale deze.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-122">This resource has a `dependsOn` clause that references hello scale set tooensure that hello scale set exists before attempting tooautoscale it.</span></span> <span data-ttu-id="1b4bd-123">Als er een andere metrische tooautoscale op kiest, zouden we hello gebruiken `counterSpecifier` van Hallo diagnostics extensie configuratie als Hallo `metricName` in Hallo automatisch schalen configuratie.</span><span class="sxs-lookup"><span data-stu-id="1b4bd-123">If we choose a different metric tooautoscale on, we would use hello `counterSpecifier` from hello diagnostics extension configuration as hello `metricName` in hello autoscale configuration.</span></span> <span data-ttu-id="1b4bd-124">Zie voor meer informatie over automatisch schalen configuratie Hallo [aanbevolen procedures voor automatisch schalen](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) en Hallo [Azure Monitor REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="1b4bd-124">For more information on autoscale configuration, see hello [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and hello [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="1b4bd-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b4bd-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
