---
title: Een JSON-object doorgeven aan een Azure Automation-runbook | Microsoft Docs
description: Hoe parameters doorgeven aan een runbook als een JSON-object
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
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="92f9d-104">Een JSON-object doorgeven aan een Azure Automation-runbook</span><span class="sxs-lookup"><span data-stu-id="92f9d-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="92f9d-105">Dit kan nuttig zijn voor het opslaan van gegevens die u wilt doorgeven aan een runbook in een JSON-bestand zijn.</span><span class="sxs-lookup"><span data-stu-id="92f9d-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="92f9d-106">U kunt bijvoorbeeld een JSON-bestand met alle van de parameters die u wilt doorgeven aan een runbook maken.</span><span class="sxs-lookup"><span data-stu-id="92f9d-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="92f9d-107">U doet dit door die u moet de JSON converteren naar een tekenreeks en vervolgens de tekenreeks niet converteren naar een PowerShell-object voordat de inhoud wordt doorgegeven aan het runbook.</span><span class="sxs-lookup"><span data-stu-id="92f9d-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="92f9d-108">In dit voorbeeld maakt u een PowerShell-script aanroept [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) een PowerShell-runbook, de inhoud van de JSON wordt doorgegeven aan het runbook starten.</span><span class="sxs-lookup"><span data-stu-id="92f9d-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="92f9d-109">Het PowerShell-runbook start een Azure VM, het ophalen van de parameters voor de virtuele machine uit de JSON die is doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="92f9d-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92f9d-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92f9d-110">Prerequisites</span></span>
<span data-ttu-id="92f9d-111">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="92f9d-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="92f9d-112">Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="92f9d-112">Azure subscription.</span></span> <span data-ttu-id="92f9d-113">Als u nog geen abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) of <a href="/pricing/free-account/" target="_blank">[u aanmelden voor een gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="92f9d-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="92f9d-114">[Automation-account](automation-sec-configure-azure-runas-account.md) om het runbook te bevatten en te verifiëren voor Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="92f9d-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="92f9d-115">Dit account moet machtigingen hebben om de virtuele machine te starten en stoppen.</span><span class="sxs-lookup"><span data-stu-id="92f9d-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="92f9d-116">Een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="92f9d-116">An Azure virtual machine.</span></span> <span data-ttu-id="92f9d-117">We stoppen en starten deze machine, dus het mag geen productiemachine zijn.</span><span class="sxs-lookup"><span data-stu-id="92f9d-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="92f9d-118">Azure Powershell installeren op een lokale machine.</span><span class="sxs-lookup"><span data-stu-id="92f9d-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="92f9d-119">Zie [installeren en configureren van Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) voor informatie over het ophalen van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92f9d-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="92f9d-120">Het JSON-bestand maken</span><span class="sxs-lookup"><span data-stu-id="92f9d-120">Create the JSON file</span></span>

<span data-ttu-id="92f9d-121">Typ de volgende test in een tekstbestand en sla het bestand als `test.json` ergens op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="92f9d-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="92f9d-122">Het runbook te maken</span><span class="sxs-lookup"><span data-stu-id="92f9d-122">Create the runbook</span></span>

<span data-ttu-id="92f9d-123">Maak een nieuw PowerShell-runbook met de naam 'Test-Json' in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="92f9d-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="92f9d-124">Zie voor meer informatie over het maken van een nieuwe PowerShell-runbook, [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="92f9d-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="92f9d-125">Het runbook moet een object nemen als invoerparameter voor het accepteren van de JSON-gegevens.</span><span class="sxs-lookup"><span data-stu-id="92f9d-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="92f9d-126">De eigenschappen die zijn gedefinieerd in de JSON kan vervolgens worden gebruikt in het runbook.</span><span class="sxs-lookup"><span data-stu-id="92f9d-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="92f9d-127">Opslaan en dit runbook publiceren in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="92f9d-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="92f9d-128">Het runbook aanroepen vanuit PowerShell</span><span class="sxs-lookup"><span data-stu-id="92f9d-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="92f9d-129">U kunt nu het runbook aanroepen vanuit uw lokale computer met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92f9d-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="92f9d-130">Voer de volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="92f9d-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="92f9d-131">Aanmelden bij Azure:</span><span class="sxs-lookup"><span data-stu-id="92f9d-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="92f9d-132">U wordt gevraagd uw Azure-referenties invoeren.</span><span class="sxs-lookup"><span data-stu-id="92f9d-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="92f9d-133">Ophalen van de inhoud van het JSON-bestand en converteren naar een tekenreeks:</span><span class="sxs-lookup"><span data-stu-id="92f9d-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="92f9d-134">`JsonPath`is het pad waar u het JSON-bestand opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="92f9d-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="92f9d-135">Converteren van de inhoud van de tekenreeks van `$json` naar een PowerShell-object:</span><span class="sxs-lookup"><span data-stu-id="92f9d-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="92f9d-136">Maken van een hashtabel voor de parameters voor `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="92f9d-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="92f9d-137">U ziet dat u de waarde van instelt `Parameters` naar het PowerShell-object dat de waarden van het JSON-bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="92f9d-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="92f9d-138">Het runbook starten</span><span class="sxs-lookup"><span data-stu-id="92f9d-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="92f9d-139">Het runbook maakt gebruik van de waarden van het JSON-bestand naar een virtuele machine start.</span><span class="sxs-lookup"><span data-stu-id="92f9d-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92f9d-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92f9d-140">Next steps</span></span>

* <span data-ttu-id="92f9d-141">Zie voor meer informatie over het bewerken van PowerShell en PowerShell Workflow-runbooks met een teksteditor, [tekstuele runbooks in Azure Automation bewerken](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="92f9d-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="92f9d-142">Zie voor meer informatie over het maken en importeren van runbooks [maken of importeren van een runbook in Azure Automation](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="92f9d-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


