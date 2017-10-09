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
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="1b2ab-104">Geeft een JSON-object tooan Azure Automation-runbook</span><span class="sxs-lookup"><span data-stu-id="1b2ab-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="1b2ab-105">Het kan nuttig toostore gegevens die u wilt dat toopass tooa runbook in een JSON-bestand zijn.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="1b2ab-106">U kunt bijvoorbeeld een JSON-bestand met alle parameters Hallo maken gewenste toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="1b2ab-107">toodo dit u tooconvert Hallo JSON tooa tekenreeks hebben en deze vervolgens converteren Hallo tekenreeks tooa PowerShell-object voordat de inhoud toohello runbook doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="1b2ab-108">In dit voorbeeld maakt u een PowerShell-script aanroept [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart een PowerShell-runbook Hallo inhoud van Hallo JSON toohello runbook wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="1b2ab-109">Hallo PowerShell-runbook wordt gestart van een virtuele machine van Azure, Hallo parameters voor Hallo VM ophalen uit Hallo JSON die is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b2ab-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b2ab-110">Prerequisites</span></span>
<span data-ttu-id="1b2ab-111">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b2ab-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1b2ab-112">Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-112">Azure subscription.</span></span> <span data-ttu-id="1b2ab-113">Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1b2ab-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="1b2ab-114">[Automation-account](automation-sec-configure-azure-runas-account.md) toohold Hallo runbook en tooAzure bronnen te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="1b2ab-115">Dit account moet hebben machtiging toostart en stop Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="1b2ab-116">Een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-116">An Azure virtual machine.</span></span> <span data-ttu-id="1b2ab-117">We stoppen en starten deze machine, dus het mag geen productiemachine zijn.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="1b2ab-118">Azure Powershell installeren op een lokale machine.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="1b2ab-119">Zie [installeren en configureren van Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) voor informatie over het tooget Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="1b2ab-120">Hallo JSON-bestand maken</span><span class="sxs-lookup"><span data-stu-id="1b2ab-120">Create hello JSON file</span></span>

<span data-ttu-id="1b2ab-121">Type Hallo volgende testen in een tekstbestand en sla het bestand als `test.json` ergens op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="1b2ab-122">Hallo-runbook maken</span><span class="sxs-lookup"><span data-stu-id="1b2ab-122">Create hello runbook</span></span>

<span data-ttu-id="1b2ab-123">Maak een nieuw PowerShell-runbook met de naam 'Test-Json' in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="1b2ab-124">hoe een nieuwe PowerShell-runbook toocreate zien toolearn [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1b2ab-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="1b2ab-125">tooaccept hello JSON-gegevens Hallo runbook moet rekening houden met een object als invoerparameter.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="1b2ab-126">Hallo runbook kunt Hallo-eigenschappen die zijn gedefinieerd in Hallo JSON vervolgens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

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

 <span data-ttu-id="1b2ab-127">Opslaan en dit runbook publiceren in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="1b2ab-128">Hallo runbook aanroepen vanuit PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b2ab-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="1b2ab-129">U kunt nu Hallo runbook aanroepen vanuit uw lokale computer met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="1b2ab-130">Voer Hallo volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="1b2ab-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="1b2ab-131">Meld u bij tooAzure:</span><span class="sxs-lookup"><span data-stu-id="1b2ab-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="1b2ab-132">U na vragen aan gebruiker tooenter worden uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="1b2ab-133">Hallo-inhoud van de JSON-bestand Hallo ophalen en deze converteren tooa tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="1b2ab-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="1b2ab-134">`JsonPath`Hallo-pad waar u Hallo JSON-bestand hebt opgeslagen is.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="1b2ab-135">Hallo tekenreeks inhoud van converteren `$json` tooa PowerShell-object:</span><span class="sxs-lookup"><span data-stu-id="1b2ab-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="1b2ab-136">Maken van een hashtabel voor Hallo parameters voor `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="1b2ab-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="1b2ab-137">U ziet dat u Hallo-waarde van instelt `Parameters` toohello PowerShell-object die Hallo waarden uit Hallo JSON-bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="1b2ab-138">Hallo runbook starten</span><span class="sxs-lookup"><span data-stu-id="1b2ab-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="1b2ab-139">Hallo runbook Hallo waarden van Hallo JSON-bestand toostart een virtuele machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1b2ab-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b2ab-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b2ab-140">Next steps</span></span>

* <span data-ttu-id="1b2ab-141">Zie toolearn meer informatie over het bewerken van PowerShell en PowerShell Workflow-runbooks met een teksteditor [tekstuele runbooks in Azure Automation bewerken](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="1b2ab-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="1b2ab-142">toolearn meer informatie over het maken en importeren van runbooks, Zie [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="1b2ab-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


