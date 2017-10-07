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
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Diagnostische gegevens in Azure Cloud Services met behulp van PowerShell inschakelen
U kunt diagnostische gegevens, zoals Logboeken verzamelen, prestatiemeteritems enzovoort vanuit een Cloudservice met hello Azure Diagnostics-extensie. Dit artikel wordt beschreven hoe tooenable extensie voor diagnostische gegevens van Azure Hallo voor een Cloudservice met behulp van PowerShell.  Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor Hallo vereisten die nodig zijn voor dit artikel.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>De extensie voor diagnostische gegevens inschakelen als onderdeel van het implementeren van een cloudservice
Deze aanpak is van toepassing toocontinuous integratie soort scenario's waarbij Hallo diagnostics uitbreiding kan worden ingeschakeld als onderdeel van de implementatie van cloudservice Hallo. Bij het maken van een nieuwe Cloudservice-implementatie kunt u Hallo-extensie voor diagnostische gegevens inschakelen door door te geven in Hallo *ExtensionConfiguration* parameter toohello [nieuw AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet. Hallo *ExtensionConfiguration* parameter neemt een matrix van configuraties voor diagnostische gegevens die kunnen worden gemaakt met de Hallo [nieuw AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.

Hallo volgende voorbeeld ziet u hoe u diagnostische gegevens voor een cloudservice met een WebRole en WorkerRole, elk met de configuratie van een andere diagnostische kunt inschakelen.

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

Als Hallo diagnostische gegevens van het configuratiebestand wordt een `StorageAccount` element met de naam van een account, klikt u vervolgens Hallo `New-AzureServiceDiagnosticsExtensionConfig` cmdlet automatisch gebruikmaken van dit opslagaccount. Voor deze toowork Hallo storage-account moet toobe in hetzelfde abonnement Hallo zoals Hallo Cloud Service wordt geïmplementeerd.

Azure SDK versie 2.6 verdere Hallo configuratie extensiebestanden die worden gegenereerd door Hallo MSBuild publiceren bevat Doeluitvoer Hallo opslagaccountnaam op basis van Hallo diagnostics configuratietekenreeks die is opgegeven in het Hallo-service-configuratiebestand (.cscfg). Hallo script hieronder toont u hoe tooparse Hallo extensieconfiguratiebestanden uit Hallo Doeluitvoer publiceren en extensie voor diagnostische gegevens voor elke rol configureren wanneer Hallo cloudservice wordt geïmplementeerd.

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

Visual Studio Online maakt gebruik van een soortgelijke benadering voor geautomatiseerde implementaties van Cloud Services met Hallo-extensie voor diagnostische gegevens. Zie [publiceren AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) voor een compleet voorbeeld.

Als er geen `StorageAccount` is opgegeven in de configuratie van de diagnostische hello, moet u toopass in Hallo *StorageAccountName* parameter toohello cmdlet. Als hello *StorageAccountName* parameter wordt opgegeven, wordt Hallo cmdlet wordt altijd Hallo-opslagaccount die is opgegeven in de parameter hello gebruiken en niet Hallo die is opgegeven in het configuratiebestand voor Hallo diagnostische gegevens.

Als Hallo diagnostics storage-account in een ander abonnement van Hallo Cloud-Service, is moet u tooexplicitly in Hallo doorgeeft *StorageAccountName* en *StorageAccountKey* parameters toohello cmdlet. Hallo *StorageAccountKey* parameter is niet nodig bij Hallo diagnostics storage-account bevindt zich in hetzelfde abonnement Hallo als Hallo cmdlet kunt automatisch een query Hallo sleutelwaarde ingesteld bij het Hallo-extensie voor diagnostische gegevens inschakelen. Als hello opslagaccount voor diagnostische gegevens is echter in een ander abonnement en vervolgens Hallo cmdlet mogelijk kunnen tooget Hallo sleutel niet automatisch worden en moet u tooexplicitly Hallo sleutel via Hallo opgeven *StorageAccountKey* parameter.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>De extensie voor diagnostische gegevens inschakelen voor een bestaande cloudservice
U kunt Hallo [Set AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable of update configuratie van diagnostische gegevens op een Cloudservice die al wordt uitgevoerd.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>De huidige configuratie van de extensie voor diagnostische gegevens ophalen
Gebruik Hallo [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget Hallo huidige configuratie van diagnostische voor een cloudservice.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>De extensie voor diagnostische gegevens verwijderen
tooturn uitschakelen diagnostische gegevens in een cloud-service dat u kunt Hallo [verwijderen AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Als u Hallo extensie voor diagnostische gegevens met behulp van ingeschakeld *Set AzureServiceDiagnosticsExtension* of Hallo *nieuw AzureServiceDiagnosticsExtensionConfig* zonder Hallo *rol* parameter en u kunt verwijderen Hallo met behulp van de extensie *verwijderen AzureServiceDiagnosticsExtension* zonder Hallo *rol* parameter. Als hello *rol* parameter is gebruikt bij het inschakelen en vervolgens het Hallo-uitbreiding moet ook worden gebruikt bij het verwijderen van Hallo-extensie.

tooremove hello extensie voor diagnostische gegevens van elke afzonderlijke rol:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het gebruik van Azure diagnostics- en andere technieken tootroubleshoot problemen [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](cloud-services-dotnet-diagnostics.md).
* Hallo [Diagnostics configuratieschema](https://msdn.microsoft.com/library/azure/dn782207.aspx) Hallo verschillende configuraties van de XML-opties voor Hallo-extensie voor diagnostische gegevens wordt uitgelegd.
* hoe tooenable Hallo-extensie voor diagnostische gegevens voor virtuele Machines, Zie toolearn [een Windows virtuele machine met de controle en diagnostische gegevens met Azure Resource Manager-sjabloon maken](../virtual-machines/windows/extensions-diagnostics-template.md)
