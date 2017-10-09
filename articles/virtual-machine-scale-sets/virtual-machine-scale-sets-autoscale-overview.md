---
title: aaaAutomatic schalen en de virtuele machine schalen sets | Microsoft Docs
description: Meer informatie over het gebruik van diagnostische gegevens en automatisch schalen resources tooautomatically scale virtuele machines in een schaalset.
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d29a3385-179e-4331-a315-daa7ea5701df
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: adegeo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 25f54b693e3c991577238242008c262023ed479c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-automatic-scaling-and-virtual-machine-scale-sets"></a>Hoe toouse automatisch schalen en virtuele-Machineschaalsets
Automatische schaling van virtuele machines in een scale-set is Hallo maken of verwijderen van virtuele machines in Hallo instellen als nodig is toomatch prestatie-eisen. Wanneer Hallo volume van werk groeit, een toepassing mogelijk aanvullende bronnen tooenable het tooeffectively taken uitvoeren.

Automatische schaling is een geautomatiseerd proces gemakkelijk beheeroverhead. Vermindert de overhead, of u kunt geen toocontinually monitor systeemprestaties bepalen hoe toomanage resources. Schalen is een elastische proces. Meer bronnen kunnen worden toegevoegd als Hallo belasting toeneemt. En als de aanvraag-afname resources kunnen verwijderde toominimize kosten worden en prestatieniveaus onderhouden.

Stel automatisch schalen op een schaal ingesteld met behulp van een Azure Resource Manager-sjabloon, Azure PowerShell, Azure CLI of hello Azure-portal.

## <a name="set-up-scaling-by-using-resource-manager-templates"></a>Een schaal met behulp van Resource Manager-sjablonen instellen
In plaats van te implementeren en beheren van elke resource van uw toepassing afzonderlijk, een sjabloon gebruiken waarmee alle resources in een enkele, gecoördineerde bewerking implementeert. In de sjabloon hello, toepassingsbronnen worden gedefinieerd en implementatieparameters zijn opgegeven voor verschillende omgevingen. Hallo sjabloon bestaat uit JSON en uitdrukkingen die u kunt tooconstruct waarden voor uw implementatie te gebruiken. toolearn meer, Bekijk [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).

