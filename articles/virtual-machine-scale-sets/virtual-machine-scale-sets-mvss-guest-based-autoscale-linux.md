---
title: Gebruik Azure automatisch schalen met gast metrische gegevens in een sjabloon van Linux scale set | Microsoft Docs
description: Meer informatie over hoe u met behulp van de Gast metrische gegevens in een sjabloon van Linux virtuele-Machineschaalset voor automatisch schalen
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
ms.openlocfilehash: ac0bbb4dbfccca3f3fc31526aeff11afe55d44be
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="autoscale-using-guest-metrics-in-a-linux-scale-set-template"></a><span data-ttu-id="3a114-103">Met behulp van de Gast metrische gegevens in een sjabloon van Linux scale set voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="3a114-103">Autoscale using guest metrics in a Linux scale set template</span></span>

<span data-ttu-id="3a114-104">Er zijn twee soorten metrische gegevens in Azure die worden verzameld uit de virtuele machines en schalen sets: sommige afkomstig zijn van de VM-host en anderen afkomstig zijn van de Gast-VM.</span><span class="sxs-lookup"><span data-stu-id="3a114-104">There are two types of metrics in Azure that are gathered from VMs and scale sets: some come from the host VM and others come from the guest VM.</span></span> <span data-ttu-id="3a114-105">Host metrische gegevens vereisen geen aanvullende instellingen omdat ze zijn verzameld door de host VM, terwijl Gast metrische gegevens ons vereisen voor het installeren van de [Windows Azure Diagnostics extensie](../virtual-machines/windows/extensions-diagnostics-template.md) of de [Linux Azure Diagnostics-uitbreiding ](../virtual-machines/linux/diagnostic-extension.md) in de Gast-VM.</span><span class="sxs-lookup"><span data-stu-id="3a114-105">Host metrics do not require additional setup because they are collected by the host VM, whereas guest metrics require us to install the [Windows Azure Diagnostics extension](../virtual-machines/windows/extensions-diagnostics-template.md) or the [Linux Azure Diagnostics extension](../virtual-machines/linux/diagnostic-extension.md) in the guest VM.</span></span> <span data-ttu-id="3a114-106">Een veelvoorkomende reden Gast metrische gegevens gebruiken in plaats van de host metrische gegevens is dat Gast metrische gegevens bestaan uit een grotere selectie van metrische gegevens dan host metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a114-106">One common reason to use guest metrics instead of host metrics is that guest metrics provide a larger selection of metrics than host metrics.</span></span> <span data-ttu-id="3a114-107">Een voorbeeld is geheugenverbruik hoger metrische gegevens, die alleen beschikbaar via de Gast metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a114-107">One such example is memory-consumption metrics, which are only available via guest metrics.</span></span> <span data-ttu-id="3a114-108">De metrische gegevens van ondersteunde host staan [hier](../monitoring-and-diagnostics/monitoring-supported-metrics.md), en veelgebruikte Gast metrische gegevens staan [hier](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3a114-108">The supported host metrics are listed [here](../monitoring-and-diagnostics/monitoring-supported-metrics.md), and commonly used guest metrics are listed [here](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span> <span data-ttu-id="3a114-109">Dit artikel laat zien hoe u wijzigt de [minimale levensvatbaar schaalset sjabloon](./virtual-machine-scale-sets-mvss-start.md) automatisch schalen regels op basis van de Gast metrische gegevens voor Linux-schaalsets.</span><span class="sxs-lookup"><span data-stu-id="3a114-109">This article shows how to modify the [minimum viable scale set template](./virtual-machine-scale-sets-mvss-start.md) to use autoscale rules based on guest metrics for Linux scale sets.</span></span>

## <a name="change-the-template-definition"></a><span data-ttu-id="3a114-110">De sjabloondefinitie wijzigen</span><span class="sxs-lookup"><span data-stu-id="3a114-110">Change the template definition</span></span>

<span data-ttu-id="3a114-111">Onze minimale levensvatbaar scale set sjabloon kan worden gezien [hier](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), en de sjabloon voor het implementeren van de schaal Linux ingesteld met automatisch schalen op basis van een gast zichtbaar [hier](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="3a114-111">Our minimum viable scale set template can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json), and our template for deploying the Linux scale set with guest-based autoscale can be seen [here](https://raw.githubusercontent.com/gatneil/mvss/guest-based-autoscale-linux/azuredeploy.json).</span></span> <span data-ttu-id="3a114-112">We bekijken de diff gebruikt voor het maken van deze sjabloon (`git diff minimum-viable-scale-set existing-vnet`) stuk door stuk:</span><span class="sxs-lookup"><span data-stu-id="3a114-112">Let's examine the diff used to create this template (`git diff minimum-viable-scale-set existing-vnet`) piece by piece:</span></span>

<span data-ttu-id="3a114-113">Voeg eerst we parameters voor `storageAccountName` en `storageAccountSasToken`.</span><span class="sxs-lookup"><span data-stu-id="3a114-113">First, we add parameters for `storageAccountName` and `storageAccountSasToken`.</span></span> <span data-ttu-id="3a114-114">De diagnostics-agent wordt metrische gegevens opslaan in een [tabel](../cosmos-db/table-storage-how-to-use-dotnet.md) in dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3a114-114">The diagnostics agent will store metric data in a [table](../cosmos-db/table-storage-how-to-use-dotnet.md) in this storage account.</span></span> <span data-ttu-id="3a114-115">Vanaf de Diagnostics Linux Agent versie 3.0, met behulp van een toegangssleutel voor opslag is niet langer ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3a114-115">As of the Linux Diagnostics Agent version 3.0, using a storage access key is no longer supported.</span></span> <span data-ttu-id="3a114-116">We gebruiken moet een [SAS-Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="3a114-116">We must use a [SAS Token](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

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

<span data-ttu-id="3a114-117">Vervolgens wijzigt u de schaalaanpassingsset `extensionProfile` om op te nemen van de extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a114-117">Next, we modify the scale set `extensionProfile` to include the diagnostics extension.</span></span> <span data-ttu-id="3a114-118">In deze configuratie is opgegeven de resource-ID van de schaal instelt voor het verzamelen van meetgegevens van, evenals de storage-account en SAS-token te gebruiken voor het opslaan van de metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a114-118">In this configuration, we specify the resource ID of the scale set to collect metrics from, as well as the storage account and SAS token to use to store the metrics.</span></span> <span data-ttu-id="3a114-119">We ook opgeven hoe vaak de metrische gegevens worden geaggregeerd (in dit geval wordt elke minuut) en welke metrische gegevens bijhouden (in dit geval percentage gebruikt geheugen).</span><span class="sxs-lookup"><span data-stu-id="3a114-119">We also specify how frequently the metrics are aggregated (in this case every minute) and which metrics to track (in this case percent used memory).</span></span> <span data-ttu-id="3a114-120">Zie voor meer informatie over deze configuratie gedetailleerde en metrische gegevens dan percentage geheugen gebruikt, [deze documentatie](../virtual-machines/linux/diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="3a114-120">For more detailed information on this configuration and metrics other than percent used memory, see [this documentation](../virtual-machines/linux/diagnostic-extension.md).</span></span>

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

<span data-ttu-id="3a114-121">Ten slotte we voegen een `autoscaleSettings` bron configureren voor automatisch schalen op basis van deze metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a114-121">Finally, we add an `autoscaleSettings` resource to configure autoscale based on these metrics.</span></span> <span data-ttu-id="3a114-122">Deze bron heeft een `dependsOn` component die verwijst naar de schaal instellen om ervoor te zorgen dat de schaalaanpassingsset voordat u probeert te schalen deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="3a114-122">This resource has a `dependsOn` clause that references the scale set to ensure that the scale set exists before attempting to autoscale it.</span></span> <span data-ttu-id="3a114-123">Als er een andere waarde automatisch te schalen op kiest, zouden we gebruiken de `counterSpecifier` van de configuratie voor de uitbreiding van diagnostische gegevens als de `metricName` in de configuratie voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="3a114-123">If we choose a different metric to autoscale on, we would use the `counterSpecifier` from the diagnostics extension configuration as the `metricName` in the autoscale configuration.</span></span> <span data-ttu-id="3a114-124">Zie voor meer informatie over de configuratie voor automatisch schalen, de [aanbevolen procedures voor automatisch schalen](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) en de [Azure Monitor REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a114-124">For more information on autoscale configuration, see the [autoscale best practices](..//monitoring-and-diagnostics/insights-autoscale-best-practices.md) and the [Azure Monitor REST API reference documentation](https://msdn.microsoft.com/library/azure/dn931928.aspx).</span></span>

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





## <a name="next-steps"></a><span data-ttu-id="3a114-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a114-125">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
