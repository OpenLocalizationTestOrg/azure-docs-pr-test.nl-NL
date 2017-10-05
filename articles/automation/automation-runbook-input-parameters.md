---
title: De invoerparameters van Runbook | Microsoft Docs
description: Invoerparameters van Runbook vergroot de flexibiliteit van runbooks doordat u gegevens moeten worden doorgegeven aan een runbook wanneer deze wordt gestart. In dit artikel beschrijft de verschillende scenario's waar invoerparameters worden gebruikt in runbooks.
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 4d3dff2c-1f55-498d-9a0e-eee497e5bedb
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: sngun
ms.openlocfilehash: 1ebf32338f5242e72eb2e2daa2da50d231f4b683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="02593-104">Invoerparameters voor runbook</span><span class="sxs-lookup"><span data-stu-id="02593-104">Runbook input parameters</span></span>
<span data-ttu-id="02593-105">Invoerparameters van Runbook vergroot de flexibiliteit van runbooks doordat u gegevens moeten worden doorgegeven aan wanneer deze wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-105">Runbook input parameters increase the flexibility of runbooks by allowing you to pass data to it when it is started.</span></span> <span data-ttu-id="02593-106">De parameters kunnen de acties van het runbook moet worden toegepast voor specifieke scenario's en omgevingen.</span><span class="sxs-lookup"><span data-stu-id="02593-106">The parameters allow the runbook actions to be targeted for specific scenarios and environments.</span></span> <span data-ttu-id="02593-107">In dit artikel begeleidt we u stapsgewijs door verschillende scenario's waar invoerparameters worden gebruikt in runbooks.</span><span class="sxs-lookup"><span data-stu-id="02593-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="02593-108">Invoerparameters configureren</span><span class="sxs-lookup"><span data-stu-id="02593-108">Configure input parameters</span></span>
<span data-ttu-id="02593-109">Invoerparameters kunnen worden geconfigureerd in PowerShell en PowerShell Workflow grafische runbooks.</span><span class="sxs-lookup"><span data-stu-id="02593-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="02593-110">Een runbook kan meerdere parameters met verschillende gegevenstypen, of hebben geen parameters helemaal.</span><span class="sxs-lookup"><span data-stu-id="02593-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="02593-111">Invoerparameters kunnen worden verplicht of optioneel en u een standaardwaarde opgeven voor optionele parameters kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="02593-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="02593-112">U kunt waarden toewijzen aan de invoerparameters voor een runbook bij het starten via een van de beschikbare methoden.</span><span class="sxs-lookup"><span data-stu-id="02593-112">You can assign values to the input parameters for a runbook when you start it through one of the available methods.</span></span> <span data-ttu-id="02593-113">Deze methoden omvatten een runbook starten vanuit de portal of een webservice.</span><span class="sxs-lookup"><span data-stu-id="02593-113">These methods include starting  a runbook from the portal  or a web service.</span></span> <span data-ttu-id="02593-114">U kunt ook starten als een onderliggend runbook dat inline wordt aangeroepen in een ander runbook.</span><span class="sxs-lookup"><span data-stu-id="02593-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="02593-115">De invoerparameters in PowerShell en PowerShell Workflow-runbooks configureren</span><span class="sxs-lookup"><span data-stu-id="02593-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="02593-116">PowerShell en [PowerShell Workflow-runbooks](automation-first-runbook-textual.md) in Azure Automation ondersteunen invoerparameters die via de volgende kenmerken worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="02593-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through the following attributes.</span></span>  

