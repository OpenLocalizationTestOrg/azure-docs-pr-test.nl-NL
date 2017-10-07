---
title: aaaUse Azure PowerShell tooenable diagnostische gegevens op een virtuele machine van Windows | Microsoft Docs
services: virtual-machines-windows
documentationcenter: 
description: Meer informatie over hoe toouse tooenable diagnostische Azure-gegevens in een virtuele machine met Windows PowerShell
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Gebruik PowerShell tooenable Azure Diagnostics in een virtuele machine met Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Azure Diagnostics is de functie Hallo binnen Azure waarmee Hallo verzamelen van diagnostische gegevens op een geïmplementeerde toepassing. U kunt Hallo diagnostics extensie toocollect diagnostische gegevens, zoals toepassingslogboeken of prestatiemeteritems van een Azure virtuele machine (VM) waarop Windows wordt uitgevoerd. Dit artikel wordt beschreven hoe Windows PowerShell-tooenable toouse extensie voor diagnostische gegevens Hallo voor een virtuele machine. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor Hallo vereisten die nodig zijn voor dit artikel.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Hallo-extensie voor diagnostische gegevens inschakelen als u Hallo Resource Manager-implementatiemodel
U kunt Hallo-extensie voor diagnostische gegevens inschakelen bij het maken van een Windows-VM via hello Azure Resource Manager-implementatiemodel door Hallo extensie configuratie toohello Resource Manager-sjabloon toe te voegen. Zie [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van Azure Resource Manager-sjabloon Hallo](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

tooenable hello extensie voor diagnostische gegevens op een bestaande virtuele machine die is gemaakt via Hallo Resource Manager-implementatiemodel, kunt u Hallo [Set AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell-cmdlet, zoals hieronder wordt weergegeven.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* is Hallo pad toohello-bestand met de configuratie van diagnostische Hallo in XML, zoals beschreven in Hallo [voorbeeld](#sample-diagnostics-configuration) hieronder.  

Als Hallo diagnostische gegevens van het configuratiebestand wordt een **StorageAccount** element met de naam van een account, klikt u vervolgens Hallo *Set AzureRMVMDiagnosticsExtension* script wordt automatisch ingesteld Hallo extensie toosend diagnostische gegevens toothat opslagaccount voor diagnostische gegevens. Voor deze toowork Hallo storage-account moet toobe in hetzelfde abonnement Hallo zoals Hallo VM.

Als er geen **StorageAccount** is opgegeven in de configuratie van de diagnostische hello, moet u toopass in Hallo *StorageAccountName* parameter toohello cmdlet. Als hello *StorageAccountName* parameter wordt opgegeven, wordt Hallo cmdlet wordt altijd Hallo-opslagaccount die is opgegeven in de parameter hello gebruiken en niet Hallo die is opgegeven in het configuratiebestand voor Hallo diagnostische gegevens.

Als Hallo diagnostics storage-account in een ander abonnement van Hallo virtuele machine, is moet u tooexplicitly in Hallo doorgeeft *StorageAccountName* en *StorageAccountKey* parameters toohello cmdlet. Hallo *StorageAccountKey* parameter is niet nodig bij Hallo diagnostics storage-account bevindt zich in hetzelfde abonnement Hallo als Hallo cmdlet kunt automatisch een query Hallo sleutelwaarde ingesteld bij het Hallo-extensie voor diagnostische gegevens inschakelen. Als hello opslagaccount voor diagnostische gegevens is echter in een ander abonnement en vervolgens Hallo cmdlet mogelijk kunnen tooget Hallo sleutel niet automatisch worden en moet u tooexplicitly Hallo sleutel via Hallo opgeven *StorageAccountKey* parameter.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Zodra Hallo-extensie voor diagnostische gegevens op een virtuele machine is ingeschakeld, kunt u de huidige instellingen Hallo verkrijgen door middel van Hallo [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Hallo cmdlet retourneert *PublicSettings*, die de configuratie van diagnostische Hallo bevat. Er zijn twee soorten configuratie wordt ondersteund, WadCfg en xmlCfg. WadCfg configuratie uit JSON en xmlCfg XML-configuratie in een Base64-gecodeerde indeling. tooread Hallo XML, moet u toodecode deze.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Hallo [verwijderen AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet gebruikte tooremove Hallo-extensie voor diagnostische gegevens van Hallo VM kan worden.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Hallo-extensie voor diagnostische gegevens inschakelen als u het klassieke implementatiemodel hello gebruiken
U kunt Hallo [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable een extensie voor diagnostische gegevens op een virtuele machine die u via de klassieke implementatiemodel Hallo. Hallo volgende voorbeeld ziet u hoe toocreate een nieuwe virtuele machine via de klassieke implementatiemodel Hallo met Hallo-extensie voor diagnostische gegevens ingeschakeld.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

tooenable Hallo-extensie voor diagnostische gegevens op een bestaande virtuele machine die is gemaakt via Hallo klassieke implementatiemodel, eerste gebruik Hallo [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget Hallo VM-configuratie. Hallo VM-configuratie tooinclude Hallo diagnostics extensie vervolgens bijwerken met behulp van Hallo [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet. Ten slotte Hallo bijgewerkt configuratie toohello VM toepassen met behulp van [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>In de configuratie van diagnostische gegevens
Hallo die volgende XML-code kan worden gebruikt voor de openbare configuratie van Hallo diagnostische Hello hierboven scripts. De voorbeeldconfiguratie van dit wordt verschillende prestaties tellers toohello opslagaccount voor diagnostische gegevens, samen met fouten van toepassing hello, beveiliging en systeemkanalen in Hallo Windows-gebeurtenislogboeken en eventuele fouten overbrengen van Hallo diagnostische gegevens de logboeken van de infrastructuur.

Hallo-configuratie heeft toobe bijgewerkte tooinclude Hallo volgende nodig:

* Hallo *resourceID* kenmerk Hallo **metrische gegevens** element moet toobe bijgewerkt met de Hallo resource-ID voor Hallo VM.
  
  * Hallo resource-ID kan worden samengesteld met behulp van Hallo patroon volgen: "/ subscriptions / {*abonnements-ID voor Hallo abonnement Hello VM*} /resourceGroups/ {*Hallo resourcegroup-naam voor Hallo VM*} / providers/Microsoft.Compute/virtualMachines/ {*Hallo VM-naam*} '.
  * Bijvoorbeeld, als hello abonnements-ID voor Hallo abonnement waarbij hello VM wordt uitgevoerd, is **11111111-1111-1111-1111-111111111111**, Hallo Resourcegroepnaam voor de resourcegroep hello wordt **MyResourceGroup**, en hello VM-naam is **MyWindowsVM**, vervolgens Hallo waarde voor *resourceID* zou zijn:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Zie voor meer informatie over de wijze waarop metrische gegevens gegenereerd op basis van Hallo prestatiemeteritems en configuratie van de metrische gegevens [Azure Diagnostics metrische gegevens tabel in de opslag](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Hallo **StorageAccount** element moet toobe bijgewerkt met de naam van het opslagaccount voor diagnostische gegevens Hallo Hallo.
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het gebruik van hello Azure Diagnostics functionaliteit en andere technieken tootroubleshoot problemen [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Diagnostische gegevens configuraties schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) Hallo verschillende configuraties van de XML-opties voor Hallo-extensie voor diagnostische gegevens wordt uitgelegd.

