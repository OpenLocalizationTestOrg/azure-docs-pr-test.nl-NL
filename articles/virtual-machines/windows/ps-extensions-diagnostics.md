---
title: Azure PowerShell gebruiken voor diagnostische gegevens op een virtuele machine van Windows inschakelen | Microsoft Docs
services: virtual-machines-windows
documentationcenter: 
description: Informatie over het gebruik van PowerShell voor het inschakelen van Azure Diagnostics in een virtuele machine met Windows
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
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="2bb92-103">PowerShell gebruiken voor het inschakelen van Azure Diagnostics in een virtuele machine met Windows</span><span class="sxs-lookup"><span data-stu-id="2bb92-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="2bb92-104">Azure Diagnostics is de functie binnen Azure waarmee het verzamelen van diagnostische gegevens op een geïmplementeerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="2bb92-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="2bb92-105">U kunt de extensie voor diagnostische gegevens gebruiken voor het verzamelen van diagnostische gegevens, zoals toepassingslogboeken of prestatiemeteritems van een Azure virtuele machine (VM) waarop Windows wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2bb92-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="2bb92-106">In dit artikel wordt beschreven hoe u Windows PowerShell gebruikt voor het inschakelen van de extensie voor diagnostische gegevens voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2bb92-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="2bb92-107">Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) voor de vereisten die nodig zijn voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="2bb92-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="2bb92-108">De extensie voor diagnostische gegevens inschakelen als u het implementatiemodel van Resource Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="2bb92-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="2bb92-109">Bij het maken van een virtuele Windows-machine via het Azure Resource Manager-implementatiemodel door de configuratie voor de uitbreiding aan de Resource Manager-sjabloon toe te voegen, kunt u de extensie voor diagnostische gegevens inschakelen.</span><span class="sxs-lookup"><span data-stu-id="2bb92-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="2bb92-110">Zie [virtuele Windows-machine maken met controle en diagnostische gegevens met behulp van de Azure Resource Manager-sjabloon](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2bb92-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="2bb92-111">Als u wilt dat de extensie voor diagnostische gegevens op een bestaande virtuele machine die is gemaakt via het implementatiemodel van Resource Manager, kunt u de [Set AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell-cmdlet, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2bb92-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="2bb92-112">*$diagnosticsconfig_path* is het pad naar het bestand met de configuratie van de diagnostische gegevens in XML, zoals beschreven in de [voorbeeld](#sample-diagnostics-configuration) hieronder.</span><span class="sxs-lookup"><span data-stu-id="2bb92-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="2bb92-113">Als het configuratiebestand van de diagnostische gegevens wordt een **StorageAccount** element met de naam van een opslagaccount, wordt de *Set AzureRMVMDiagnosticsExtension* script stelt automatisch de diagnostics-extensie voor diagnostische gegevens verzenden naar dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="2bb92-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="2bb92-114">Dit werkt, moet het opslagaccount zich in hetzelfde abonnement als de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2bb92-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="2bb92-115">Als er geen **StorageAccount** is opgegeven in de configuratie van diagnostische gegevens, moet u doorgeeft in de *StorageAccountName* parameter aan de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bb92-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="2bb92-116">Als de *StorageAccountName* parameter wordt opgegeven, wordt de cmdlet gebruik altijd het opslagaccount dat is opgegeven in de parameter en niet de naam die is opgegeven in het configuratiebestand van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2bb92-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="2bb92-117">Als het opslagaccount voor diagnostische gegevens zich in een ander abonnement van de virtuele machine, moet u expliciet de *StorageAccountName* en *StorageAccountKey* parameters aan de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bb92-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="2bb92-118">De *StorageAccountKey* parameter is niet nodig als het opslagaccount voor diagnostische gegevens in hetzelfde abonnement behoren, aangezien de cmdlet kan automatisch een query en de waarde van de sleutel bij het inschakelen van de extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2bb92-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="2bb92-119">Evenwel opgeven als het opslagaccount voor diagnostische gegevens in een ander abonnement en vervolgens de cmdlet mogelijk niet de sleutel automatisch ophalen en u expliciet moet de sleutel via de *StorageAccountKey* parameter.</span><span class="sxs-lookup"><span data-stu-id="2bb92-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="2bb92-120">Wanneer de extensie voor diagnostische gegevens op een virtuele machine is ingeschakeld, kunt u de huidige instellingen met behulp van de [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bb92-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="2bb92-121">De cmdlet retourneert *PublicSettings*, die de configuratie van diagnostische gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="2bb92-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="2bb92-122">Er zijn twee soorten configuratie wordt ondersteund, WadCfg en xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="2bb92-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="2bb92-123">WadCfg configuratie uit JSON en xmlCfg XML-configuratie in een Base64-gecodeerde indeling.</span><span class="sxs-lookup"><span data-stu-id="2bb92-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="2bb92-124">Als u wilt lezen van het XML-bestand, moet u dit decoderen.</span><span class="sxs-lookup"><span data-stu-id="2bb92-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="2bb92-125">De [verwijderen AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet kan de extensie voor diagnostische gegevens verwijderen uit de virtuele machine worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2bb92-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="2bb92-126">De extensie voor diagnostische gegevens inschakelen als u het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="2bb92-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="2bb92-127">U kunt de [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet om in te schakelen van een extensie voor diagnostische gegevens op een virtuele machine die u via het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="2bb92-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="2bb92-128">Het volgende voorbeeld laat zien hoe een nieuwe virtuele machine via het klassieke implementatiemodel maken met de extensie voor diagnostische gegevens ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2bb92-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="2bb92-129">Als u wilt dat de extensie voor diagnostische gegevens op een bestaande virtuele machine die is gemaakt via het klassieke implementatiemodel, voor het eerst gebruiken de [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet ophalen van de VM-configuratie.</span><span class="sxs-lookup"><span data-stu-id="2bb92-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="2bb92-130">Werk vervolgens het VM-configuratie zodanig dat de extensie voor diagnostische gegevens met behulp van de [Set AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2bb92-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="2bb92-131">Ten slotte de bijgewerkte configuratie van toepassing op de virtuele machine met behulp van [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="2bb92-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="2bb92-132">In de configuratie van diagnostische gegevens</span><span class="sxs-lookup"><span data-stu-id="2bb92-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="2bb92-133">De volgende XML-code kan worden gebruikt voor de openbare configuratie van diagnostische gegevens met de bovenstaande scripts.</span><span class="sxs-lookup"><span data-stu-id="2bb92-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="2bb92-134">De voorbeeldconfiguratie van dit wordt verschillende prestatiemeteritems overbrengen naar het opslagaccount voor diagnostische gegevens, samen met fouten van de toepassings-, beveiligings- en systeemkanalen in de Windows-gebeurtenislogboeken en fouten van de infrastructuur diagnostische logboeken.</span><span class="sxs-lookup"><span data-stu-id="2bb92-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="2bb92-135">De configuratie moet worden bijgewerkt met het volgende:</span><span class="sxs-lookup"><span data-stu-id="2bb92-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="2bb92-136">De *resourceID* kenmerk van de **metrische gegevens** element moet worden bijgewerkt met de bron-ID voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2bb92-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="2bb92-137">De resource-ID kan worden samengesteld met behulp van het volgende patroon volgen: "/ subscriptions / {*abonnements-ID voor het abonnement met de virtuele machine*} /resourceGroups/ {*resourcegroup-naam voor de virtuele machine*} / providers/Microsoft.Compute/virtualMachines/ {*naam van de VM*} '.</span><span class="sxs-lookup"><span data-stu-id="2bb92-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="2bb92-138">Bijvoorbeeld, als het abonnement-ID voor het abonnement waarop de virtuele machine wordt uitgevoerd is **11111111-1111-1111-1111-111111111111**, de naam van de resourcegroep voor de resourcegroep is **MyResourceGroup**, en de naam van de VM is **MyWindowsVM**, moet u de waarde voor *resourceID* zou zijn:</span><span class="sxs-lookup"><span data-stu-id="2bb92-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="2bb92-139">Voor meer informatie over de metrische gegevens worden gegenereerd op basis van de configuratie van de prestaties tellers en metrische gegevens, Zie [Azure Diagnostics metrische gegevens tabel in de opslag](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="2bb92-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="2bb92-140">De **StorageAccount** element moet worden bijgewerkt met de naam van het opslagaccount voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2bb92-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
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
        <Metrics resourceId="(Update with resource ID for the VM)" >
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

## <a name="next-steps"></a><span data-ttu-id="2bb92-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2bb92-141">Next steps</span></span>
* <span data-ttu-id="2bb92-142">Zie voor meer informatie over het gebruik van de mogelijkheid Azure Diagnostics- en andere technieken voor het oplossen van problemen [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="2bb92-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="2bb92-143">[Diagnostische gegevens configuraties schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) worden de verschillende XML-configuraties opties voor de extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="2bb92-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