| <span data-ttu-id="02593-117">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="02593-117">**Property**</span></span> | <span data-ttu-id="02593-118">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="02593-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="02593-119">Type</span><span class="sxs-lookup"><span data-stu-id="02593-119">Type</span></span> |<span data-ttu-id="02593-120">Vereist.</span><span class="sxs-lookup"><span data-stu-id="02593-120">Required.</span></span> <span data-ttu-id="02593-121">Het gegevenstype voor de waarde van parameter verwacht.</span><span class="sxs-lookup"><span data-stu-id="02593-121">The data type expected for the parameter value.</span></span> <span data-ttu-id="02593-122">Elk type .NET is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="02593-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="02593-123">Naam</span><span class="sxs-lookup"><span data-stu-id="02593-123">Name</span></span> |<span data-ttu-id="02593-124">Vereist.</span><span class="sxs-lookup"><span data-stu-id="02593-124">Required.</span></span> <span data-ttu-id="02593-125">De naam van de parameter.</span><span class="sxs-lookup"><span data-stu-id="02593-125">The name of the parameter.</span></span> <span data-ttu-id="02593-126">Dit moet uniek zijn binnen het runbook en kan bevatten alleen letters, cijfers of onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="02593-126">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="02593-127">Moet beginnen met een letter.</span><span class="sxs-lookup"><span data-stu-id="02593-127">It must start with a letter.</span></span> |
| <span data-ttu-id="02593-128">Verplicht</span><span class="sxs-lookup"><span data-stu-id="02593-128">Mandatory</span></span> |<span data-ttu-id="02593-129">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-129">Optional.</span></span> <span data-ttu-id="02593-130">Hiermee geeft u op of een waarde voor de parameter moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="02593-130">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="02593-131">Als u dit instellen op **$true**, en vervolgens moet een waarde worden opgegeven wanneer het runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-131">If you set this to **$true**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="02593-132">Als u dit instellen op **$false**, en vervolgens een waarde optioneel is.</span><span class="sxs-lookup"><span data-stu-id="02593-132">If you set this to **$false**, then a value is optional.</span></span> |
| <span data-ttu-id="02593-133">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="02593-133">Default value</span></span> |<span data-ttu-id="02593-134">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-134">Optional.</span></span>  <span data-ttu-id="02593-135">Hiermee geeft u een waarde die voor de parameter worden gebruikt als een waarde niet is doorgegeven als het runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-135">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="02593-136">Een standaardwaarde zal kan worden ingesteld voor elke parameter en automatisch de parameter optioneel ongeacht de verplichte instelling.</span><span class="sxs-lookup"><span data-stu-id="02593-136">A default value can be set for any parameter and will automatically make the parameter optional regardless of the Mandatory setting.</span></span> |

<span data-ttu-id="02593-137">Windows PowerShell ondersteunt meer kenmerken van invoerparameters dan die hier worden vermeld, zoals validatie, aliassen en parametersets.</span><span class="sxs-lookup"><span data-stu-id="02593-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="02593-138">Azure Automation ondersteunt momenteel echter alleen de invoerparameters die hierboven worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="02593-138">However, Azure Automation currently supports only the input parameters listed above.</span></span>

<span data-ttu-id="02593-139">De parameterdefinitie van een in PowerShell Workflow-runbooks heeft de volgende algemene vorm waarin meerdere parameters zijn gescheiden door komma's.</span><span class="sxs-lookup"><span data-stu-id="02593-139">A parameter definition in PowerShell Workflow runbooks has the following general form, where multiple parameters are separated by commas.</span></span>

   ```
     Param
     (
         [Parameter (Mandatory= $true/$false)]
         [Type] Name1 = <Default value>,

         [Parameter (Mandatory= $true/$false)]
         [Type] Name2 = <Default value>
     )
   ```

> [!NOTE]
> <span data-ttu-id="02593-140">Wanneer u parameters, als u geen opgeeft definieert het **verplichte** kenmerk, wordt standaard de parameter wordt beschouwd als optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-140">When you're defining parameters, if you don’t specify the **Mandatory** attribute, then by default, the parameter is considered optional.</span></span> <span data-ttu-id="02593-141">Ook als u een standaardwaarde voor een parameter in PowerShell Workflow-runbooks instelt, wordt deze verwerkt door PowerShell als een optionele parameter, ongeacht de **verplichte** kenmerkwaarde.</span><span class="sxs-lookup"><span data-stu-id="02593-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of the **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="02593-142">Als voorbeeld gaan we de invoerparameters configureren voor een PowerShell Workflow-runbook die uitvoer meer informatie over virtuele machines, één VM of alle virtuele machines binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="02593-142">As an example, let’s configure the input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="02593-143">Dit runbook heeft twee parameters zoals aangegeven in de volgende schermafbeelding: de naam van de virtuele machine en de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="02593-143">This runbook has two parameters as shown in the following screenshot: the name of virtual machine and the name of the resource group.</span></span>

