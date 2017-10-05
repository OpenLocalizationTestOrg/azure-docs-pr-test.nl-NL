---
title: Schakel diagnostische gegevens in Azure Cloud Services met behulp van PowerShell | Microsoft Docs
description: Informatie over het inschakelen van diagnostische gegevens voor cloudservices met behulp van PowerShell
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="60b92-103">Diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen</span><span class="sxs-lookup"><span data-stu-id="60b92-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="60b92-104">U kunt diagnostische gegevens, zoals Logboeken, verzamelen prestatiemeteritems enzovoort van een Cloudservice met de extensie Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="60b92-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="60b92-105">In dit artikel wordt beschreven hoe de Azure Diagnostics-extensie inschakelen voor een Cloudservice met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60b92-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="60b92-106">Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) voor de vereisten die nodig zijn voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="60b92-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="60b92-107">De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="60b92-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="60b92-108">Deze aanpak is van toepassing op type continue integratie van scenario's, waarbij de extensie voor diagnostische gegevens kan worden ingeschakeld als onderdeel van de implementatie van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="60b92-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="60b92-109">Bij het maken van een nieuwe Cloudservice-implementatie kunt u de extensie voor diagnostische gegevens inschakelen door door te geven in de *ExtensionConfiguration* -parameter voor de [nieuw AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60b92-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="60b92-110">De *ExtensionConfiguration* parameter neemt een matrix van configuraties voor diagnostische gegevens die kunnen worden gemaakt met de [nieuw AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60b92-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="60b92-111">Het volgende voorbeeld ziet hoe u diagnostische gegevens voor een cloudservice met een WebRole en WorkerRole, elk met de configuratie van een andere diagnostische kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="60b92-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="60b92-112">Als het configuratiebestand van de diagnostische gegevens wordt een `StorageAccount` element met de naam van een opslagaccount, wordt de `New-AzureServiceDiagnosticsExtensionConfig` cmdlet automatisch gebruikmaken van dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="60b92-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="60b92-113">Dit werkt, moet het storage-account zich in hetzelfde abonnement als de Cloud-Service wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="60b92-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="60b92-114">Azure SDK versie 2.6 bewerken publiceren van de extensieconfiguratiebestanden die worden gegenereerd door het MSBuild bevat Doeluitvoer de naam van de opslag op basis van de configuratietekenreeks voor diagnostische gegevens opgegeven in het configuratiebestand (.cscfg) van de service.</span><span class="sxs-lookup"><span data-stu-id="60b92-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="60b92-115">Het onderstaande script laat zien hoe u de configuratiebestanden voor de uitbreiding van de doel-uitvoer publiceren parseren en het configureren van extensie voor diagnostische gegevens voor elke rol bij het implementeren van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="60b92-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="60b92-116">Visual Studio Online maakt gebruik van een soortgelijke benadering voor geautomatiseerde implementaties van Cloud Services met de extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="60b92-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="60b92-117">Zie [publiceren AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) voor een compleet voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="60b92-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="60b92-118">Als er geen `StorageAccount` is opgegeven in de configuratie van diagnostische gegevens, moet u doorgeeft in de *StorageAccountName* parameter aan de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60b92-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="60b92-119">Als de *StorageAccountName* parameter wordt opgegeven, wordt de cmdlet gebruik altijd het opslagaccount dat is opgegeven in de parameter en niet de naam die is opgegeven in het configuratiebestand van de diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="60b92-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="60b92-120">Als het opslagaccount voor diagnostische gegevens in een ander abonnement uit de Cloudservice is, moet u expliciet de *StorageAccountName* en *StorageAccountKey* parameters aan de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60b92-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="60b92-121">De *StorageAccountKey* parameter is niet nodig als het opslagaccount voor diagnostische gegevens in hetzelfde abonnement behoren, aangezien de cmdlet kan automatisch een query en de waarde van de sleutel bij het inschakelen van de extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="60b92-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="60b92-122">Evenwel opgeven als het opslagaccount voor diagnostische gegevens in een ander abonnement en vervolgens de cmdlet mogelijk niet de sleutel automatisch ophalen en u expliciet moet de sleutel via de *StorageAccountKey* parameter.</span><span class="sxs-lookup"><span data-stu-id="60b92-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="60b92-123">De extensie voor diagnostische gegevens inschakelen voor een bestaande cloudservice</span><span class="sxs-lookup"><span data-stu-id="60b92-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="60b92-124">U kunt de [Set AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet inschakelen of werk de configuratie van diagnostische gegevens op een Cloudservice die al wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60b92-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="60b92-125">De huidige configuratie van de extensie voor diagnostische gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="60b92-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="60b92-126">Gebruik de [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet ophalen van de huidige configuratie van diagnostische gegevens voor een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="60b92-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="60b92-127">De extensie voor diagnostische gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="60b92-127">Remove diagnostics extension</span></span>
<span data-ttu-id="60b92-128">Uitschakelen van diagnostische gegevens op een cloudservice kunt u de [verwijderen AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60b92-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="60b92-129">Als u de extensie voor diagnostische gegevens met behulp van ingeschakeld *Set AzureServiceDiagnosticsExtension* of de *nieuw AzureServiceDiagnosticsExtensionConfig* zonder de *rol*u vervolgens een parameter kan de extensie verwijderen met *verwijderen AzureServiceDiagnosticsExtension* zonder de *rol* parameter.</span><span class="sxs-lookup"><span data-stu-id="60b92-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="60b92-130">Als de *rol* parameter is gebruikt bij het inschakelen van de uitbreiding wordt moet ook worden gebruikt bij het verwijderen hiervan.</span><span class="sxs-lookup"><span data-stu-id="60b92-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="60b92-131">De extensie voor diagnostische gegevens verwijderen voor elke afzonderlijke rol:</span><span class="sxs-lookup"><span data-stu-id="60b92-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="60b92-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60b92-132">Next Steps</span></span>
* <span data-ttu-id="60b92-133">Zie voor meer informatie over het gebruik van Azure diagnoses en andere technieken voor het oplossen van problemen [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="60b92-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="60b92-134">De [Diagnostics configuratieschema](https://msdn.microsoft.com/library/azure/dn782207.aspx) worden de verschillende XML-configuraties opties voor de extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="60b92-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="60b92-135">Zie voor meer informatie over het inschakelen van de extensie voor diagnostische gegevens voor virtuele Machines, [een Windows virtuele machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon maken](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="60b92-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
