---
title: aaaVariable activa in Azure Automation | Microsoft Docs
description: Variabele assets zijn waarden die beschikbaar tooall runbooks en in Azure Automation DSC-configuraties zijn.  Dit artikel wordt uitgelegd Hallo details van de variabelen en hoe toowork ermee in tekstvorm en grafisch ontwerpen.
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Variabele assets in Azure Automation

Variabele assets zijn waarden die beschikbaar tooall runbooks en DSC-configuraties in uw automation-account zijn. Ze kunnen worden gemaakt, gewijzigd en opgehaald uit hello Azure-portal, Windows PowerShell en vanuit een runbook of de DSC-configuratie. Automation-variabelen zijn handig voor het Hallo volgen scenario's:

- Een waarde tussen meerdere runbooks of DSC-configuraties delen.

- Een waarde tussen meerdere taken van Hallo delen hetzelfde runbook of DSC-configuratie.

- Een waarde beheren vanuit de portal Hallo of vanaf Hallo Windows PowerShell-opdrachtregel die wordt gebruikt door runbooks of DSC-configuraties, zoals een set algemene configuratie-items zoals bepaalde lijst van de VM-namen, een specifieke resourcegroep, een naam voor AD-domein, enzovoort.  

Automation-variabelen worden behouden zodat ze toobe beschikbaar blijven zelfs als het Hallo-runbook of de DSC-configuratie is mislukt.  Hierdoor kunt u ook een waarde toobe ingesteld door het ene runbook die vervolgens wordt gebruikt door een andere of wordt gebruikt door Hallo hetzelfde runbook of DSC-configuratie Hallo volgende keer dat deze wordt uitgevoerd.

