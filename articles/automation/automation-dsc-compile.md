---
title: aaaCompiling configuraties in Azure Automation DSC | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocompile Desired State Configuration (DSC) configuraties voor Azure Automation.
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Compileren van configuraties in Azure Automation DSC

U kunt configuraties Desired State Configuration (DSC) op twee manieren met Azure Automation compileren: in hello Azure-portal en met Windows PowerShell. Hallo onderstaande tabel kunt u bepalen wanneer toouse welke methode op basis van kenmerken van elk Hallo:

### <a name="azure-portal"></a>Azure Portal

* Eenvoudigste methode met interactieve gebruikersinterface
* Formulier tooprovide eenvoudige parameterwaarden
* Eenvoudig bijhouden taakstatus
* Toegang met aanmelding bij Azure is geverifieerd

### <a name="windows-powershell"></a>Windows Powershell

* Aanroepen vanuit de opdrachtregel met Windows PowerShell-cmdlets
* Kan worden opgenomen in een geautomatiseerde oplossing met meerdere stappen
* Eenvoudige en complexe parameterwaarden opgeven
* Taakstatus bijhouden
* Client vereist toosupport PowerShell-cmdlets
* ConfigurationData doorgeven
* Configuraties die gebruikmaken van referenties compileren

Zodra u hebt besloten een compilatie-methode, kunt u onderstaande toostart compileren respectieve procedures Hallo volgen.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>Compileren van een DSC-configuratie met hello Azure-portal

