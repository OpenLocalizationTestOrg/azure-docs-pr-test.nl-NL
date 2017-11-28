---
title: aaaEnable diagnostische gegevens in Azure Cloud Services met behulp van PowerShell | Microsoft Docs
description: Meer informatie over hoe diagnostische gegevens tooenable voor cloud services met behulp van PowerShell
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
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="cd00b-103">Diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen</span><span class="sxs-lookup"><span data-stu-id="cd00b-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="cd00b-104">U kunt diagnostische gegevens, zoals Logboeken verzamelen, prestatiemeteritems enzovoort vanuit een Cloudservice met hello Azure Diagnostics-extensie.</span><span class="sxs-lookup"><span data-stu-id="cd00b-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="cd00b-105">Dit artikel wordt beschreven hoe tooenable extensie voor diagnostische gegevens van Azure Hallo voor een Cloudservice met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd00b-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="cd00b-106">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor Hallo vereisten die nodig zijn voor dit artikel.</span><span class="sxs-lookup"><span data-stu-id="cd00b-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="cd00b-107">De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="cd00b-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="cd00b-108">Deze aanpak is van toepassing toocontinuous integratie soort scenario's waarbij Hallo diagnostics uitbreiding kan worden ingeschakeld als onderdeel van de implementatie van cloudservice Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd00b-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="cd00b-109">Bij het maken van een nieuwe Cloudservice-implementatie kunt u Hallo-extensie voor diagnostische gegevens inschakelen door door te geven in Hallo *ExtensionConfiguration* parameter toohello [nieuw AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd00b-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="cd00b-110">Hallo *ExtensionConfiguration* parameter neemt een matrix van configuraties voor diagnostische gegevens die kunnen worden gemaakt met de Hallo [nieuw AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd00b-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="cd00b-111">Hallo volgende voorbeeld ziet u hoe u diagnostische gegevens voor een cloudservice met een WebRole en WorkerRole, elk met de configuratie van een andere diagnostische kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cd00b-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="cd00b-112">Als Hallo diagnostische gegevens van het configuratiebestand wordt een `StorageAccount` element met de naam van een account, klikt u vervolgens Hallo `New-AzureServiceDiagnosticsExtensionConfig` cmdlet automatisch gebruikmaken van dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="cd00b-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="cd00b-113">Voor deze toowork Hallo storage-account moet toobe in hetzelfde abonnement Hallo zoals Hallo Cloud Service wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cd00b-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="cd00b-114">Azure SDK versie 2.6 verdere Hallo configuratie extensiebestanden die worden gegenereerd door Hallo MSBuild publiceren bevat Doeluitvoer Hallo opslagaccountnaam op basis van Hallo diagnostics configuratietekenreeks die is opgegeven in het Hallo-service-configuratiebestand (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="cd00b-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="cd00b-115">Hallo script hieronder toont u hoe tooparse Hallo extensieconfiguratiebestanden uit Hallo Doeluitvoer publiceren en extensie voor diagnostische gegevens voor elke rol configureren wanneer Hallo cloudservice wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="cd00b-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="cd00b-116">Visual Studio Online maakt gebruik van een soortgelijke benadering voor geautomatiseerde implementaties van Cloud Services met Hallo-extensie voor diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="cd00b-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="cd00b-117">Zie [publiceren AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) voor een compleet voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="cd00b-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="cd00b-118">Als er geen `StorageAccount` is opgegeven in de configuratie van de diagnostische hello, moet u toopass in Hallo *StorageAccountName* parameter toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd00b-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="cd00b-119">Als hello *StorageAccountName* parameter wordt opgegeven, wordt Hallo cmdlet wordt altijd Hallo-opslagaccount die is opgegeven in de parameter hello gebruiken en niet Hallo die is opgegeven in het configuratiebestand voor Hallo diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="cd00b-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="cd00b-120">Als Hallo diagnostics storage-account in een ander abonnement van Hallo Cloud-Service, is moet u tooexplicitly in Hallo doorgeeft *StorageAccountName* en *StorageAccountKey* parameters toohello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd00b-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="cd00b-121">Hallo *StorageAccountKey* parameter is niet nodig bij Hallo diagnostics storage-account bevindt zich in hetzelfde abonnement Hallo als Hallo cmdlet kunt automatisch een query Hallo sleutelwaarde ingesteld bij het Hallo-extensie voor diagnostische gegevens inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cd00b-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="cd00b-122">Als hello opslagaccount voor diagnostische gegevens is echter in een ander abonnement en vervolgens Hallo cmdlet mogelijk kunnen tooget Hallo sleutel niet automatisch worden en moet u tooexplicitly Hallo sleutel via Hallo opgeven *StorageAccountKey* parameter.</span><span class="sxs-lookup"><span data-stu-id="cd00b-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="cd00b-123">De extensie voor diagnostische gegevens inschakelen voor een bestaande cloudservice</span><span class="sxs-lookup"><span data-stu-id="cd00b-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="cd00b-124">U kunt Hallo [Set AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable of update configuratie van diagnostische gegevens op een Cloudservice die al wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cd00b-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="cd00b-125">De huidige configuratie van de extensie voor diagnostische gegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="cd00b-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="cd00b-126">Gebruik Hallo [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Hallo huidige configuratie van diagnostische voor een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="cd00b-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="cd00b-127">De extensie voor diagnostische gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="cd00b-127">Remove diagnostics extension</span></span>
<span data-ttu-id="cd00b-128">tooturn uitschakelen diagnostische gegevens in een cloud-service dat u kunt Hallo [verwijderen AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd00b-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="cd00b-129">Als u Hallo extensie voor diagnostische gegevens met behulp van ingeschakeld *Set AzureServiceDiagnosticsExtension* of Hallo *nieuw AzureServiceDiagnosticsExtensionConfig* zonder Hallo *rol* parameter en u kunt verwijderen Hallo met behulp van de extensie *verwijderen AzureServiceDiagnosticsExtension* zonder Hallo *rol* parameter.</span><span class="sxs-lookup"><span data-stu-id="cd00b-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="cd00b-130">Als hello *rol* parameter is gebruikt bij het inschakelen en vervolgens het Hallo-uitbreiding moet ook worden gebruikt bij het verwijderen van Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="cd00b-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="cd00b-131">tooremove hello extensie voor diagnostische gegevens van elke afzonderlijke rol:</span><span class="sxs-lookup"><span data-stu-id="cd00b-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="cd00b-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd00b-132">Next Steps</span></span>
* <span data-ttu-id="cd00b-133">Zie voor meer informatie over het gebruik van Azure diagnostics- en andere technieken tootroubleshoot problemen [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="cd00b-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="cd00b-134">Hallo [Diagnostics configuratieschema](https://msdn.microsoft.com/library/azure/dn782207.aspx) Hallo verschillende configuraties van de XML-opties voor Hallo-extensie voor diagnostische gegevens wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="cd00b-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="cd00b-135">hoe tooenable Hallo-extensie voor diagnostische gegevens voor virtuele Machines, Zie toolearn [een Windows virtuele machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon maken](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="cd00b-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
