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
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="6e6d5-104">Variabele assets in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="6e6d5-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="6e6d5-105">Variabele assets zijn waarden die beschikbaar tooall runbooks en DSC-configuraties in uw automation-account zijn.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="6e6d5-106">Ze kunnen worden gemaakt, gewijzigd en opgehaald uit hello Azure-portal, Windows PowerShell en vanuit een runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="6e6d5-107">Automation-variabelen zijn handig voor het Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="6e6d5-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="6e6d5-108">Een waarde tussen meerdere runbooks of DSC-configuraties delen.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="6e6d5-109">Een waarde tussen meerdere taken van Hallo delen hetzelfde runbook of DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="6e6d5-110">Een waarde beheren vanuit de portal Hallo of vanaf Hallo Windows PowerShell-opdrachtregel die wordt gebruikt door runbooks of DSC-configuraties, zoals een set algemene configuratie-items zoals bepaalde lijst van de VM-namen, een specifieke resourcegroep, een naam voor AD-domein, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="6e6d5-111">Automation-variabelen worden behouden zodat ze toobe beschikbaar blijven zelfs als het Hallo-runbook of de DSC-configuratie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="6e6d5-112">Hierdoor kunt u ook een waarde toobe ingesteld door het ene runbook die vervolgens wordt gebruikt door een andere of wordt gebruikt door Hallo hetzelfde runbook of DSC-configuratie Hallo volgende keer dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="6e6d5-113">Wanneer een variabele is gemaakt, kunt u opgeven dat deze worden opgeslagen versleuteld.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="6e6d5-114">Wanneer een variabele is versleuteld, het veilig in Azure Automation opgeslagen wordt en de waarde kan niet worden opgehaald uit Hallo [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet die wordt geleverd als onderdeel van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="6e6d5-115">Hallo enige manier om dat er een gecodeerde waarde kan worden opgehaald wordt uit Hallo **Get-AutomationVariable** activiteit in een runbook of de DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="6e6d5-116">Beveiligde activa in Azure Automation zijn referenties, certificaten, verbindingen en gecodeerde variabelen.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="6e6d5-117">Deze activa zijn versleuteld en opgeslagen in hello Azure Automation, met een unieke sleutel die wordt gegenereerd voor elk automation-account.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="6e6d5-118">Deze sleutel is versleuteld met een basiscertificaat en opgeslagen in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="6e6d5-119">Voordat u een beveiligd bedrijfsmiddel op te slaan, Hallo-sleutel voor Hallo automation-account wordt ontsleuteld met behulp van het basiscertificaat Hallo en vervolgens gebruikt tooencrypt Hallo asset.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="6e6d5-120">Typen variabelen</span><span class="sxs-lookup"><span data-stu-id="6e6d5-120">Variable types</span></span>

<span data-ttu-id="6e6d5-121">Wanneer u een variabele Hello Azure-portal maakt, moet u een gegevenstype uit de vervolgkeuzelijst Hallo opgeven zodat Hallo portal Hallo juiste besturingselement voor het invoeren van de variabele waarde Hallo kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="6e6d5-122">Hallo-variabele is niet beperkt toothis gegevens type, maar u moet instellen met behulp van Windows PowerShell als u wilt dat toospecify Hallo-variabele een waarde van een ander type.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="6e6d5-123">Als u opgeeft **niet gedefinieerd**, en vervolgens het Hallo-waarde van variabele hello te ingesteld**$null**, en stelt u de waarde Hallo Hello [Set AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet of **Set-AutomationVariable** activiteit.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="6e6d5-124">Kan niet maken of wijzigen van Hallo-waarde voor een variabele voor complex type in Hallo-portal, maar u kunt een waarde van een type met Windows PowerShell opgeven.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="6e6d5-125">Complexe typen worden geretourneerd als een [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e6d5-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="6e6d5-126">U kunt meerdere waarden tooa enkele variabele opslaan door het maken van een matrix of een hashtabel en opslaan van de variabele toohello.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="6e6d5-127">Hallo hieronder vindt u een lijst met variabelen die beschikbaar zijn in Automation:</span><span class="sxs-lookup"><span data-stu-id="6e6d5-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="6e6d5-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="6e6d5-128">String</span></span>
* <span data-ttu-id="6e6d5-129">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="6e6d5-129">Integer</span></span>
* <span data-ttu-id="6e6d5-130">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="6e6d5-130">DateTime</span></span>
* <span data-ttu-id="6e6d5-131">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="6e6d5-131">Boolean</span></span>
* <span data-ttu-id="6e6d5-132">Null</span><span class="sxs-lookup"><span data-stu-id="6e6d5-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="6e6d5-133">-Cmdlets en workflow-activiteiten</span><span class="sxs-lookup"><span data-stu-id="6e6d5-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="6e6d5-134">Hallo-cmdlets in de volgende tabel Hallo gebruikte toocreate zijn en beheren van Automation-variabelen met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="6e6d5-135">Ze worden verzonden als onderdeel van Hallo [Azure PowerShell-module](../powershell-install-configure.md) die beschikbaar is voor gebruik in Automation-runbooks en DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="6e6d5-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="6e6d5-136">Cmdlets</span></span>|<span data-ttu-id="6e6d5-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e6d5-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="6e6d5-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="6e6d5-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="6e6d5-139">Hallo-waarde van een bestaande variabele opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="6e6d5-140">Nieuwe AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="6e6d5-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="6e6d5-141">Maakt een nieuwe variabele en stelt u de waarde ervan.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="6e6d5-142">Verwijder AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="6e6d5-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="6e6d5-143">Hiermee verwijdert u een bestaande variabele.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="6e6d5-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="6e6d5-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="6e6d5-145">Hallo-waarde voor een bestaande variabele ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="6e6d5-146">Hallo workflow-activiteiten in de volgende tabel Hallo zijn gebruikte tooaccess Automation-variabelen in een runbook.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="6e6d5-147">Ze zijn alleen beschikbaar voor gebruik in een runbook of de DSC-configuratie en niet worden geleverd als onderdeel van hello Azure PowerShell-module.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="6e6d5-148">Workflow-activiteiten</span><span class="sxs-lookup"><span data-stu-id="6e6d5-148">Workflow Activities</span></span>|<span data-ttu-id="6e6d5-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="6e6d5-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="6e6d5-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="6e6d5-150">Get-AutomationVariable</span></span>|<span data-ttu-id="6e6d5-151">Hallo-waarde van een bestaande variabele opgehaald.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="6e6d5-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="6e6d5-152">Set-AutomationVariable</span></span>|<span data-ttu-id="6e6d5-153">Hallo-waarde voor een bestaande variabele ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="6e6d5-154">Vermijd het gebruik van variabelen in Hallo – Name-parameter van **Get-AutomationVariable** in een runbook of de DSC-configuratie omdat dit detecteren van afhankelijkheden tussen runbooks of DSC-configuratie en automatisering bemoeilijken kan variabelen in de ontwerpfase.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="6e6d5-155">Een nieuwe automatiseringsvariabele maken</span><span class="sxs-lookup"><span data-stu-id="6e6d5-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="6e6d5-156">toocreate een nieuwe variabele Hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="6e6d5-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="6e6d5-157">Klik op Hallo van uw Automation-account **activa** tegel en klik vervolgens op Hallo **activa** blade Selecteer **variabelen**.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="6e6d5-158">Op Hallo **variabelen** tegel, selecteer **toevoegen van een variabele**.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="6e6d5-159">Hallo-opties op Hallo voltooien **nieuwe variabele** blade en klik op **maken** opslaan Hallo nieuwe variabele.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="6e6d5-160">toocreate een nieuwe variabele met Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e6d5-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="6e6d5-161">Hallo [nieuw AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet maakt een nieuwe variabele en stelt u de initiële waarde.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="6e6d5-162">U kunt ophalen Hallo-waarde met [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e6d5-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="6e6d5-163">Hallo-waarde is een eenvoudig type, die hetzelfde type geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="6e6d5-164">Als het een complex type en vervolgens een **PSCustomObject** wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="6e6d5-165">Hallo volgende steekproef opdrachten weergeven hoe toocreate een variabele van het type tekenreeks en de retourwaarde.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="6e6d5-166">Hallo volgende steekproef opdrachten tonen hoe een variabele met een complex toocreate installatietype en retourneren ze de eigenschappen ervan.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="6e6d5-167">In dit geval wordt een virtuele machine object uit **Get-AzureRmVm** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="6e6d5-168">Met behulp van een variabele in een runbook of de DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="6e6d5-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="6e6d5-169">Gebruik Hallo **Set-AutomationVariable** activiteit tooset Hallo waarde van een automatiseringsvariabele in een runbook of de DSC-configuratie en het Hallo **Get-AutomationVariable** tooretrieve deze.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="6e6d5-170">Gebruik Hallo niet **Set AzureAutomationVariable** of **Get-AzureAutomationVariable** cmdlets in een runbook of de DSC-configuratie omdat ze minder efficiënt dan Hallo workflow-activiteiten zijn.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="6e6d5-171">Kunt u ook niet ophalen Hallo-waarde van beveiligde variabelen met **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="6e6d5-172">Hallo alleen manier toocreate een nieuwe variabele van binnen een runbook of de DSC-configuratie is toouse hello [nieuw AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="6e6d5-173">Tekstueel runbook-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="6e6d5-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="6e6d5-174">Instellen en een eenvoudige waarde ophalen van een variabele</span><span class="sxs-lookup"><span data-stu-id="6e6d5-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="6e6d5-175">Hallo volgende steekproef opdrachten weergeven hoe tooset en een variabele in een tekstueel runbook op te halen.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="6e6d5-176">In dit voorbeeld wordt ervan uitgegaan dat variabelen van het type integer naam *NumberOfIterations* en *NumberOfRunnings* en een variabele van het type tekenreeks met de naam *SampleMessage* al zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="6e6d5-177">Bijwerken en het ophalen van een complex object in een variabele</span><span class="sxs-lookup"><span data-stu-id="6e6d5-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="6e6d5-178">Hallo volgende steekproef code wordt getoond hoe tooupdate een variabele met een complexe waarde in een tekstueel runbook.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="6e6d5-179">In dit voorbeeld wordt een virtuele machine van Azure is opgehaald met **Get-AzureVM** en opgeslagen tooan bestaande Automation-variabele.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="6e6d5-180">Zoals uitgelegd in [typen variabelen](#variable-types), dit wordt opgeslagen als een PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="6e6d5-181">In de Hallo code te volgen, wordt Hallo-waarde opgehaald uit Hallo-variabele en gebruikte toostart Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="6e6d5-182">Bijwerken en het ophalen van een verzameling in een variabele</span><span class="sxs-lookup"><span data-stu-id="6e6d5-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="6e6d5-183">Hallo volgende steekproef code wordt getoond hoe toouse een variabele met een verzameling complexe waarden in een tekstueel runbook.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="6e6d5-184">In dit voorbeeld meerdere virtuele machines in Azure worden opgehaald met **Get-AzureVM** en opgeslagen tooan bestaande Automation-variabele.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="6e6d5-185">Zoals uitgelegd in [typen variabelen](#variable-types), dit wordt opgeslagen als een verzameling van PSCustomObjects.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="6e6d5-186">In Hallo code te volgen, Hallo verzameling wordt opgehaald uit het Hallo-variabele en toostart elke virtuele machine gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="6e6d5-187">Grafische runbook-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="6e6d5-187">Graphical runbook samples</span></span>

<span data-ttu-id="6e6d5-188">In een grafisch runbook, voegt u Hallo **Get-AutomationVariable** of **Set-AutomationVariable** door met de rechtermuisknop op het Hallo-variabele in Hallo bibliotheek deelvenster van de grafische editor Hallo en Hallo selecteren activiteit die u zoekt.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Variabele toocanvas toevoegen](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="6e6d5-190">Instellen van waarden in een variabele</span><span class="sxs-lookup"><span data-stu-id="6e6d5-190">Setting values in a variable</span></span>
<span data-ttu-id="6e6d5-191">Hallo volgende afbeelding toont voorbeeld activiteiten tooupdate een variabele met een eenvoudige waarde in een grafisch runbook.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="6e6d5-192">In dit voorbeeld wordt een enkele virtuele machine van Azure is opgehaald met **Get-AzureRmVM** en Hallo computernaam tooan bestaande Automation-variabele van het type tekenreeks wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="6e6d5-193">Het maakt niet uit of hello [koppeling is een pijplijn of een reeks](automation-graphical-authoring-intro.md#links-and-workflow) omdat alleen we een enkel object in Hallo uitvoer verwachten.</span><span class="sxs-lookup"><span data-stu-id="6e6d5-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Eenvoudige variabele instellen](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="6e6d5-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e6d5-195">Next Steps</span></span>

* <span data-ttu-id="6e6d5-196">Zie toolearn meer informatie over activiteiten aan elkaar koppelen in het grafisch ontwerpen [koppelingen in het grafisch ontwerpen](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="6e6d5-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="6e6d5-197">Zie tooget gestart met grafische runbooks [Mijn eerste grafische runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="6e6d5-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

