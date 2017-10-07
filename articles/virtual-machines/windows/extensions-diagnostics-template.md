---
title: aaaAdd bewaking & diagnostics tooan virtuele Azure-machine | Microsoft Docs
description: Gebruik een Azure resource manager-sjabloon toocreate een nieuwe virtuele machine voor Windows met de extensie Azure diagnostics.
services: virtual-machines-windows
documentationcenter: 
author: sbtron
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8cde8fe7-977b-43d2-be74-ad46dc946058
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: saurabh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d8a831421a0f9d38c09d51cf8c2e6dff913c77ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-monitoring-and-diagnostics-with-a-windows-vm-and-azure-resource-manager-templates"></a>Controle en diagnostische gegevens met een virtuele machine van Windows en Azure Resource Manager-sjablonen gebruiken
Hallo extensie voor diagnostische gegevens van Azure biedt Hallo bewaking en mogelijkheden van diagnostische gegevens op een Windows op basis van virtuele machine van Azure. U kunt deze mogelijkheden op Hallo virtuele machine inschakelen door uitbreiding Hallo als onderdeel van hello azure resource manager-sjabloon. Zie [Azure Resource Manager-sjablonen ontwerpen met VM-extensies](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions) voor meer informatie over het toevoegen van elke extensie als onderdeel van een sjabloon voor virtuele machines. Dit artikel wordt beschreven hoe u hello Azure Diagnostics extensie tooa windows virtuele machine-sjabloon kunt toevoegen.  

## <a name="add-hello-azure-diagnostics-extension-toohello-vm-resource-definition"></a>Hello Azure Diagnostics toohello VM resource-uitbreidingsdefinitie toevoegen
tooenable Hallo-extensie voor diagnostische gegevens op een virtuele Windows-Machine moet u tooadd Hallo extensie als een VM-resource in Hallo Resource manager-sjabloon.

Voor een eenvoudige Resource Manager gebaseerde virtuele Machine toevoegen Hallo extensie configuratie toohello *resources* matrix voor Hallo virtuele Machine: 

    "resources": [
                {
                    "name": "Microsoft.Insights.VMDiagnosticsSettings",
                    "type": "extensions",
                    "location": "[resourceGroup().location]",
                    "apiVersion": "2015-06-15",
                    "dependsOn": [
                        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
                    ],
                    "tags": {
                        "displayName": "AzureDiagnostics"
                    },
                    "properties": {
                        "publisher": "Microsoft.Azure.Diagnostics",
                        "type": "IaaSDiagnostics",
                        "typeHandlerVersion": "1.5",
                        "autoUpgradeMinorVersion": true,
                        "settings": {
                            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
                            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
                        },
                        "protectedSettings": {
                            "storageAccountName": "[parameters('existingdiagnosticsStorageAccountName')]",
                            "storageAccountKey": "[listkeys(variables('accountid'), '2015-05-01-preview').key1]",
                            "storageAccountEndPoint": "https://core.windows.net"
                        }
                    }
                }
            ]


Een andere algemene conventie wordt configuratie van de uitbreiding Hallo op Hallo hoofdknooppunt resources van de sjabloon Hallo in plaats van waarin het is gedefinieerd onder hardwarebronnen Hallo virtuele machine toevoegen. Met deze aanpak hebt u tooexplicitly opgeven van een hiërarchische relatie tussen Hallo-extensie en Hallo virtuele machine met Hallo *naam* en *type* waarden. Bijvoorbeeld: 

    "name": "[concat(variables('vmName'),'Microsoft.Insights.VMDiagnosticsSettings')]",
    "type": "Microsoft.Compute/virtualMachines/extensions",

Hallo uitbreiding is altijd Hallo virtuele machine is gekoppeld, kunt u rechtstreeks direct onder het bronknooppunt Hallo virtuele machine definiëren of definiëren op basisniveau Hallo en Hallo hiërarchische naming convention tooassociate gebruiken met virtuele Hallo machine.

Voor virtuele-Machineschaalsets Hallo uitbreidingen configuratie is opgegeven in Hallo *extensionProfile* eigenschap Hallo *VirtualMachineProfile*.

Hallo *publisher* eigenschap met de waarde van Hallo **Microsoft.Azure.Diagnostics** en Hallo *type* eigenschap met de waarde van Hallo **IaaSDiagnostics** hello Azure Diagnostics extensie uniek te identificeren.

