---
title: aaaPass een JSON-object tooan Azure Automation-runbook | Microsoft Docs
description: Hoe toopass parameters tooa runbook als een JSON-object
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: PowerShell, runbook, json, azure automation
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Geeft een JSON-object tooan Azure Automation-runbook

Het kan nuttig toostore gegevens die u wilt dat toopass tooa runbook in een JSON-bestand zijn.
U kunt bijvoorbeeld een JSON-bestand met alle parameters Hallo maken gewenste toopass tooa runbook.
toodo dit u tooconvert Hallo JSON tooa tekenreeks hebben en deze vervolgens converteren Hallo tekenreeks tooa PowerShell-object voordat de inhoud toohello runbook doorgegeven.

In dit voorbeeld maakt u een PowerShell-script aanroept [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart een PowerShell-runbook Hallo inhoud van Hallo JSON toohello runbook wordt doorgegeven.
Hallo PowerShell-runbook wordt gestart van een virtuele machine van Azure, Hallo parameters voor Hallo VM ophalen uit Hallo JSON die is doorgegeven.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u hello te volgen:

* Azure-abonnement. Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).
* [Automation-account](automation-sec-configure-azure-runas-account.md) toohold Hallo runbook en tooAzure bronnen te verifiëren.  Dit account moet hebben machtiging toostart en stop Hallo virtuele machine.
* Een virtuele machine van Azure. We stoppen en starten deze machine, dus het mag geen productiemachine zijn.
* Azure Powershell installeren op een lokale machine. Zie [installeren en configureren van Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) voor informatie over het tooget Azure PowerShell.

## <a name="create-hello-json-file"></a>Hallo JSON-bestand maken

Type Hallo volgende testen in een tekstbestand en sla het bestand als `test.json` ergens op uw lokale computer.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Hallo-runbook maken

Maak een nieuw PowerShell-runbook met de naam 'Test-Json' in Azure Automation.
hoe een nieuwe PowerShell-runbook toocreate zien toolearn [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md).

tooaccept hello JSON-gegevens Hallo runbook moet rekening houden met een object als invoerparameter.

Hallo runbook kunt Hallo-eigenschappen die zijn gedefinieerd in Hallo JSON vervolgens gebruiken.

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 Opslaan en dit runbook publiceren in uw Automation-account.

## <a name="call-hello-runbook-from-powershell"></a>Hallo runbook aanroepen vanuit PowerShell

U kunt nu Hallo runbook aanroepen vanuit uw lokale computer met behulp van Azure PowerShell.
Voer Hallo volgende PowerShell-opdrachten:

1. Meld u bij tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    U na vragen aan gebruiker tooenter worden uw Azure-referenties.
1. Hallo-inhoud van de JSON-bestand Hallo ophalen en deze converteren tooa tekenreeks:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`Hallo-pad waar u Hallo JSON-bestand hebt opgeslagen is.
1. Hallo tekenreeks inhoud van converteren `$json` tooa PowerShell-object:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Maken van een hashtabel voor Hallo parameters voor `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   U ziet dat u Hallo-waarde van instelt `Parameters` toohello PowerShell-object die Hallo waarden uit Hallo JSON-bestand bevat. 
1. Hallo runbook starten
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Hallo runbook Hallo waarden van Hallo JSON-bestand toostart een virtuele machine gebruikt.

## <a name="next-steps"></a>Volgende stappen

* Zie toolearn meer informatie over het bewerken van PowerShell en PowerShell Workflow-runbooks met een teksteditor [tekstuele runbooks in Azure Automation bewerken](automation-edit-textual-runbook.md) 
* toolearn meer informatie over het maken en importeren van runbooks, Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)


