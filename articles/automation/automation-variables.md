---
title: Variabele assets in Azure Automation | Microsoft Docs
description: Variabele assets zijn waarden die beschikbaar voor alle runbooks en in Azure Automation DSC-configuraties zijn.  Dit artikel wordt uitgelegd dat de details van de variabelen en hoe u ermee in tekstvorm en grafisch ontwerpen.
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
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="4a0b6-104">Variabele assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="4a0b6-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="4a0b6-105">Variabele assets zijn waarden die beschikbaar voor alle runbooks en DSC-configuraties in uw automation-account zijn.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="4a0b6-106">Ze kunnen worden gemaakt, gewijzigd en opgehaald uit de Azure portal, Windows PowerShell en vanuit een runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="4a0b6-107">Automation-variabelen zijn handig voor de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="4a0b6-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="4a0b6-108">Een waarde tussen meerdere runbooks of DSC-configuraties delen.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="4a0b6-109">Een waarde tussen meerdere taken van de DSC-configuratie of hetzelfde runbook delen.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="4a0b6-110">Een waarde beheren vanuit de portal of vanuit de Windows PowerShell-opdrachtregel die wordt gebruikt door runbooks of DSC-configuraties, zoals een set algemene configuratie-items zoals bepaalde lijst van de VM-namen, een specifieke resourcegroep, een naam voor AD-domein, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="4a0b6-111">Automation-variabelen worden behouden zodat ze beschikbaar blijven zelfs als het runbook of de DSC-configuratie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="4a0b6-112">Hierdoor kunt ook een waarde worden ingesteld door een runbook dat vervolgens wordt gebruikt door een ander of wordt gebruikt door de hetzelfde runbook of de DSC-configuratie de volgende keer dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="4a0b6-113">Wanneer een variabele is gemaakt, kunt u opgeven dat deze worden opgeslagen versleuteld.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="4a0b6-114">Als een variabele is versleuteld, het veilig in Azure Automation opgeslagen wordt en wordt de waarde kan niet worden opgehaald uit de [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet die wordt geleverd als onderdeel van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="4a0b6-115">De enige manier om dat er een gecodeerde waarde kan worden opgehaald, is van de **Get-AutomationVariable** activiteit in een runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="4a0b6-116">Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="4a0b6-117">Deze activa zijn versleuteld en opgeslagen in de Azure Automation met een unieke sleutel die wordt gegenereerd voor elk automation-account.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="4a0b6-118">Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="4a0b6-119">Voordat u een beveiligd bedrijfsmiddel op te slaan, wordt de sleutel voor het automation-account worden ontsleuteld met het basiscertificaat en vervolgens worden gebruikt voor het versleutelen van de asset.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="4a0b6-120">Typen variabelen</span><span class="sxs-lookup"><span data-stu-id="4a0b6-120">Variable types</span></span>

<span data-ttu-id="4a0b6-121">Wanneer u een variabele met de Azure portal maakt, kunt u een gegevenstype uit de vervolgkeuzelijst moet opgeven, zodat het juiste besturingselement voor het invoeren van de variabele waarde door de portal kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="4a0b6-122">De variabele is niet beperkt tot dit gegevenstype, maar u moet de variabele met Windows PowerShell als u wilt opgeven van een waarde van een ander type instellen.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="4a0b6-123">Als u opgeeft **niet gedefinieerd**, wordt de waarde van de variabele wordt ingesteld op **$null**, en moet u instellen dat de waarde met de [Set AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet of **Set-AutomationVariable** activiteit.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="4a0b6-124">U kunt maken of wijzig de waarde voor een variabele voor complex type in de portal, maar u kunt een waarde van een type met Windows PowerShell opgeven.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="4a0b6-125">Complexe typen worden geretourneerd als een [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a0b6-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="4a0b6-126">U kunt meerdere waarden in een enkele variabele opslaan door het maken van een matrix of een hashtabel en op de variabele op te slaan.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="4a0b6-127">Hier volgen een lijst met variabelen die beschikbaar zijn in Automation:</span><span class="sxs-lookup"><span data-stu-id="4a0b6-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="4a0b6-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4a0b6-128">String</span></span>
* <span data-ttu-id="4a0b6-129">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="4a0b6-129">Integer</span></span>
* <span data-ttu-id="4a0b6-130">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="4a0b6-130">DateTime</span></span>
* <span data-ttu-id="4a0b6-131">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4a0b6-131">Boolean</span></span>
* <span data-ttu-id="4a0b6-132">Null</span><span class="sxs-lookup"><span data-stu-id="4a0b6-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="4a0b6-133">-Cmdlets en workflow-activiteiten</span><span class="sxs-lookup"><span data-stu-id="4a0b6-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="4a0b6-134">De cmdlets in de volgende tabel worden gebruikt voor het maken en beheren van Automation-variabelen met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="4a0b6-135">Ze worden verzonden als onderdeel van de [Azure PowerShell-module](../powershell-install-configure.md) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="4a0b6-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="4a0b6-136">Cmdlets</span></span>|<span data-ttu-id="4a0b6-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4a0b6-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="4a0b6-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="4a0b6-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="4a0b6-139">Haalt de waarde van een bestaande variabele.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="4a0b6-140">Nieuwe AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="4a0b6-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="4a0b6-141">Maakt een nieuwe variabele en stelt u de waarde ervan.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="4a0b6-142">Verwijder AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="4a0b6-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="4a0b6-143">Hiermee verwijdert u een bestaande variabele.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="4a0b6-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="4a0b6-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="4a0b6-145">De waarde voor een bestaande variabele ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="4a0b6-146">De workflow-activiteiten in de volgende tabel worden gebruikt voor toegang tot Automation-variabelen in een runbook.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="4a0b6-147">Ze zijn alleen beschikbaar voor gebruik in een runbook of de DSC-configuratie en niet worden geleverd als onderdeel van de Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="4a0b6-148">Workflow-activiteiten</span><span class="sxs-lookup"><span data-stu-id="4a0b6-148">Workflow Activities</span></span>|<span data-ttu-id="4a0b6-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4a0b6-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="4a0b6-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="4a0b6-150">Get-AutomationVariable</span></span>|<span data-ttu-id="4a0b6-151">Haalt de waarde van een bestaande variabele.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="4a0b6-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="4a0b6-152">Set-AutomationVariable</span></span>|<span data-ttu-id="4a0b6-153">De waarde voor een bestaande variabele ingesteld.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="4a0b6-154">Vermijd het gebruik van variabelen in de parameter-Name van **Get-AutomationVariable** in een runbook of de DSC-configuratie omdat dit detecteren van afhankelijkheden tussen runbooks of DSC-configuratie en de Automation-variabelen tijdens de ontwerpfase bemoeilijken kan.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="4a0b6-155">Een nieuwe automatiseringsvariabele maken</span><span class="sxs-lookup"><span data-stu-id="4a0b6-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="4a0b6-156">Een nieuwe variabele maken met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="4a0b6-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="4a0b6-157">Van uw Automation-account, klikt u op de **activa** tegel en klik vervolgens op de **activa** blade Selecteer **variabelen**.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="4a0b6-158">Op de **variabelen** tegel, selecteer **toevoegen van een variabele**.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="4a0b6-159">Het voltooien van de opties op de **nieuwe variabele** blade en klik op **maken** opslaan van de nieuwe variabele.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="4a0b6-160">Een nieuwe variabele maken met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a0b6-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="4a0b6-161">De [nieuw AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet maakt een nieuwe variabele en stelt u de initiële waarde.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="4a0b6-162">U kunt ophalen met de waarde met behulp van [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="4a0b6-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="4a0b6-163">Als de waarde een eenvoudig type is, wordt dat hetzelfde type geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="4a0b6-164">Als het een complex type en vervolgens een **PSCustomObject** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="4a0b6-165">De volgende voorbeeldopdrachten laten zien hoe een variabele van het type tekenreeks maken en vervolgens de waarde te retourneren.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="4a0b6-166">De volgende voorbeeldopdrachten laten zien hoe een variabele maken met een complex type en vervolgens de eigenschappen ervan te retourneren.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="4a0b6-167">In dit geval wordt een virtuele machine object uit **Get-AzureRmVm** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="4a0b6-168">Met behulp van een variabele in een runbook of de DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="4a0b6-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="4a0b6-169">Gebruik de **Set-AutomationVariable** activiteit is de waarde van een Automation-variabele instellen in een runbook of de DSC-configuratie en de **Get-AutomationVariable** te halen.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="4a0b6-170">Gebruik niet de **Set AzureAutomationVariable** of **Get-AzureAutomationVariable** cmdlets in een runbook of de DSC-configuratie omdat ze minder efficiënt dan de werkstroomactiviteiten zijn.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="4a0b6-171">U de waarde van beveiligde variabelen met ook niet ophalen **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="4a0b6-172">De enige manier om een nieuwe variabele van binnen een runbook of de DSC-configuratie maken is met de [nieuw AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="4a0b6-173">Tekstueel runbook-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="4a0b6-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="4a0b6-174">Instellen en een eenvoudige waarde ophalen van een variabele</span><span class="sxs-lookup"><span data-stu-id="4a0b6-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="4a0b6-175">De volgende voorbeeldopdrachten laten zien hoe instelt en ophaalt van een variabele in een tekstueel runbook.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="4a0b6-176">In dit voorbeeld wordt ervan uitgegaan dat variabelen van het type integer naam *NumberOfIterations* en *NumberOfRunnings* en een variabele van het type tekenreeks met de naam *SampleMessage* al zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="4a0b6-177">Bijwerken en het ophalen van een complex object in een variabele</span><span class="sxs-lookup"><span data-stu-id="4a0b6-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="4a0b6-178">De volgende voorbeeldcode laat zien hoe een variabele met een complexe waarde in een tekstueel runbook bijwerken.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="4a0b6-179">In dit voorbeeld wordt een virtuele machine van Azure is opgehaald met **Get-AzureVM** en opgeslagen in een bestaand Automation-variabele.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="4a0b6-180">Zoals uitgelegd in [typen variabelen](#variable-types), dit wordt opgeslagen als een PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="4a0b6-181">De waarde is opgehaald van de variabele en gebruikt voor het starten van de virtuele machine in de volgende code.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="4a0b6-182">Bijwerken en het ophalen van een verzameling in een variabele</span><span class="sxs-lookup"><span data-stu-id="4a0b6-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="4a0b6-183">De volgende voorbeeldcode laat zien hoe het gebruik van een variabele met een verzameling complexe waarden in een tekstueel runbook.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="4a0b6-184">In dit voorbeeld meerdere virtuele machines in Azure worden opgehaald met **Get-AzureVM** en opgeslagen in een bestaand Automation-variabele.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="4a0b6-185">Zoals uitgelegd in [typen variabelen](#variable-types), dit wordt opgeslagen als een verzameling van PSCustomObjects.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="4a0b6-186">De verzameling is opgehaald van de variabele en gebruikt voor het starten van elke virtuele machine in de volgende code.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="4a0b6-187">Grafische runbook-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="4a0b6-187">Graphical runbook samples</span></span>

<span data-ttu-id="4a0b6-188">In een grafisch runbook, voegt u de **Get-AutomationVariable** of **Set-AutomationVariable** door met de rechtermuisknop op de variabele in het deelvenster bibliotheek van de grafische editor en de activiteit die u wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Variabele aan canvas toevoegen](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="4a0b6-190">Instellen van waarden in een variabele</span><span class="sxs-lookup"><span data-stu-id="4a0b6-190">Setting values in a variable</span></span>
<span data-ttu-id="4a0b6-191">De volgende afbeelding toont een voorbeeld van activiteiten voor het bijwerken van een variabele met een eenvoudige waarde in een grafisch runbook.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="4a0b6-192">In dit voorbeeld wordt een enkele virtuele machine van Azure is opgehaald met **Get-AzureRmVM** en naam van de computer is opgeslagen in een bestaand Automation-variabele van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="4a0b6-193">Het maakt niet uit of de [koppeling is een pijplijn of een reeks](automation-graphical-authoring-intro.md#links-and-workflow) omdat alleen we een enkel object in de uitvoer verwachten.</span><span class="sxs-lookup"><span data-stu-id="4a0b6-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Eenvoudige variabele instellen](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="4a0b6-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a0b6-195">Next Steps</span></span>

* <span data-ttu-id="4a0b6-196">Zie voor meer informatie over het aansluiten van activiteiten bij elkaar in grafisch ontwerpen, [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="4a0b6-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="4a0b6-197">Zie [Mijn eerste grafische runbook](automation-first-runbook-graphical.md) om aan de slag te gaan met grafische runbooks</span><span class="sxs-lookup"><span data-stu-id="4a0b6-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