Geef in het Hallo-sjabloon Hallo capaciteit element:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 3
},
```

Capaciteit van identificeert het aantal virtuele machines in de set Hallo Hallo. U kunt handmatig Hallo capaciteit wijzigen door het implementeren van een sjabloon met een andere waarde. Als u een sjabloon tooonly wijziging Hallo capaciteit implementeert, kunt u alleen Hallo SKU-element met Hallo bijgewerkt capaciteit kunt opnemen.

Hallo capaciteit van uw scale set kan worden automatisch aangepast door een combinatie van Hallo **autoscaleSettings** resource en Hallo extensie voor diagnostische gegevens.

### <a name="configure-hello-azure-diagnostics-extension"></a>Hello Azure Diagnostics-uitbreiding configureren
Automatische schaling kan alleen worden uitgevoerd als de verzameling van metrische gegevens is voltooid op elke virtuele machine in de schaalset Hallo. Hello Azure-extensie voor diagnostische gegevens levert Hallo controle en diagnostische gegevens die voldoet aan Hallo metrische gegevens verzameling behoeften van Hallo automatisch schalen resource. U kunt Hallo uitbreiding installeren als onderdeel van Hallo Resource Manager-sjabloon.

Dit voorbeeld ziet Hallo variabelen die worden gebruikt in de extensie voor diagnostische gegevens van Hallo sjabloon tooconfigure Hallo:

```json
"diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'saa')]",
"accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/', 'Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
"wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
"wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Thread Count\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
"wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
"wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
"wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
```

Parameters worden opgegeven wanneer Hallo sjabloon wordt geïmplementeerd. In dit voorbeeld Hallo-naam van Hallo storage-account (waar gegevens worden opgeslagen) en Hallo vindt u de naam van Hallo scale set (waarbij gegevens worden verzameld). In dit voorbeeld Windows Server alleen Hallo aantal threads prestatiemeteritem ook verzameld. Alle prestatiemeteritems die beschikbaar in Windows hello of Linux gebruikte toocollect diagnostische gegevens kan worden en kan worden opgenomen in de configuratie van Hallo-uitbreiding.

Dit voorbeeld ziet Hallo definitie van Hallo-uitbreiding in Hallo sjabloon:

```json
"extensionProfile": {
  "extensions": [
    {
      "name": "Microsoft.Insights.VMDiagnosticsSettings",
      "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
          "xmlCfg": "[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
          "storageAccount": "[variables('diagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
          "storageAccountName": "[variables('diagnosticsStorageAccountName')]",
          "storageAccountKey": "[listkeys(variables('accountid'), variables('apiVersion')).key1]",
          "storageAccountEndPoint": "https://core.windows.net"
        }
      }
    }
  ]
}
```

Wanneer Hallo-extensie voor diagnostische gegevens wordt uitgevoerd, wordt dit door Hallo gegevens worden opgeslagen en die worden verzameld in een tabel in Hallo storage-account die u opgeeft. In Hallo **WADPerformanceCounters** tabel vindt u Hallo verzamelde gegevens:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountBefore2.png)

### <a name="configure-hello-autoscalesettings-resource"></a>Hallo autoScaleSettings resource configureren
Hallo autoscaleSettings resource hand Hallo van Hallo diagnostics extensie toodecide of tooincrease of afname Hallo aantal virtuele machines in Hallo scale ingesteld.

In dit voorbeeld ziet u de configuratie Hallo van Hallo resource in Hallo sjabloon:

```json
{
  "type": "Microsoft.Insights/autoscaleSettings",
  "apiVersion": "2015-04-01",
  "name": "[concat(parameters('resourcePrefix'),'as1')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
  ],
  "properties": {
    "enabled": true,
    "name": "[concat(parameters('resourcePrefix'),'as1')]",
    "profiles": [
      {
        "name": "Profile1",
        "capacity": {
          "minimum": "1",
          "maximum": "10",
          "default": "1"
        },
        "rules": [
          {
            "metricTrigger": {
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "GreaterThan",
              "threshold": 650
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
              "metricName": "\\Processor(_Total)\\Thread Count",
              "metricNamespace": "",
              "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
              "timeGrain": "PT1M",
              "statistic": "Average",
              "timeWindow": "PT5M",
              "timeAggregation": "Average",
              "operator": "LessThan",
              "threshold": 550
            },
            "scaleAction": {
              "direction": "Decrease",
              "type": "ChangeCount",
              "value": "1",
              "cooldown": "PT5M"
            }
          }
        ]
      }
    ],
    "targetResourceUri": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
  }
}
```

Hallo bovenstaande voorbeeld worden twee regels voor het definiëren van automatische schaling acties Hallo gemaakt. Hallo eerste regel definieert Hallo scale-out actie en de tweede regel Hallo definieert Hallo schaal in te grijpen. Deze waarden zijn beschikbaar in Hallo regels:

| Regel | Beschrijving |
| ---- | ----------- |
| metricName        | Deze waarde is hetzelfde als Hallo prestatiemeteritem dat u hebt gedefinieerd in Hallo wadperfcounter variabele voor de extensie voor diagnostische gegevens Hallo Hallo. Hallo bovenstaande voorbeeld wordt Hallo aantal threads teller gebruikt.    |
| metricResourceUri | Deze waarde is Hallo resource-id van de virtuele-machineschaalset Hallo weergeven. Deze id bevat Hallo-naam van de resourcegroep hello, Hallo-naam van de resourceprovider Hallo en Hallo-naam van Hallo scale set tooscale. |
| TimeGrain         | Deze waarde is Hallo granulatie van Hallo metrische gegevens die worden verzameld. In de Hallo voorgaande voorbeeld, worden gegevens verzameld tijdens een interval van één minuut. Deze waarde wordt gebruikt met de waarde voor timeWindow. |
| statistiek         | Deze waarde bepaalt hoe Hallo metrische gegevens worden gecombineerd tooaccommodate Hallo automatisch vergroten / verkleinen in te grijpen. Hallo mogelijke waarden zijn: gemiddelde, Min, Max. |
| Waarde voor TimeWindow        | Deze waarde is Hallo tijdbereik waarin de gegevens worden verzameld. Deze moet tussen 5 minuten en 12 uur. |
| TimeAggregation van   | Deze waarde bepaalt hoe Hallo-gegevens die worden verzameld gedurende een bepaalde periode moeten worden gecombineerd. Hallo-standaardwaarde is de gemiddelde. Hallo mogelijke waarden zijn: gemiddeld, Minimum, Maximum, laatste, totaal, Count. |
| Operator          | Deze waarde is Hallo-operator die wordt gebruikt toocompare Hallo metrische gegevens en Hallo drempelwaarde. Hallo mogelijke waarden zijn: gelijk is aan NotEquals, groter dan, GreaterThanOrEqual, LessThan, LessThanOrEqual. |
| Drempelwaarde         | Deze waarde is Hallo-waarde waarmee de schaalactie hello wordt geactiveerd. Worden tooprovide ervoor dat een voldoende verschil tussen de drempelwaarden Hallo voor Hallo **scale-out** en **schaal in** acties. Als u op dezelfde waarden voor beide acties Hallo instelt, verwacht Hallo system constante wijziging, die voorkomt dat het implementeren van een actie vergroten/verkleinen. Bijvoorbeeld, werkt instellen van beide too600 threads in het voorgaande voorbeeld Hallo niet. |
| Richting         | Deze waarde bepaalt Hallo-actie die wordt uitgevoerd wanneer het Hallo-drempelwaarde wordt bereikt. Hallo mogelijke waarden zijn vergroten of verkleinen. |
| type              | Deze waarde is Hallo type actie dat moet worden uitgevoerd en tooChangeCount moet worden ingesteld. |
| waarde             | Deze waarde is het aantal virtuele machines die zijn toegevoegd tooor verwijderd uit Hallo scale set Hallo. Deze waarde moet 1 of hoger. |
| cooldown          | Deze waarde is Hallo hoeveelheid tijd toowait sinds de laatste vergroten/verkleinen actie Hallo voordat de volgende actie Hallo optreedt. Deze waarde moet tussen 1 minuut en één week. |

U gebruikt, afhankelijk van het prestatiemeteritem hello, aantal elementen in de sjabloonconfiguratie Hallo Hallo anders worden gebruikt. In Hallo voorgaande voorbeeld, Hallo prestatiemeteritem is aantal threads, Hallo-drempelwaarde is 650 voor de actie van een scale-out en Hallo-drempelwaarde is 550 voor Hallo schaal in te grijpen. Als u een item, zoals % processortijd gebruikt, is de drempelwaarde Hallo toohello percentage van CPU-verbruik dat een vergroten/verkleinen actie bepaalt ingesteld.

Wanneer een actie vergroten/verkleinen wordt geactiveerd, zoals een hoge belasting Hallo-capaciteit van Hallo is ingesteld op basis van de waarde in de sjabloon Hallo Hallo verhoogd. Stel bijvoorbeeld in een schaal waar Hallo capaciteit too3 is ingesteld en Hallo schaalactiewaarde too1 is ingesteld:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerBefore.png)

Wanneer Hallo huidige load oorzaken Hallo thread gemiddelde aantal toogo boven de drempelwaarde Hallo 650:

![](./media/virtual-machine-scale-sets-autoscale-overview/ThreadCountAfter.png)

Een **scale-out** actie dat oorzaken capaciteit van Hallo set toobe verhoogd met één Hallo wordt geactiveerd:

```json
"sku": {
  "name": "Standard_A0",
  "tier": "Standard",
  "capacity": 4
},
```

Hallo-resultaat is dat een virtuele machine toohello scale set wordt toegevoegd:

![](./media/virtual-machine-scale-sets-autoscale-overview/ResourceExplorerAfter.png)

Nadat een cooldown periode van vijf minuten, als Hallo kunt u het gemiddelde aantal threads op Hallo machines meer dan 600 blijft, is een andere computer toegevoegd toohello set. Hallo gemiddelde aantal threads onder 550 blijft, Hallo-capaciteit van Hallo scale set wordt verminderd door een als een machine wordt verwijderd uit het Hallo-set.

## <a name="set-up-scaling-using-azure-powershell"></a>Instellen van schalen met Azure PowerShell

Voorbeelden van het gebruik van PowerShell tooset up automatisch schalen, toosee kijken [Azure Monitor PowerShell snel starten voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md).

## <a name="set-up-scaling-using-azure-cli"></a>Schalen met Azure CLI instellen

Voorbeelden van het gebruik van Azure CLI tooset up automatisch schalen, toosee kijken [Azure Monitor platformoverschrijdende CLI snel starten voorbeelden](../monitoring-and-diagnostics/insights-cli-samples.md).

## <a name="set-up-scaling-using-hello-azure-portal"></a>Schalen met hello Azure-portal instellen

een voorbeeld van het gebruik van toosee hello Azure portal tooset up automatisch schalen, zoekt u naar op [maken van een virtuele-Machineschaalset hello Azure-portal met](virtual-machine-scale-sets-portal-create.md).

## <a name="investigate-scaling-actions"></a>Schalen acties onderzoeken

* **Azure Portal**  
Momenteel kunt u een beperkte hoeveelheid informatie met Hallo portal ophalen.

* **Azure Resource Explorer**  
Dit hulpprogramma is Hallo aanbevolen voor de huidige status van uw scale set Hallo verkennen. Volg dit pad en ziet u Hallo instantieweergave van de schaal Hallo instellen die u hebt gemaakt:  
**Abonnementen > {uw abonnement} > resourceGroups > {uw resourcegroep} > providers > Microsoft.Compute > virtualMachineScaleSets > {uw schaalset} > virtuele machines**

* **Azure PowerShell**  
Gebruik deze opdracht tooget sommige informatie:

  ```powershell
  Get-AzureRmResource -name vmsstest1 -ResourceGroupName vmsstestrg1 -ResourceType Microsoft.Compute/virtualMachineScaleSets -ApiVersion 2015-06-15
  Get-Autoscalesetting -ResourceGroup rainvmss -DetailedOutput
  ```

* Net zoals u zou een andere machine en klikt u op afstand toegang Hallo virtuele machines in Hallo scale set toomonitor afzonderlijke processen tot, verbinding maken met toohello jumpbox virtuele machine.

## <a name="next-steps"></a>Volgende stappen
* Bekijk [machines automatisch schalen in een virtuele-Machineschaalset](virtual-machine-scale-sets-windows-autoscale.md) toosee een voorbeeld van hoe toocreate een schaalset met automatisch schalen is geconfigureerd.

* Voorbeelden van Azure Monitor bewakingsfuncties in [Azure Monitor PowerShell snel starten-voorbeelden](../monitoring-and-diagnostics/insights-powershell-samples.md)

* Meer informatie over functies in [automatisch schalen acties toosend e-mail en -webhook waarschuwingsmeldingen gebruiken in Azure Monitor](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md).

* Meer informatie over het te[gebruik auditlogboeken toosend e-mail en -webhook waarschuwingsmeldingen in de Azure-Monitor](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)

* Meer informatie over [automatisch schalen ingewikkelde](virtual-machine-scale-sets-advanced-autoscale.md).