1. Van uw Automation-account, klikt u op **DSC-configuraties**.
2. Klik op een tooopen configuratie van de blade.
3. Klik op **compileren**.
4. Als het Hallo-configuratie geen parameters heeft, worden na vragen aan gebruiker tooconfirm of u toocompile wilt deze. Als Hallo configuratie parameters heeft, Hallo **configuratie compileren** blade geopend zodat u parameterwaarden kan opgeven. Zie Hallo [ **fundamentele Parameters** ](#basic-parameters) sectie hieronder voor meer informatie over parameters.
5. Hallo **Compilatietaak** blade wordt geopend zodat u de status van taak Hallo-compilatie volgen kunt en hello knooppuntconfiguraties (MOF configuratiedocumenten) het veroorzaakt toobe op Hallo Azure Automation DSC-Pull-Server geplaatst.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>Compileren van een DSC-configuratie met Windows PowerShell

U kunt [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart compileren met Windows PowerShell. Hallo volgende voorbeeldcode wordt gestart compilatie van een DSC-configuratie aangeroepen **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`retourneert een compilatie taak object waarmee u tootrack de status ervan kunt. U kunt dit object compilatie met [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine Hallo status van Hallo-Compilatietaak en [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview de streams (uitvoer). Hallo volgende voorbeeldcode wordt gestart compilatie van Hallo **SampleConfig** configuratie, wacht totdat deze is voltooid en wordt vervolgens de stromen.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Basic-Parameters
Parameterdeclaratie in DSC-configuraties, inclusief parametertypen en eigenschappen werkt Hallo hetzelfde als in Azure Automation-runbooks. Zie [een runbook starten in Azure Automation](automation-starting-a-runbook.md) toolearn meer informatie over runbook-parameters.

Hallo volgende voorbeeld worden twee parameters aangeroepen **FeatureName** en **IsPresent**, toodetermine Hallo waarden van eigenschappen in Hallo **ParametersExample.sample** knooppunt configuratie gegenereerd tijdens de compilatie.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

U kunt compileren DSC-configuraties die gebruikmaken van eenvoudige parameters in hello Azure Automation DSC-portal of met Azure PowerShell:

### <a name="portal"></a>Portal

In Hallo-portal, kunt u parameterwaarden opgeven wanneer u op **compileren**.

![alternatieve tekst](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell-parameters in vereist een [hashtabel](http://technet.microsoft.com/library/hh847780.aspx) Hallo-sleutel komt overeen met de parameternaam Hallo waarbij Hallo-waarde is gelijk aan Hallo parameterwaarde.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

Zie voor meer informatie over PSCredentials doorgeeft als parameters <a href="#credential-assets"> **Referentieassets** </a> hieronder.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** kunt u tooseparate structurele configuratie uit een specifieke configuratie van de omgeving tijdens het gebruik van PowerShell DSC. Zie [scheiden 'Wat' op 'Waar' in PowerShell DSC](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn meer informatie over **ConfigurationData**.

> [!NOTE]
> U kunt **ConfigurationData** bij het compileren van in Azure Automation DSC met Azure PowerShell, maar niet in hello Azure-portal.

Hallo volgende DSC-voorbeeldconfiguratie gebruikt **ConfigurationData** via Hallo **$ConfigurationData** en **$AllNodes** trefwoorden. U moet ook Hallo [ **xWebAdministration** module](https://www.powershellgallery.com/packages/xWebAdministration/) voor dit voorbeeld:

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

U kunt compileren Hallo DSC-configuratie hierboven met PowerShell. Hallo onderstaande PowerShell voegt twee knooppunt configuraties toohello Azure Automation DSC-Pull-Server: **ConfigurationDataSample.MyVM1** en **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Assets

Asset-verwijzingen zijn hetzelfde in Azure Automation DSC-configuraties en runbooks Hallo. Zie de volgende Hallo voor meer informatie:

* [Certificaten](automation-certificates.md)
* [Verbindingen](automation-connections.md)
* [Referenties](automation-credentials.md)
* [Variabelen](automation-variables.md)

### <a name="credential-assets"></a>Referentieassets

Terwijl in Azure Automation DSC-configuraties kunnen verwijzen naar referentieassets met **Get-AzureRmAutomationCredential**, referentieassets kunnen ook worden doorgegeven via parameters, indien gewenst. Als een parameter van het duurt een configuratie voordat **PSCredential** typt, moet u toopass Hallo-naam van een Azure Automation-referentieasset als waarde van de parameter in plaats van een PSCredential-object. Achter de schermen hello, wordt hello Azure Automation-referentieasset met die naam opgehaald en doorgegeven toohello configuratie.

Referenties houden vereist beveiligd in knooppuntconfiguraties (MOF configuratiedocumenten) versleutelen Hallo-referenties in Hallo knooppunt configuratie MOF-bestand. Azure Automation wordt hierbij nog een stapje verder en versleutelt Hallo volledige MOF-bestand. Echter, momenteel u moet de hoogte PowerShell DSC dit klopt voor referenties toobe output als tekst zonder opmaak tijdens het genereren van het knooppunt configuratie MOF omdat PowerShell DSC niet weet dat Azure Automation Hallo volledige MOF-bestand na wordt versleutelen de het genereren via een Compilatietaak.

U kunt PowerShell DSC zien of dit voor referenties toobe output in tekst zonder opmaak in Hallo gegenereerd knooppuntconfiguratie MOF-bestanden klopt met [ **ConfigurationData**](#configurationdata). U moet doorgeven `PSDscAllowPlainTextPassword = $true` via **ConfigurationData** voor elk knooppunt-blok-naam die wordt weergegeven in Hallo DSC-configuratie en de referenties worden gebruikt.

Hallo volgende voorbeeld ziet u een DSC-configuratie die gebruikmaakt van een Automation-referentieasset.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

U kunt compileren Hallo DSC-configuratie hierboven met PowerShell. Hallo onderstaande PowerShell voegt twee knooppunt configuraties toohello Azure Automation DSC-Pull-Server: **CredentialSample.MyVM1** en **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Knooppuntconfiguraties importeren

U kunt ook knooppunt configuratons (MOF-bestanden) die u hebt gecompileerd buiten Azure importeren. Een voordeel hiervan is dat confiturations knooppunt kan worden ondertekend.
Een ondertekende knooppuntconfiguratie is lokaal op een beheerde knooppunt gecontroleerd door Hallo DSC-agent, waarbij u ervoor zorgt dat Hallo toegepaste toohello knooppunt wordt de configuratie van een gemachtigde bron afkomstig is.

> [!NOTE]
> U kunt importeren gebruiken configuraties in uw Azure Automation-account is ondertekend, maar Azure Automation biedt momenteel geen ondersteuning voor het compileren van ondertekende configuraties.

> [!NOTE]
> Een configuratiebestand knooppunt is mag niet groter zijn dan 1 MB tooallow het toobe geïmporteerd in Azure Automation.

U leert hoe toosign knooppuntconfiguraties op https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Importeren van de knooppuntconfiguratie van een in hello Azure-portal

1. Van uw Automation-account, klikt u op **DSC-knooppuntconfiguraties**.

    ![DSC-knooppuntconfiguraties](./media/automation-dsc-compile/node-config.png)
2. In Hallo **DSC-knooppuntconfiguraties** blade, klikt u op **toevoegen van een NodeConfiguration**.
3. In Hallo **importeren** blade, klikt u op Hallo map pictogram volgende toohello **configuratiebestand knooppunt** textbox toobrowse voor een knooppunt-configuratiebestand (MOF) op de lokale computer.

    ![Zoeken naar een lokaal bestand](./media/automation-dsc-compile/import-browse.png)
4. Voer een naam in Hallo **configuratienaam** textbox. Deze naam moet overeenkomen met de naam van de Hallo van Hallo-configuratie waaruit Hallo knooppuntconfiguratie is gecompileerd.
5. Klik op **OK**.

### <a name="importing-a-node-configuration-with-powershell"></a>Importeren van de configuratie van een knooppunt met PowerShell

U kunt Hallo [importeren AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport een knooppuntconfiguratie in uw automation-account.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