![Werkstroom voor automatisering van PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="02593-145">In de parameterdefinitie van deze, de parameters **$VMName** en **$resourceGroupName** eenvoudige parameters van het type tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="02593-145">In this parameter definition, the parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="02593-146">PowerShell en PowerShell Workflow-runbooks ondersteunen echter alle eenvoudige typen en complexe typen, zoals **object** of **PSCredential** voor invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="02593-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="02593-147">Als uw runbook een invoerparameter objecttype heeft, gebruikt u een PowerShell-hashtable met (naam, waarde) paren om door te geven in een waarde.</span><span class="sxs-lookup"><span data-stu-id="02593-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs to pass in a value.</span></span> <span data-ttu-id="02593-148">Bijvoorbeeld, als u de volgende parameter in een runbook hebt:</span><span class="sxs-lookup"><span data-stu-id="02593-148">For example, if you have the following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="02593-149">U kunt vervolgens de volgende waarde doorgeven aan de parameter:</span><span class="sxs-lookup"><span data-stu-id="02593-149">Then you can pass the following value to the parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="02593-150">De invoerparameters in grafische runbooks configureren</span><span class="sxs-lookup"><span data-stu-id="02593-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="02593-151">Naar [configureren van een grafisch runbook](automation-first-runbook-graphical.md) met invoerparameters we maken een grafisch runbook die meer informatie over virtuele machines, ofwel een enkele virtuele machine of alle virtuele machines binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="02593-151">To [configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="02593-152">Configureren van een runbook bestaat uit twee belangrijkste activiteiten, zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="02593-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="02593-153">[**Runbooks verifiëren met Azure uitvoeren als-account** ](automation-sec-configure-azure-runas-account.md) te verifiëren bij Azure.</span><span class="sxs-lookup"><span data-stu-id="02593-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) to authenticate with Azure.</span></span>

<span data-ttu-id="02593-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) ophalen van de eigenschappen van een virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="02593-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) to get the properties of a virtual machines.</span></span>