waarde van Hallo Hallo *naam* gebruikte toorefer toohello extensie in de resourcegroep Hallo voor de eigenschap zijn. Te specifiek instelling**Microsoft.Insights.VMDiagnosticsSettings** toobe gemakkelijk worden geïdentificeerd door hello Azure portal ervoor te zorgen dat Hallo bewaking grafieken weergegeven correct in hello Azure-portal wordt inschakelen.

Hallo *typeHandlerVersion* Hallo-versie van de uitbreiding Hallo gewenst toouse. Instelling *autoUpgradeMinorVersion* updateversies te**true** zorgt ervoor dat u krijgt Hallo nieuwste secundaire versie van het Hallo-extensie die beschikbaar is. Het is raadzaam dat u altijd ingesteld *autoUpgradeMinorVersion* tooalways worden **true** zodat u altijd toouse Hallo meest recente beschikbare extensie voor diagnostische gegevens met alle Hallo nieuwe functies en oplossingen ophalen corrigeert. 

Hallo *instellingen* element bevat eigenschappen van de configuraties voor Hallo-extensie die kunnen worden ingesteld en kan worden gelezen door Hallo-extensie (soms waarnaar wordt verwezen tooas openbare configuratie). Hallo *xmlcfg* eigenschap bevat op basis van xml-configuratie voor Hallo diagnostische logboeken prestatiemeteritems enzovoort die worden verzameld door Hallo diagnostics agent. Zie [Diagnostics configuratieschema](https://msdn.microsoft.com/library/azure/dn782207.aspx) voor meer informatie over xml-schema voor Hallo zelf. Een gebruikelijk is toostore Hallo werkelijke XML-configuratie als een variabele in hello Azure Resource Manager-sjabloon en vervolgens tekst en base64 ze coderen tooset Hallo waarde voor *xmlcfg*. Zie de sectie Hallo over [diagnostische gegevens van de variabelen](#diagnostics-configuration-variables) toounderstand meer informatie over hoe toostore Hallo xml in variabelen. Hallo *storageAccount* -eigenschap geeft u op het Hallo-naam van Hallo storage account toowhich diagnostics-gegevens worden overgebracht. 

eigenschappen in Hallo *protectedSettings* (soms waarnaar wordt verwezen tooas persoonlijke configuratie) kan worden ingesteld, maar kan niet worden gelezen terug nadat wordt ingesteld. alleen-schrijven aard van Hallo *protectedSettings* is daarom geschikt voor het opslaan van geheimen zoals Hallo opslagaccountsleutel waar Hallo diagnostics-gegevens worden geschreven.    

## <a name="specifying-diagnostics-storage-account-as-parameters"></a>Opslagaccount voor diagnostische gegevens als parameters opgeven
Hallo diagnostics extensie json-codefragment hierboven wordt ervan uitgegaan dat de twee parameters *existingdiagnosticsStorageAccountName* en *existingdiagnosticsStorageResourceGroup* toospecify Hallo diagnostische gegevens opslagaccount waarin de diagnostics-gegevens worden opgeslagen. Opslagaccount voor diagnostische gegevens Hallo opgeven als een parameter het eenvoudig toochange hello opslagaccount voor diagnostische gegevens maakt in verschillende omgevingen zoals u kunt toouse een opslagaccount voor verschillende diagnostische gegevens voor het testen en een andere naam voor uw productie-implementatie.  

        "existingdiagnosticsStorageAccountName": {
            "type": "string",
            "metadata": {
        "description": "hello name of an existing storage account toowhich diagnostics data will be transfered."
            }        
        },
        "existingdiagnosticsStorageResourceGroup": {
            "type": "string",
            "metadata": {
        "description": "hello resource group for hello storage account specified in existingdiagnosticsStorageAccountName"
              }
        }

Het is best practice toospecify een opslagaccount voor diagnostische gegevens in een andere resourcegroep dan Hallo resourcegroep voor Hallo virtuele machine. Een resourcegroep kan worden beschouwd als een implementatie-eenheid met een eigen levensduur toobe, een virtuele machine kan worden geïmplementeerd en geïmplementeerd wanneer er nieuwe updates van de configuraties worden worden aangebracht tooit, maar u kunt toocontinue Hallo diagnostische gegevens opslaan in Hallo hetzelfde opslagaccount Met deze virtuele machine-implementaties. Hallo storage-account dat in een andere resource schakelt Hallo storage account tooaccept gegevens uit verschillende implementaties van virtuele machines zodat u eenvoudig tootroubleshoot Hallo problemen tussen verschillende versies.

> [!NOTE]
> Als u een windows-sjabloon voor virtuele machine maakt vanuit Visual Studio Hallo standaardopslagaccount kan worden ingesteld Hallo toouse hetzelfde opslagaccount waar de VHD Hallo virtuele machine wordt geüpload. Dit is de eerste installatie toosimplify van Hallo VM. U dient opnieuw rekening Hallo sjabloon toouse een ander opslagaccount die kan worden doorgegeven als parameter. 
> 
> 

## <a name="diagnostics-configuration-variables"></a>Variabelen voor de configuratie van diagnostische gegevens
Hallo diagnostics extensie json-codefragment bovenstaande definieert een *accountid* variabele toosimplify Hallo-toegangssleutel voor opslag van Hallo diagnostische gegevens ophalen:   

    "accountid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/',parameters('existingdiagnosticsStorageResourceGroup'), '/providers/','Microsoft.Storage/storageAccounts/', parameters('existingdiagnosticsStorageAccountName'))]"


Hallo *xmlcfg* eigenschap voor Hallo-extensie voor diagnostische gegevens wordt gedefinieerd met meerdere variabelen die worden samengevoegd. Hallo-waarden van deze variabelen zijn in xml daarom ze toobe correct escape-teken moeten bij het instellen van Hallo json-variabelen.

Hallo-hieronder wordt beschreven Hallo diagnostics configuratie-xml die standaard niveau systeemprestatiemeteritems samen met enkele windows-gebeurtenislogboeken en diagnostische gegevens infrastructuur logboeken verzamelt. Het is escape-teken en de juiste indeling zodat hello configuratie kan rechtstreeks worden geplakt in de sectie met sjabloonvariabelen Hallo van uw sjabloon. Zie Hallo [Diagnostics configuratieschema](https://msdn.microsoft.com/library/azure/dn782207.aspx) voor een voorbeeld van een meer menselijke leesbare van Hallo configuratie-xml.

        "wadlogs": "<WadCfg> <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" /></WindowsEventLog>",
        "wadperfcounters1": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Processor Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU utilization\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% Privileged Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU privileged time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor(_Total)\\% User Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU user time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Processor Information(_Total)\\Processor Frequency\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"CPU frequency\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\System\\Processes\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Processes\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Threads\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Handle Count\" sampleRate=\"PT15S\" unit=\"Count\"><annotation displayName=\"Handles\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\% Committed Bytes In Use\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Memory usage\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Available Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory available\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Committed Bytes\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory committed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\Memory\\Commit Limit\" sampleRate=\"PT15S\" unit=\"Bytes\"><annotation displayName=\"Memory commit limit\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active time\" locale=\"en-us\"/></PerformanceCounterConfiguration>",
        "wadperfcounters2": "<PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Read Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active read time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\% Disk Write Time\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk active write time\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Transfers/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Reads/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk read operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Writes/sec\" sampleRate=\"PT15S\" unit=\"CountPerSecond\"><annotation displayName=\"Disk write operations\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Read Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk read speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\PhysicalDisk(_Total)\\Disk Write Bytes/sec\" sampleRate=\"PT15S\" unit=\"BytesPerSecond\"><annotation displayName=\"Disk write speed\" locale=\"en-us\"/></PerformanceCounterConfiguration><PerformanceCounterConfiguration counterSpecifier=\"\\LogicalDisk(_Total)\\% Free Space\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"Disk free space (percentage)\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
        "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters1'), variables('wadperfcounters2'), '<Metrics resourceId=\"')]",
        "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name , '/providers/', 'Microsoft.Compute/virtualMachines/')]",
        "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>"

Hallo metrische gegevens definitie XML-knooppunt in Hallo hierboven configuratie is een belangrijke configuratie-element wordt gedefinieerd hoe Hallo prestatiemeteritems die eerder in xml in Hallo gedefinieerd *PerformanceCounter* knooppunt worden samengevoegd en opgeslagen. 

> [!IMPORTANT]
> Deze metrische gegevens station Hallo bewaking grafieken en waarschuwingen in hello Azure-portal.  Hallo **metrische gegevens** knooppunt Hello *resourceID* en **MetricAggregation** moeten worden opgenomen in de configuratie van diagnostische Hallo voor uw virtuele machine als u wilt dat toosee Hallo VM het bewaken van gegevens in hello Azure-portal. 
> 
> 

Hallo Hieronder volgt een voorbeeld van Hallo xml voor definities van de metrische gegevens: 

        <Metrics resourceId="/subscriptions/subscription().subscriptionId/resourceGroups/resourceGroup().name/providers/Microsoft.Compute/virtualMachines/vmName">
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>

Hallo *resourceID* kenmerk uniek wordt geïdentificeerd Hallo virtuele machine in uw abonnement. Zorg ervoor dat toouse hello subscription() en resourceGroup() functies zodat hello sjabloon automatisch bijgewerkt die waarden op basis van Hallo-groep abonnement en die u implementeert.

Als u meerdere virtuele Machines in een lus maakt hebt u wordt toopopulate hello *resourceID* waarde met een functie copyIndex() toocorrectly onderscheiden elke afzonderlijke virtuele machine. Hallo *xmlCfg* waarde kan worden bijgewerkt toosupport dit als volgt:  

    "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), concat(parameters('vmNamePrefix'), copyindex()), variables('wadcfgxend')))]", 

Hallo MetricAggregation waarde van *PT1H* en *PT1M* geven een aggregatie in een minuut en een aggregatie ruim een uur.

## <a name="wadmetrics-tables-in-storage"></a>WADMetrics tabellen in de opslag
Hallo metrische gegevens configuratie bovenstaande wordt tabellen gegenereerd in uw opslagaccount voor diagnostische gegevens met Hallo volgende naamgevingsregels:

* **WADMetrics** : standaardvoorvoegsel voor alle WADMetrics tabellen
* **PT1H** of **PT1M** : geeft aan dat Hallo-tabel bevat de statistische gegevens meer dan 1 uur of 1 minuut
* **P10D** : geeft aan dat Hallo tabel gegevens bevat voor 10 dagen vanaf wanneer het verzamelen van gegevens van Hallo tabel wordt gestart
* **V2S** : tekenreeksconstante
* **JJJJMMDD** : Hallo datum welke Hallo tabel gestart verzamelen van gegevens

Voorbeeld: *WADMetricsPT1HP10DV2S20151108* bevatten metrische gegevens geaggregeerd ruim een uur tien dagen starten op 11-november-2015    

Elke tabel WADMetrics bevat Hallo kolommen te volgen:

* **PartitionKey**: Hallo partitionkey is samengesteld op basis van Hallo *resourceID* waarde toouniquely identificeren Hallo VM-resource. voor bijvoorbeeld: 002Fsubscriptions:<subscriptionID>: 002FresourceGroups:002F<ResourceGroupName>: 002Fproviders:002FMicrosoft:002ECompute:002FvirtualMachines:002F<vmName>  
* **RowKey** : volgt Hallo indeling <Descending time tick>:<Performance Counter Name>. Hallo aflopende maatstreepjes berekening is maximale tijd ticks min Hallo-tijd van Hallo begin van Hallo aggregatie periode. Bijvoorbeeld Als Hallo voorbeeld periode op november-10-2015 gestart en 00:00Hrs UTC vervolgens Hallo berekening zou zijn: DateTime.MaxValue.Ticks - (nieuwe DateTime(2015,11,10,0,0,0,DateTimeKind.Utc). Tikken). Voor Hallo geheugen beschikbare bytes Hallo rij-sleutel performance teller ziet, zoals: 2519551871999999999__:005CMemory:005CAvailable:0020 Bytes
* **CounterName** : Hallo naam is van het prestatiemeteritem Hallo. Dit komt overeen met Hallo *counterSpecifier* gedefinieerd in Hallo XML-configuratie.
* **Maximale** : maximumwaarde van het prestatiemeteritem Hallo HALLO hallo aggregatie periode.
* **Minimale** : de minimumwaarde van het prestatiemeteritem Hallo HALLO hallo aggregatie periode.
* **Totaal aantal** : Hallo som van alle waarden van het prestatiemeteritem Hallo gerapporteerd over Hallo aggregatie periode.
* **Aantal** : Hallo kunt u het totale aantal waarden die zijn gerapporteerd voor het prestatiemeteritem Hallo.
* **Gemiddelde** : gemiddelde (totaal/aantal)-waarde van het prestatiemeteritem Hallo HALLO hallo aggregatie periode.

## <a name="next-steps"></a>Volgende stappen
* Zie voor een compleet codevoorbeeld sjabloon van een virtuele Windows-computer met de extensie voor diagnostische gegevens [201-vm-bewaking--extensie voor diagnostische gegevens](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-monitoring-diagnostics-extension)   
* Implementeren met behulp Hallo resource manager sjabloon [Azure PowerShell](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [Azure vanaf de opdrachtregel](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Meer informatie over [Azure Resource Manager-sjablonen ontwerpen](../../resource-group-authoring-templates.md)