Wanneer een variabele is gemaakt, kunt u opgeven dat deze worden opgeslagen versleuteld.  Wanneer een variabele is versleuteld, het veilig in Azure Automation opgeslagen wordt en de waarde kan niet worden opgehaald uit Hallo [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet die wordt geleverd als onderdeel van hello Azure PowerShell-module.  Hallo enige manier om dat er een gecodeerde waarde kan worden opgehaald wordt uit Hallo **Get-AutomationVariable** activiteit in een runbook of de DSC-configuratie.

> [!NOTE]
> Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen. Deze activa zijn versleuteld en opgeslagen in hello Azure Automation, met een unieke sleutel die wordt gegenereerd voor elk automation-account. Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation. Voordat u een beveiligd bedrijfsmiddel op te slaan, Hallo-sleutel voor Hallo automation-account wordt ontsleuteld met behulp van het basiscertificaat Hallo en vervolgens gebruikt tooencrypt Hallo asset.

## <a name="variable-types"></a>Typen variabelen

Wanneer u een variabele Hello Azure-portal maakt, moet u een gegevenstype uit de vervolgkeuzelijst Hallo opgeven zodat Hallo portal Hallo juiste besturingselement voor het invoeren van de variabele waarde Hallo kunt weergeven. Hallo-variabele is niet beperkt toothis gegevens type, maar u moet instellen met behulp van Windows PowerShell als u wilt dat toospecify Hallo-variabele een waarde van een ander type. Als u opgeeft **niet gedefinieerd**, en vervolgens het Hallo-waarde van variabele hello te ingesteld**$null**, en stelt u de waarde Hallo Hello [Set AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet of **Set-AutomationVariable** activiteit.  Kan niet maken of wijzigen van Hallo-waarde voor een variabele voor complex type in Hallo-portal, maar u kunt een waarde van een type met Windows PowerShell opgeven. Complexe typen worden geretourneerd als een [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).

U kunt meerdere waarden tooa enkele variabele opslaan door het maken van een matrix of een hashtabel en opslaan van de variabele toohello.

Hallo hieronder vindt u een lijst met variabelen die beschikbaar zijn in Automation:

* Tekenreeks
* Geheel getal
* Datum/tijd
* Booleaanse waarde
* Null

## <a name="cmdlets-and-workflow-activities"></a>-Cmdlets en workflow-activiteiten

Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en beheren van Automation-variabelen met Windows PowerShell. Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](../powershell-install-configure.md) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuratie.

|Cmdlets|Beschrijving|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|Hallo-waarde van een bestaande variabele opgehaald.|
|[Nieuwe AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|Maakt een nieuwe variabele en stelt u de waarde ervan.|
|[Verwijder AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|Hiermee verwijdert u een bestaande variabele.|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|Hallo-waarde voor een bestaande variabele ingesteld.|

Hallo workflow-activiteiten in de volgende tabel Hallo zijn gebruikte tooaccess Automation-variabelen in een runbook. Ze zijn alleen beschikbaar voor gebruik in een runbook of de DSC-configuratie en niet worden geleverd als onderdeel van hello Azure PowerShell-module.

|Workflow-activiteiten|Beschrijving|
|:---|:---|
|Get-AutomationVariable|Hallo-waarde van een bestaande variabele opgehaald.|
|Set-AutomationVariable|Hallo-waarde voor een bestaande variabele ingesteld.|

> [!NOTE] 
> Vermijd het gebruik van variabelen in Hallo – Name-parameter van **Get-AutomationVariable** in een runbook of de DSC-configuratie omdat dit detecteren van afhankelijkheden tussen runbooks of DSC-configuratie en automatisering bemoeilijken kan variabelen in de ontwerpfase.

## <a name="creating-a-new-automation-variable"></a>Een nieuwe automatiseringsvariabele maken

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate een nieuwe variabele Hello Azure-portal

1. Klik op Hallo van uw Automation-account **activa** tegel en klik vervolgens op Hallo **activa** blade Selecteer **variabelen**.
2. Op Hallo **variabelen** tegel, selecteer **toevoegen van een variabele**.
3. Hallo-opties op Hallo voltooien **nieuwe variabele** blade en klik op **maken** opslaan Hallo nieuwe variabele.

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate een nieuwe variabele met Windows PowerShell

Hallo [nieuw AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet maakt een nieuwe variabele en stelt u de initiële waarde. U kunt ophalen Hallo-waarde met [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx). Hallo-waarde is een eenvoudig type, die hetzelfde type geretourneerd. Als het een complex type en vervolgens een **PSCustomObject** wordt geretourneerd.

Hallo volgende steekproef opdrachten weergeven hoe toocreate een variabele van het type tekenreeks en de retourwaarde.

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

Hallo volgende steekproef opdrachten tonen hoe een variabele met een complex toocreate installatietype en retourneren ze de eigenschappen ervan. In dit geval wordt een virtuele machine object uit **Get-AzureRmVm** wordt gebruikt.

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>Met behulp van een variabele in een runbook of de DSC-configuratie

Gebruik Hallo **Set-AutomationVariable** activiteit tooset Hallo waarde van een automatiseringsvariabele in een runbook of de DSC-configuratie en het Hallo **Get-AutomationVariable** tooretrieve deze.  Gebruik Hallo niet **Set AzureAutomationVariable** of **Get-AzureAutomationVariable** cmdlets in een runbook of de DSC-configuratie omdat ze minder efficiënt dan Hallo workflow-activiteiten zijn.  Kunt u ook niet ophalen Hallo-waarde van beveiligde variabelen met **Get-AzureAutomationVariable**.  Hallo alleen manier toocreate een nieuwe variabele van binnen een runbook of de DSC-configuratie is toouse hello [nieuw AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.


### <a name="textual-runbook-samples"></a>Tekstueel runbook-voorbeelden

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>Instellen en een eenvoudige waarde ophalen van een variabele

Hallo volgende steekproef opdrachten weergeven hoe tooset en een variabele in een tekstueel runbook op te halen. In dit voorbeeld wordt ervan uitgegaan dat variabelen van het type integer naam *NumberOfIterations* en *NumberOfRunnings* en een variabele van het type tekenreeks met de naam *SampleMessage* al zijn gemaakt.

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>Bijwerken en het ophalen van een complex object in een variabele

Hallo volgende steekproef code wordt getoond hoe tooupdate een variabele met een complexe waarde in een tekstueel runbook. In dit voorbeeld wordt een virtuele machine van Azure is opgehaald met **Get-AzureVM** en opgeslagen tooan bestaande Automation-variabele.  Zoals uitgelegd in [typen variabelen](#variable-types), dit wordt opgeslagen als een PSCustomObject.

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


In de Hallo code te volgen, wordt Hallo-waarde opgehaald uit Hallo-variabele en gebruikte toostart Hallo virtuele machine.

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>Bijwerken en het ophalen van een verzameling in een variabele

Hallo volgende steekproef code wordt getoond hoe toouse een variabele met een verzameling complexe waarden in een tekstueel runbook. In dit voorbeeld meerdere virtuele machines in Azure worden opgehaald met **Get-AzureVM** en opgeslagen tooan bestaande Automation-variabele.  Zoals uitgelegd in [typen variabelen](#variable-types), dit wordt opgeslagen als een verzameling van PSCustomObjects.

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

In Hallo code te volgen, Hallo verzameling wordt opgehaald uit het Hallo-variabele en toostart elke virtuele machine gebruikt.

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>Grafische runbook-voorbeelden

In een grafisch runbook, voegt u Hallo **Get-AutomationVariable** of **Set-AutomationVariable** door met de rechtermuisknop op het Hallo-variabele in Hallo bibliotheek deelvenster van de grafische editor Hallo en Hallo selecteren activiteit die u zoekt.

![Variabele toocanvas toevoegen](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>Instellen van waarden in een variabele
Hallo volgende afbeelding toont voorbeeld activiteiten tooupdate een variabele met een eenvoudige waarde in een grafisch runbook. In dit voorbeeld wordt een enkele virtuele machine van Azure is opgehaald met **Get-AzureRmVM** en Hallo computernaam tooan bestaande Automation-variabele van het type tekenreeks wordt opgeslagen.  Het maakt niet uit of hello [koppeling is een pijplijn of een reeks](automation-graphical-authoring-intro.md#links-and-workflow) omdat alleen we een enkel object in Hallo uitvoer verwachten.

![Eenvoudige variabele instellen](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>Volgende stappen

* Zie toolearn meer informatie over activiteiten aan elkaar koppelen in het grafisch ontwerpen [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow)
* Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md) 