<span data-ttu-id="02593-155">U kunt de [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) activiteit voor uitvoer van de namen van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="02593-155">You can use the [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity to output the names of virtual machines.</span></span> <span data-ttu-id="02593-156">De activiteit **Get-AzureRmVm** twee parameters accepteert de **virtuele-machinenaam** en de **Resourcegroepnaam**.</span><span class="sxs-lookup"><span data-stu-id="02593-156">The activity **Get-AzureRmVm** accepts two parameters, the **virtual machine name** and the **resource group name**.</span></span> <span data-ttu-id="02593-157">Omdat deze parameters voor verschillende waarden telkens wanneer die u het runbook start vereist kunnen, kunt u invoerparameters toevoegen aan uw runbook.</span><span class="sxs-lookup"><span data-stu-id="02593-157">Since these parameters could require different values each time you start the runbook, you can add input parameters to your runbook.</span></span> <span data-ttu-id="02593-158">Hier volgen de stappen voor de invoerparameters toevoegen:</span><span class="sxs-lookup"><span data-stu-id="02593-158">Here are the steps to add input parameters:</span></span>

1. <span data-ttu-id="02593-159">Selecteer het grafisch runbook vanuit de **Runbooks** blade en klik vervolgens op [ **bewerken** ](automation-graphical-authoring-intro.md) deze.</span><span class="sxs-lookup"><span data-stu-id="02593-159">Select the graphical runbook from the **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="02593-160">Klik in de runbookeditor op **invoer en uitvoer** openen de **invoer en uitvoer** blade.</span><span class="sxs-lookup"><span data-stu-id="02593-160">From the runbook editor, click **Input and output** to open the **Input and output** blade.</span></span>
   
    ![Grafisch runbook automatisering](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="02593-162">De **invoer en uitvoer** blade geeft een lijst met invoerparameters die zijn gedefinieerd voor het runbook.</span><span class="sxs-lookup"><span data-stu-id="02593-162">The **Input and output** blade displays a list of input parameters that are defined for the runbook.</span></span> <span data-ttu-id="02593-163">Op deze blade kunt u een nieuwe invoerparameter toevoegen of bewerken van de configuratie van een bestaande invoerparameter.</span><span class="sxs-lookup"><span data-stu-id="02593-163">On this blade, you can either add a new input parameter or edit the configuration of an existing input parameter.</span></span> <span data-ttu-id="02593-164">Klik op als u een nieuwe parameter voor het runbook **invoer toevoegen** openen de **runbookinvoerparameter** blade.</span><span class="sxs-lookup"><span data-stu-id="02593-164">To add a new parameter for the runbook, click **Add input** to open the **Runbook input parameter** blade.</span></span> <span data-ttu-id="02593-165">Daar kunt u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="02593-165">There, you can configure the following parameters:</span></span>
   
   | <span data-ttu-id="02593-166">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="02593-166">**Property**</span></span> | <span data-ttu-id="02593-167">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="02593-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="02593-168">Naam</span><span class="sxs-lookup"><span data-stu-id="02593-168">Name</span></span> |<span data-ttu-id="02593-169">Vereist.</span><span class="sxs-lookup"><span data-stu-id="02593-169">Required.</span></span>  <span data-ttu-id="02593-170">De naam van de parameter.</span><span class="sxs-lookup"><span data-stu-id="02593-170">The name of the parameter.</span></span> <span data-ttu-id="02593-171">Dit moet uniek zijn binnen het runbook en kan bevatten alleen letters, cijfers of onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="02593-171">This must be unique within the runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="02593-172">Moet beginnen met een letter.</span><span class="sxs-lookup"><span data-stu-id="02593-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="02593-173">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="02593-173">Description</span></span> |<span data-ttu-id="02593-174">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-174">Optional.</span></span> <span data-ttu-id="02593-175">Beschrijving van het doel van de invoerparameter.</span><span class="sxs-lookup"><span data-stu-id="02593-175">Description about the purpose of input parameter.</span></span> |
   | <span data-ttu-id="02593-176">Type</span><span class="sxs-lookup"><span data-stu-id="02593-176">Type</span></span> |<span data-ttu-id="02593-177">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-177">Optional.</span></span> <span data-ttu-id="02593-178">Het gegevenstype dat voor de waarde van parameter wordt verwacht.</span><span class="sxs-lookup"><span data-stu-id="02593-178">The data type that's expected for the parameter value.</span></span> <span data-ttu-id="02593-179">De van de ondersteunde parametertypen zijn **tekenreeks**, **Int32**, **Int64**, **decimale**, **Booleaanse**, **DateTime**, en **Object**.</span><span class="sxs-lookup"><span data-stu-id="02593-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="02593-180">Als een gegevenstype dat niet is ingeschakeld, wordt standaard **tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="02593-180">If a data type is not selected, it defaults to **String**.</span></span> |
   | <span data-ttu-id="02593-181">Verplicht</span><span class="sxs-lookup"><span data-stu-id="02593-181">Mandatory</span></span> |<span data-ttu-id="02593-182">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-182">Optional.</span></span> <span data-ttu-id="02593-183">Hiermee geeft u op of een waarde voor de parameter moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="02593-183">Specifies whether a value must be provided for the parameter.</span></span> <span data-ttu-id="02593-184">Als u ervoor kiest **Ja**, en vervolgens moet een waarde worden opgegeven wanneer het runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-184">If you choose **yes**, then a value must be provided when the runbook is started.</span></span> <span data-ttu-id="02593-185">Als u ervoor kiest **geen**, en vervolgens een waarde niet vereist is als het runbook wordt gestart en een standaardwaarde kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="02593-185">If you choose **no**, then a value is not required when the runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="02593-186">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="02593-186">Default Value</span></span> |<span data-ttu-id="02593-187">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-187">Optional.</span></span> <span data-ttu-id="02593-188">Hiermee geeft u een waarde die voor de parameter worden gebruikt als een waarde niet is doorgegeven als het runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-188">Specifies a value that will be used for the parameter if a value is not passed in when the runbook is started.</span></span> <span data-ttu-id="02593-189">Een standaardwaarde kan worden ingesteld voor een parameter die is niet verplicht.</span><span class="sxs-lookup"><span data-stu-id="02593-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="02593-190">Als u wilt een standaardwaarde instelt, kies **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="02593-190">To set a default value, choose **Custom**.</span></span> <span data-ttu-id="02593-191">Deze waarde wordt gebruikt, tenzij een andere waarde wordt opgegeven als het runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-191">This value is used unless another value is provided when the runbook is started.</span></span> <span data-ttu-id="02593-192">Kies **geen** als u niet wilt bieden een standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="02593-192">Choose **None** if you don’t want to provide any default value.</span></span> |
   
    ![Nieuwe invoer toevoegen](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="02593-194">Twee parameters maken met de volgende eigenschappen die worden gebruikt door de **Get-AzureRmVm** activiteit:</span><span class="sxs-lookup"><span data-stu-id="02593-194">Create two parameters with the following properties that will be used by the **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="02593-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="02593-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="02593-196">Naam - VMName</span><span class="sxs-lookup"><span data-stu-id="02593-196">Name - VMName</span></span>
     * <span data-ttu-id="02593-197">Type - tekenreeks</span><span class="sxs-lookup"><span data-stu-id="02593-197">Type - String</span></span>
     * <span data-ttu-id="02593-198">Verplicht - Nee</span><span class="sxs-lookup"><span data-stu-id="02593-198">Mandatory - No</span></span>
   * <span data-ttu-id="02593-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="02593-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="02593-200">Naam - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="02593-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="02593-201">Type - tekenreeks</span><span class="sxs-lookup"><span data-stu-id="02593-201">Type - String</span></span>
     * <span data-ttu-id="02593-202">Verplicht - Nee</span><span class="sxs-lookup"><span data-stu-id="02593-202">Mandatory - No</span></span>
     * <span data-ttu-id="02593-203">Standaardwaarde - aangepast</span><span class="sxs-lookup"><span data-stu-id="02593-203">Default value - Custom</span></span>
     * <span data-ttu-id="02593-204">Aangepaste standaardwaarde - \<naam van de resourcegroep met de virtuele machines ></span><span class="sxs-lookup"><span data-stu-id="02593-204">Custom default value - \<Name of the resource group that contains the virtual machines></span></span>
5. <span data-ttu-id="02593-205">Nadat u de parameters toevoegt, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="02593-205">Once you add the parameters, click **OK**.</span></span>  <span data-ttu-id="02593-206">U kunt nu deze bekijken in de **invoer en uitvoer blade**.</span><span class="sxs-lookup"><span data-stu-id="02593-206">You can now view them in the **Input and output blade**.</span></span> <span data-ttu-id="02593-207">Klik op **OK** opnieuw, en klik vervolgens op **opslaan** en **publiceren** uw runbook.</span><span class="sxs-lookup"><span data-stu-id="02593-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-to-input-parameters-in-runbooks"></a><span data-ttu-id="02593-208">Geef waarden op de invoerparameters in runbooks</span><span class="sxs-lookup"><span data-stu-id="02593-208">Assign values to input parameters in runbooks</span></span>
<span data-ttu-id="02593-209">Waarden voor de invoerparameters in runbooks in de volgende scenario's kan worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="02593-209">You can pass values to input parameters in runbooks in the following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="02593-210">Een runbook Start en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="02593-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="02593-211">Een runbook kan op veel verschillende manieren worden gestart: via de Azure portal, met een webhook, met PowerShell-cmdlets, met de REST-API of met de SDK.</span><span class="sxs-lookup"><span data-stu-id="02593-211">A runbook can be started many ways: through the Azure portal, with a webhook, with PowerShell cmdlets, with the REST API, or with the SDK.</span></span> <span data-ttu-id="02593-212">Hieronder besproken verschillende methoden voor een runbook starten en het toewijzen van parameters.</span><span class="sxs-lookup"><span data-stu-id="02593-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-the-azure-portal-and-assign-parameters"></a><span data-ttu-id="02593-213">Een gepubliceerd runbook start met behulp van de Azure-portal en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="02593-213">Start a published runbook by using the Azure portal and assign parameters</span></span>
<span data-ttu-id="02593-214">Wanneer u [het runbook starten](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), wordt de **Runbook starten** blade wordt geopend en u kunt waarden configureren voor de parameters die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="02593-214">When you [start the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), the **Start Runbook** blade opens and you can configure values for the parameters that you just created.</span></span>

![Aan de slag met de portal](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="02593-216">In het label onder het invoervak ziet u de kenmerken die zijn ingesteld voor de parameter.</span><span class="sxs-lookup"><span data-stu-id="02593-216">In the label beneath the input box, you can see the attributes that have been set for the parameter.</span></span> <span data-ttu-id="02593-217">Kenmerken zijn verplicht of optioneel, type en de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="02593-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="02593-218">In de help-ballon naast de parameternaam van de ziet u alle belangrijke gegevens die u moet nemen van beslissingen over invoer parameterwaarden.</span><span class="sxs-lookup"><span data-stu-id="02593-218">In the help balloon next to the parameter name, you can see all the key information you need to make decisions about parameter input values.</span></span> <span data-ttu-id="02593-219">Deze informatie omvat of een parameter verplicht of optioneel is.</span><span class="sxs-lookup"><span data-stu-id="02593-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="02593-220">Dit omvat ook het type en de standaardwaarde (indien aanwezig) en andere nuttige opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="02593-220">It also includes the type and default value (if any), and other helpful notes.</span></span>

![Ballon met Help](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="02593-222">Ondersteuning voor parameters van type String **leeg** tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="02593-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="02593-223">Invoeren **[EmptyString]** in de invoerparameter vak een lege tekenreeks wordt doorgegeven aan de parameter.</span><span class="sxs-lookup"><span data-stu-id="02593-223">Entering **[EmptyString]** in the input parameter box will pass an empty string to the parameter.</span></span> <span data-ttu-id="02593-224">Ook de parameters van het type tekenreeks niet ondersteunen **Null** waarden worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="02593-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="02593-225">Als u niet de waarde van een aan de tekenreeksparameter doorgeeft, wordt vervolgens PowerShell geïnterpreteerd als null.</span><span class="sxs-lookup"><span data-stu-id="02593-225">If you don’t pass any value to the String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="02593-226">Een gepubliceerd runbook start met behulp van PowerShell-cmdlets en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="02593-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="02593-227">**Azure Resource Manager-cmdlets:** kunt u beginnen met een Automation-runbook is gemaakt in een resourcegroep met [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="02593-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="02593-228">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="02593-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="02593-229">**Azure Service Management-cmdlets:** kunt u beginnen met een automation-runbook dat is gemaakt in een standaardresourcegroep met behulp van [Start AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="02593-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="02593-230">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="02593-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="02593-231">Wanneer u een runbook start met behulp van PowerShell-cmdlets, een standaardparameter **MicrosoftApplicationManagementStartedBy** wordt gemaakt met de waarde **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="02593-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with the value **PowerShell**.</span></span> <span data-ttu-id="02593-232">U vindt deze parameter in de **taakgegevens** blade.</span><span class="sxs-lookup"><span data-stu-id="02593-232">You can view this parameter in the **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="02593-233">Een runbook start met behulp van een SDK en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="02593-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="02593-234">**Azure Resource Manager-methode:** kunt u een runbook start met behulp van de SDK van een programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="02593-234">**Azure Resource Manager method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="02593-235">Hieronder ziet u een C#-codefragment voor het starten van een runbook in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="02593-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="02593-236">U vindt de code aan onze [GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="02593-236">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
  ```
   public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
      {
        var response = AutomationClient.Jobs.Create(resourceGroupName, automationAccount, new JobCreateParameters
         {
            Properties = new JobCreateProperties
             {
                Runbook = new RunbookAssociationProperty
                 {
                   Name = runbookName
                 },
                   Parameters = parameters
             }
         });
      return response.Job;
      }
  ```
* <span data-ttu-id="02593-237">**Azure Service Management-methode:** kunt u een runbook start met behulp van de SDK van een programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="02593-237">**Azure Service Management method:** You can start a runbook by using the SDK of a programming language.</span></span> <span data-ttu-id="02593-238">Hieronder ziet u een C#-codefragment voor het starten van een runbook in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="02593-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="02593-239">U vindt de code aan onze [GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="02593-239">You can view all the code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
  ```      
  public Job StartRunbook(string runbookName, IDictionary<string, string> parameters = null)
    {
      var response = AutomationClient.Jobs.Create(automationAccount, new JobCreateParameters
    {
      Properties = new JobCreateProperties
         {
           Runbook = new RunbookAssociationProperty
         {
           Name = runbookName
              },
                Parameters = parameters
              }
       });
      return response.Job;
    }
  ```
  
  <span data-ttu-id="02593-240">Deze methode starten, een woordenlijst voor het opslaan van de runbookparameters, maakt **VMName** en **resourceGroupName**, en de bijbehorende waarden.</span><span class="sxs-lookup"><span data-stu-id="02593-240">To start this method, create a dictionary to store the runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="02593-241">Start het runbook.</span><span class="sxs-lookup"><span data-stu-id="02593-241">Then start the runbook.</span></span> <span data-ttu-id="02593-242">Hieronder vindt u de C#-codefragment voor het aanroepen van de methode die hierboven gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="02593-242">Below is the C# code snippet for calling the method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters to the dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call the StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-the-rest-api-and-assign-parameters"></a><span data-ttu-id="02593-243">Een runbook start met behulp van de REST-API en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="02593-243">Start a runbook by using the REST API and assign parameters</span></span>
<span data-ttu-id="02593-244">Een runbooktaak worden gemaakt en gestart met de REST-API van Azure Automation met behulp van de **plaatsen** methode met de volgende aanvraag-URI.</span><span class="sxs-lookup"><span data-stu-id="02593-244">A runbook job can be created and started with the Azure Automation REST API by using the **PUT** method with the following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="02593-245">In de aanvraag-URI, vervangt u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="02593-245">In the request URI, replace the following parameters:</span></span>

* <span data-ttu-id="02593-246">**abonnement-id:** uw Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="02593-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="02593-247">**cloud-service-naam:** de naam van de cloud service aan de aanvraag moet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="02593-247">**cloud-service-name:** The name of the cloud service to which the request should be sent.</span></span>  
* <span data-ttu-id="02593-248">**Automation-account-name:** de naam van uw automation-account die wordt gehost binnen de opgegeven cloudservice.</span><span class="sxs-lookup"><span data-stu-id="02593-248">**automation-account-name:** The name of your automation account that's hosted within the specified cloud service.</span></span>  
* <span data-ttu-id="02593-249">**taak-id:** de GUID voor de taak.</span><span class="sxs-lookup"><span data-stu-id="02593-249">**job-id:** The GUID for the job.</span></span> <span data-ttu-id="02593-250">GUID's in PowerShell kunnen worden gemaakt met behulp van de **[GUID]::NewGuid(). ToString()** opdracht.</span><span class="sxs-lookup"><span data-stu-id="02593-250">GUIDs in PowerShell can be created by using the **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="02593-251">Gebruiken om de parameters doorgeven aan de runbooktaak, de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="02593-251">In order to pass parameters to the runbook job, use the request body.</span></span> <span data-ttu-id="02593-252">Het duurt de volgende twee eigenschappen in het JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="02593-252">It takes the following two properties provided in JSON format:</span></span>

* <span data-ttu-id="02593-253">**Runbooknaam:** vereist.</span><span class="sxs-lookup"><span data-stu-id="02593-253">**Runbook name:** Required.</span></span> <span data-ttu-id="02593-254">De naam van het runbook voor de taak is gestart.</span><span class="sxs-lookup"><span data-stu-id="02593-254">The name of the runbook for the job to start.</span></span>  
* <span data-ttu-id="02593-255">**Runbook-parameters:** optioneel.</span><span class="sxs-lookup"><span data-stu-id="02593-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="02593-256">Een dictionary van de lijst met parameters in (naam, waarde) waar de naam moet van het type tekenreeks en de waarde is een geldig JSON-waarde opmaken.</span><span class="sxs-lookup"><span data-stu-id="02593-256">A dictionary of the parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="02593-257">Als u wilt beginnen de **Get-AzureVMTextual** runbook dat eerder is gemaakt met **VMName** en **resourceGroupName** als parameters, gebruikt u de volgende JSON-indeling voor de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="02593-257">If you want to start the **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use the following JSON format for the request body.</span></span>

   ```
    {
      "properties":{
        "runbook":{
        "name":"Get-AzureVMTextual"},
      "parameters":{
         "VMName":"WSVMClassic",
         "resourceGroupName":”WSCS1”}
        }
    }
   ```

<span data-ttu-id="02593-258">Een HTTP-statuscode 201 wordt geretourneerd als de taak is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="02593-258">A HTTP status code 201 is returned if the job is successfully created.</span></span> <span data-ttu-id="02593-259">Raadpleeg voor meer informatie over antwoordheaders en de antwoordtekst naar het artikel over het [een runbooktaak maken met behulp van de REST-API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="02593-259">For more information on response headers and the response body, refer to the article about how to [create a runbook job by using the REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="02593-260">Een runbook testen en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="02593-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="02593-261">Wanneer u [de conceptversie van uw runbook testen](automation-testing-runbook.md) met de optie test de **testen** blade wordt geopend en u kunt waarden configureren voor de parameters die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="02593-261">When you [test the draft version of your runbook](automation-testing-runbook.md) by using the test option, the **Test** blade opens and you can configure values for the parameters that you just created.</span></span>

![Testen en parameters toewijzen](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-to-a-runbook-and-assign-parameters"></a><span data-ttu-id="02593-263">Een planning aan een runbook koppelen en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="02593-263">Link a schedule to a runbook and assign parameters</span></span>
<span data-ttu-id="02593-264">U kunt [een planning koppelen](automation-schedules.md) aan uw runbook zodat het runbook wordt gestart op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="02593-264">You can [link a schedule](automation-schedules.md) to your runbook so that the runbook starts at a specific time.</span></span> <span data-ttu-id="02593-265">U toewijzen invoerparameters wanneer u de planning maakt en het runbook deze waarden worden gebruikt wanneer deze is gestart volgens de planning.</span><span class="sxs-lookup"><span data-stu-id="02593-265">You assign input parameters when you create the schedule, and the runbook will use these values when it is started by the schedule.</span></span> <span data-ttu-id="02593-266">U kunt de planning niet opslaan, totdat alle verplichte parameterwaarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="02593-266">You can’t save the schedule until all mandatory parameter values are provided.</span></span>

![Plannen en parameters toewijzen](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="02593-268">Een webhook voor een runbook maken en toewijzen van parameters</span><span class="sxs-lookup"><span data-stu-id="02593-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="02593-269">Kunt u een [webhook](automation-webhooks.md) voor uw runbook en invoerparameters van runbook configureren.</span><span class="sxs-lookup"><span data-stu-id="02593-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="02593-270">U kunt de webhook niet opslaan, totdat alle verplichte parameterwaarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="02593-270">You can’t save the webhook until all mandatory parameter values are provided.</span></span>

![Webhook maken en toewijzen van parameters](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="02593-272">Bij het uitvoeren van een runbook met behulp van een webhook, de vooraf gedefinieerde invoerparameter  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  wordt verzonden, samen met de invoerparameters die u hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="02593-272">When you execute a runbook by using a webhook, the predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with the input parameters that you defined.</span></span> <span data-ttu-id="02593-273">U kunt klikken op om uit te breiden de **WebhookData** parameter voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02593-273">You can click to expand the **WebhookData** parameter for more details.</span></span>

![WebhookData-parameter](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="02593-275">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02593-275">Next steps</span></span>
* <span data-ttu-id="02593-276">Zie voor meer informatie over runbookinvoer en uitvoer [Azure Automation: runbook invoer, uitvoer en geneste runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="02593-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="02593-277">Zie voor meer informatie over de verschillende manieren om een runbook te starten, [een runbook starten](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="02593-277">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="02593-278">Raadpleeg tekstueel runbook bewerken, [bewerken tekstuele runbooks](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="02593-278">To edit a textual runbook, refer to [Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="02593-279">Raadpleeg een grafisch runbook bewerken, [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="02593-279">To edit a graphical runbook, refer to [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

