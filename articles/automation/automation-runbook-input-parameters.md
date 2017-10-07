---
title: parameters voor invoer aaaRunbook | Microsoft Docs
description: Invoerparameters van Runbook verhogen Hallo flexibiliteit van runbooks doordat u toopass gegevens tooa runbook wanneer deze wordt gestart. In dit artikel beschrijft de verschillende scenario's waar invoerparameters worden gebruikt in runbooks.
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
ms.openlocfilehash: f3abaf92382e7d41019616bafb14af23cf98dd9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-input-parameters"></a><span data-ttu-id="2cd73-104">Invoerparameters voor runbook</span><span class="sxs-lookup"><span data-stu-id="2cd73-104">Runbook input parameters</span></span>
<span data-ttu-id="2cd73-105">Invoerparameters van Runbook verhogen Hallo flexibiliteit van runbooks doordat u toopass gegevens tooit wanneer deze wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-105">Runbook input parameters increase hello flexibility of runbooks by allowing you toopass data tooit when it is started.</span></span> <span data-ttu-id="2cd73-106">Hallo-parameters kunt Hallo runbook acties toobe is bedoeld voor specifieke scenario's en omgevingen.</span><span class="sxs-lookup"><span data-stu-id="2cd73-106">hello parameters allow hello runbook actions toobe targeted for specific scenarios and environments.</span></span> <span data-ttu-id="2cd73-107">In dit artikel begeleidt we u stapsgewijs door verschillende scenario's waar invoerparameters worden gebruikt in runbooks.</span><span class="sxs-lookup"><span data-stu-id="2cd73-107">In this article, we will walk you through different scenarios where input parameters are used in runbooks.</span></span>

## <a name="configure-input-parameters"></a><span data-ttu-id="2cd73-108">Invoerparameters configureren</span><span class="sxs-lookup"><span data-stu-id="2cd73-108">Configure input parameters</span></span>
<span data-ttu-id="2cd73-109">Invoerparameters kunnen worden geconfigureerd in PowerShell en PowerShell Workflow grafische runbooks.</span><span class="sxs-lookup"><span data-stu-id="2cd73-109">Input parameters can be configured in PowerShell, PowerShell Workflow, and graphical runbooks.</span></span> <span data-ttu-id="2cd73-110">Een runbook kan meerdere parameters met verschillende gegevenstypen, of hebben geen parameters helemaal.</span><span class="sxs-lookup"><span data-stu-id="2cd73-110">A runbook can have multiple parameters with different data types, or no parameters at all.</span></span> <span data-ttu-id="2cd73-111">Invoerparameters kunnen worden verplicht of optioneel en u een standaardwaarde opgeven voor optionele parameters kunt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="2cd73-111">Input parameters can be mandatory or optional, and you can assign a default value for optional parameters.</span></span> <span data-ttu-id="2cd73-112">U kunt waarden toewijzen toohello invoerparameters voor een runbook wanneer u deze via een van de beschikbare methoden Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="2cd73-112">You can assign values toohello input parameters for a runbook when you start it through one of hello available methods.</span></span> <span data-ttu-id="2cd73-113">Deze methoden omvatten een runbook starten vanuit de portal hello of een webservice.</span><span class="sxs-lookup"><span data-stu-id="2cd73-113">These methods include starting  a runbook from hello portal  or a web service.</span></span> <span data-ttu-id="2cd73-114">U kunt ook starten als een onderliggend runbook dat inline wordt aangeroepen in een ander runbook.</span><span class="sxs-lookup"><span data-stu-id="2cd73-114">You can also start one as a child runbook that is called inline in another runbook.</span></span>

## <a name="configure-input-parameters-in-powershell-and-powershell-workflow-runbooks"></a><span data-ttu-id="2cd73-115">De invoerparameters in PowerShell en PowerShell Workflow-runbooks configureren</span><span class="sxs-lookup"><span data-stu-id="2cd73-115">Configure input parameters in PowerShell and PowerShell Workflow runbooks</span></span>
<span data-ttu-id="2cd73-116">PowerShell en [PowerShell Workflow-runbooks](automation-first-runbook-textual.md) in Azure Automation ondersteunen invoerparameters die zijn gedefinieerd via Hallo kenmerken te volgen.</span><span class="sxs-lookup"><span data-stu-id="2cd73-116">PowerShell and [PowerShell Workflow runbooks](automation-first-runbook-textual.md) in Azure Automation support input parameters that are defined through hello following attributes.</span></span>  

| <span data-ttu-id="2cd73-117">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="2cd73-117">**Property**</span></span> | <span data-ttu-id="2cd73-118">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="2cd73-118">**Description**</span></span> |
|:--- |:--- |
| <span data-ttu-id="2cd73-119">Type</span><span class="sxs-lookup"><span data-stu-id="2cd73-119">Type</span></span> |<span data-ttu-id="2cd73-120">Vereist.</span><span class="sxs-lookup"><span data-stu-id="2cd73-120">Required.</span></span> <span data-ttu-id="2cd73-121">Hallo-gegevenstype voor de parameterwaarde Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="2cd73-121">hello data type expected for hello parameter value.</span></span> <span data-ttu-id="2cd73-122">Elk type .NET is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="2cd73-122">Any .NET type is valid.</span></span> |
| <span data-ttu-id="2cd73-123">Naam</span><span class="sxs-lookup"><span data-stu-id="2cd73-123">Name</span></span> |<span data-ttu-id="2cd73-124">Vereist.</span><span class="sxs-lookup"><span data-stu-id="2cd73-124">Required.</span></span> <span data-ttu-id="2cd73-125">Hallo-naam van Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="2cd73-125">hello name of hello parameter.</span></span> <span data-ttu-id="2cd73-126">Dit moet uniek zijn binnen Hallo runbook, en kan bevatten alleen letters, cijfers of onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="2cd73-126">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="2cd73-127">Moet beginnen met een letter.</span><span class="sxs-lookup"><span data-stu-id="2cd73-127">It must start with a letter.</span></span> |
| <span data-ttu-id="2cd73-128">Verplicht</span><span class="sxs-lookup"><span data-stu-id="2cd73-128">Mandatory</span></span> |<span data-ttu-id="2cd73-129">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-129">Optional.</span></span> <span data-ttu-id="2cd73-130">Hiermee geeft u op of een waarde voor parameter Hallo moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2cd73-130">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="2cd73-131">Als u deze te instelt**$true**, en vervolgens moet een waarde worden opgegeven wanneer Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-131">If you set this too**$true**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="2cd73-132">Als u deze te instelt**$false**, en vervolgens een waarde optioneel is.</span><span class="sxs-lookup"><span data-stu-id="2cd73-132">If you set this too**$false**, then a value is optional.</span></span> |
| <span data-ttu-id="2cd73-133">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="2cd73-133">Default value</span></span> |<span data-ttu-id="2cd73-134">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-134">Optional.</span></span>  <span data-ttu-id="2cd73-135">Hiermee geeft u een waarde die voor de parameter hello worden gebruikt als een waarde niet is doorgegeven als Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-135">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="2cd73-136">Een standaardwaarde kan worden ingesteld voor elke parameter en wordt automatisch doorgevoerd Hallo parameter optionele ongeacht Hallo verplichte instelling.</span><span class="sxs-lookup"><span data-stu-id="2cd73-136">A default value can be set for any parameter and will automatically make hello parameter optional regardless of hello Mandatory setting.</span></span> |

<span data-ttu-id="2cd73-137">Windows PowerShell ondersteunt meer kenmerken van invoerparameters dan die hier worden vermeld, zoals validatie, aliassen en parametersets.</span><span class="sxs-lookup"><span data-stu-id="2cd73-137">Windows PowerShell supports more attributes of input parameters than those listed here, like validation, aliases, and parameter sets.</span></span> <span data-ttu-id="2cd73-138">Azure Automation ondersteunt echter momenteel alleen Hallo invoerparameters die hierboven worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="2cd73-138">However, Azure Automation currently supports only hello input parameters listed above.</span></span>

<span data-ttu-id="2cd73-139">De parameterdefinitie van een in PowerShell Workflow-runbooks heeft Hallo volgen algemene vorm waarin meerdere parameters zijn gescheiden door komma's.</span><span class="sxs-lookup"><span data-stu-id="2cd73-139">A parameter definition in PowerShell Workflow runbooks has hello following general form, where multiple parameters are separated by commas.</span></span>

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
> <span data-ttu-id="2cd73-140">Wanneer u parameters, als u geen Hallo opgeeft definieert **verplichte** kenmerk, wordt standaard Hallo parameter wordt beschouwd als optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-140">When you're defining parameters, if you don’t specify hello **Mandatory** attribute, then by default, hello parameter is considered optional.</span></span> <span data-ttu-id="2cd73-141">Ook als u een standaardwaarde voor een parameter in PowerShell Workflow-runbooks instelt, wordt deze verwerkt door PowerShell als een optionele parameter, ongeacht Hallo **verplichte** kenmerkwaarde.</span><span class="sxs-lookup"><span data-stu-id="2cd73-141">Also, if you set a default value for a parameter in PowerShell Workflow runbooks, it will be treated by PowerShell as an optional parameter, regardless of hello **Mandatory** attribute value.</span></span>
> 
> 

<span data-ttu-id="2cd73-142">Een voorbeeld: Stel Hallo invoerparameters configureren voor een PowerShell Workflow-runbook die uitvoer meer informatie over virtuele machines, één VM of alle virtuele machines binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2cd73-142">As an example, let’s configure hello input parameters for a PowerShell Workflow runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="2cd73-143">Dit runbook heeft twee parameters zoals weergegeven in de volgende schermafbeelding Hallo: Hallo-naam van de virtuele machine en de naam van de resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2cd73-143">This runbook has two parameters as shown in hello following screenshot: hello name of virtual machine and hello name of hello resource group.</span></span>

![Werkstroom voor automatisering van PowerShell](media/automation-runbook-input-parameters/automation-01-powershellworkflow.png)

<span data-ttu-id="2cd73-145">In deze parameterdefinitie Hallo parameters **$VMName** en **$resourceGroupName** eenvoudige parameters van het type tekenreeks zijn.</span><span class="sxs-lookup"><span data-stu-id="2cd73-145">In this parameter definition, hello parameters **$VMName** and **$resourceGroupName** are simple parameters of type string.</span></span> <span data-ttu-id="2cd73-146">PowerShell en PowerShell Workflow-runbooks ondersteunen echter alle eenvoudige typen en complexe typen, zoals **object** of **PSCredential** voor invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="2cd73-146">However, PowerShell and PowerShell Workflow runbooks support all simple types and complex types, such as **object** or **PSCredential** for input parameters.</span></span>

<span data-ttu-id="2cd73-147">Als uw runbook een invoerparameter objecttype heeft, gebruik vervolgens een hashtabel PowerShell met (naam, waarde) toopass in een waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="2cd73-147">If your runbook has an object type input parameter, then use a PowerShell hashtable with (name,value) pairs toopass in a value.</span></span> <span data-ttu-id="2cd73-148">Bijvoorbeeld, als er Hallo parameter in een runbook te volgen:</span><span class="sxs-lookup"><span data-stu-id="2cd73-148">For example, if you have hello following parameter in a runbook:</span></span>

     [Parameter (Mandatory = $true)]
     [object] $FullName

<span data-ttu-id="2cd73-149">U kunt vervolgens Hallo na waarde toohello parameter doorgeven:</span><span class="sxs-lookup"><span data-stu-id="2cd73-149">Then you can pass hello following value toohello parameter:</span></span>

    @{"FirstName"="Joe";"MiddleName"="Bob";"LastName"="Smith"}


## <a name="configure-input-parameters-in-graphical-runbooks"></a><span data-ttu-id="2cd73-150">De invoerparameters in grafische runbooks configureren</span><span class="sxs-lookup"><span data-stu-id="2cd73-150">Configure input parameters in graphical runbooks</span></span>
<span data-ttu-id="2cd73-151">te[configureren van een grafisch runbook](automation-first-runbook-graphical.md) met invoerparameters we maken een grafisch runbook die meer informatie over virtuele machines, ofwel een enkele virtuele machine of alle virtuele machines binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="2cd73-151">too[configure a graphical runbook](automation-first-runbook-graphical.md) with input parameters, let’s create a graphical runbook that outputs details about virtual machines, either a single VM or all VMs within a resource group.</span></span> <span data-ttu-id="2cd73-152">Configureren van een runbook bestaat uit twee belangrijkste activiteiten, zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="2cd73-152">Configuring a runbook consists of two major activities, as described below.</span></span>

<span data-ttu-id="2cd73-153">[**Runbooks verifiëren met Azure uitvoeren als-account** ](automation-sec-configure-azure-runas-account.md) tooauthenticate met Azure.</span><span class="sxs-lookup"><span data-stu-id="2cd73-153">[**Authenticate Runbooks with Azure Run As account**](automation-sec-configure-azure-runas-account.md) tooauthenticate with Azure.</span></span>

<span data-ttu-id="2cd73-154">[**Get-AzureRmVm** ](https://msdn.microsoft.com/library/mt603718.aspx) tooget Hallo eigenschappen van een virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2cd73-154">[**Get-AzureRmVm**](https://msdn.microsoft.com/library/mt603718.aspx) tooget hello properties of a virtual machines.</span></span>

<span data-ttu-id="2cd73-155">U kunt Hallo [ **Write-Output** ](https://technet.microsoft.com/library/hh849921.aspx) activiteit toooutput Hallo namen van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="2cd73-155">You can use hello [**Write-Output**](https://technet.microsoft.com/library/hh849921.aspx) activity toooutput hello names of virtual machines.</span></span> <span data-ttu-id="2cd73-156">Hallo activiteit **Get-AzureRmVm** accepteert twee parameters hello **virtuele-machinenaam** en Hallo **Resourcegroepnaam**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-156">hello activity **Get-AzureRmVm** accepts two parameters, hello **virtual machine name** and hello **resource group name**.</span></span> <span data-ttu-id="2cd73-157">Omdat deze parameters voor verschillende waarden telkens wanneer die u Hallo runbook start vereist kunnen, kunt u invoerparameters tooyour runbook kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2cd73-157">Since these parameters could require different values each time you start hello runbook, you can add input parameters tooyour runbook.</span></span> <span data-ttu-id="2cd73-158">Hier volgen Hallo tooadd invoerparameters-stappen:</span><span class="sxs-lookup"><span data-stu-id="2cd73-158">Here are hello steps tooadd input parameters:</span></span>

1. <span data-ttu-id="2cd73-159">Selecteer Hallo grafisch runbook uit Hallo **Runbooks** blade en klik vervolgens op [ **bewerken** ](automation-graphical-authoring-intro.md) deze.</span><span class="sxs-lookup"><span data-stu-id="2cd73-159">Select hello graphical runbook from hello **Runbooks** blade and then click [**Edit**](automation-graphical-authoring-intro.md) it.</span></span>
2. <span data-ttu-id="2cd73-160">Hallo runbookeditor, klik op **invoer en uitvoer** tooopen hello **invoer en uitvoer** blade.</span><span class="sxs-lookup"><span data-stu-id="2cd73-160">From hello runbook editor, click **Input and output** tooopen hello **Input and output** blade.</span></span>
   
    ![Grafisch runbook automatisering](media/automation-runbook-input-parameters/automation-02-graphical-runbok-editor.png)
3. <span data-ttu-id="2cd73-162">Hallo **invoer en uitvoer** blade geeft een lijst van invoerparameters die zijn gedefinieerd voor Hallo runbook weer.</span><span class="sxs-lookup"><span data-stu-id="2cd73-162">hello **Input and output** blade displays a list of input parameters that are defined for hello runbook.</span></span> <span data-ttu-id="2cd73-163">Op deze blade kunt u een nieuwe invoerparameter toevoegen of Hallo configuratie van een bestaande invoerparameter bewerken.</span><span class="sxs-lookup"><span data-stu-id="2cd73-163">On this blade, you can either add a new input parameter or edit hello configuration of an existing input parameter.</span></span> <span data-ttu-id="2cd73-164">tooadd een nieuwe parameter voor Hallo runbook, klikt u op **invoer toevoegen** tooopen hello **runbookinvoerparameter** blade.</span><span class="sxs-lookup"><span data-stu-id="2cd73-164">tooadd a new parameter for hello runbook, click **Add input** tooopen hello **Runbook input parameter** blade.</span></span> <span data-ttu-id="2cd73-165">U kunt daar Hallo volgende parameters configureren:</span><span class="sxs-lookup"><span data-stu-id="2cd73-165">There, you can configure hello following parameters:</span></span>
   
   | <span data-ttu-id="2cd73-166">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="2cd73-166">**Property**</span></span> | <span data-ttu-id="2cd73-167">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="2cd73-167">**Description**</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="2cd73-168">Naam</span><span class="sxs-lookup"><span data-stu-id="2cd73-168">Name</span></span> |<span data-ttu-id="2cd73-169">Vereist.</span><span class="sxs-lookup"><span data-stu-id="2cd73-169">Required.</span></span>  <span data-ttu-id="2cd73-170">Hallo-naam van Hallo-parameter.</span><span class="sxs-lookup"><span data-stu-id="2cd73-170">hello name of hello parameter.</span></span> <span data-ttu-id="2cd73-171">Dit moet uniek zijn binnen Hallo runbook, en kan bevatten alleen letters, cijfers of onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="2cd73-171">This must be unique within hello runbook, and can contain only letters, numbers, or underscore characters.</span></span> <span data-ttu-id="2cd73-172">Moet beginnen met een letter.</span><span class="sxs-lookup"><span data-stu-id="2cd73-172">It must start with a letter.</span></span> |
   | <span data-ttu-id="2cd73-173">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2cd73-173">Description</span></span> |<span data-ttu-id="2cd73-174">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-174">Optional.</span></span> <span data-ttu-id="2cd73-175">Beschrijving van het Hallo-doel van de invoerparameter.</span><span class="sxs-lookup"><span data-stu-id="2cd73-175">Description about hello purpose of input parameter.</span></span> |
   | <span data-ttu-id="2cd73-176">Type</span><span class="sxs-lookup"><span data-stu-id="2cd73-176">Type</span></span> |<span data-ttu-id="2cd73-177">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-177">Optional.</span></span> <span data-ttu-id="2cd73-178">Hallo-gegevenswaarde die wordt verwacht voor het Hallo-parameterwaarde.</span><span class="sxs-lookup"><span data-stu-id="2cd73-178">hello data type that's expected for hello parameter value.</span></span> <span data-ttu-id="2cd73-179">De van de ondersteunde parametertypen zijn **tekenreeks**, **Int32**, **Int64**, **decimale**, **Booleaanse**, **DateTime**, en **Object**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-179">Supported parameter types are **String**, **Int32**, **Int64**, **Decimal**, **Boolean**, **DateTime**, and **Object**.</span></span> <span data-ttu-id="2cd73-180">Als een gegevenstype dat niet is geselecteerd, is de standaardwaarde te**tekenreeks**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-180">If a data type is not selected, it defaults too**String**.</span></span> |
   | <span data-ttu-id="2cd73-181">Verplicht</span><span class="sxs-lookup"><span data-stu-id="2cd73-181">Mandatory</span></span> |<span data-ttu-id="2cd73-182">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-182">Optional.</span></span> <span data-ttu-id="2cd73-183">Hiermee geeft u op of een waarde voor parameter Hallo moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2cd73-183">Specifies whether a value must be provided for hello parameter.</span></span> <span data-ttu-id="2cd73-184">Als u ervoor kiest **Ja**, en vervolgens moet een waarde worden opgegeven wanneer Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-184">If you choose **yes**, then a value must be provided when hello runbook is started.</span></span> <span data-ttu-id="2cd73-185">Als u ervoor kiest **geen**, en vervolgens een waarde niet vereist is als Hallo runbook wordt gestart en een standaardwaarde kan worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="2cd73-185">If you choose **no**, then a value is not required when hello runbook is started, and a default value may be set.</span></span> |
   | <span data-ttu-id="2cd73-186">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="2cd73-186">Default Value</span></span> |<span data-ttu-id="2cd73-187">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-187">Optional.</span></span> <span data-ttu-id="2cd73-188">Hiermee geeft u een waarde die voor de parameter hello worden gebruikt als een waarde niet is doorgegeven als Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-188">Specifies a value that will be used for hello parameter if a value is not passed in when hello runbook is started.</span></span> <span data-ttu-id="2cd73-189">Een standaardwaarde kan worden ingesteld voor een parameter die is niet verplicht.</span><span class="sxs-lookup"><span data-stu-id="2cd73-189">A default value can be set for a parameter that's not mandatory.</span></span> <span data-ttu-id="2cd73-190">Kies een standaardwaarde tooset **aangepaste**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-190">tooset a default value, choose **Custom**.</span></span> <span data-ttu-id="2cd73-191">Deze waarde wordt gebruikt, tenzij een andere waarde wordt opgegeven als Hallo runbook wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-191">This value is used unless another value is provided when hello runbook is started.</span></span> <span data-ttu-id="2cd73-192">Kies **geen** als u niet tooprovide wilt een standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="2cd73-192">Choose **None** if you don’t want tooprovide any default value.</span></span> |
   
    ![Nieuwe invoer toevoegen](media/automation-runbook-input-parameters/automation-runbook-input-parameter-new.png)
4. <span data-ttu-id="2cd73-194">Twee parameters maken met de volgende eigenschappen die worden gebruikt door Hallo Hallo **Get-AzureRmVm** activiteit:</span><span class="sxs-lookup"><span data-stu-id="2cd73-194">Create two parameters with hello following properties that will be used by hello **Get-AzureRmVm** activity:</span></span>
   
   * <span data-ttu-id="2cd73-195">**Parameter1:**</span><span class="sxs-lookup"><span data-stu-id="2cd73-195">**Parameter1:**</span></span>
     
     * <span data-ttu-id="2cd73-196">Naam - VMName</span><span class="sxs-lookup"><span data-stu-id="2cd73-196">Name - VMName</span></span>
     * <span data-ttu-id="2cd73-197">Type - tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2cd73-197">Type - String</span></span>
     * <span data-ttu-id="2cd73-198">Verplicht - Nee</span><span class="sxs-lookup"><span data-stu-id="2cd73-198">Mandatory - No</span></span>
   * <span data-ttu-id="2cd73-199">**Parameter2:**</span><span class="sxs-lookup"><span data-stu-id="2cd73-199">**Parameter2:**</span></span>
     
     * <span data-ttu-id="2cd73-200">Naam - resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="2cd73-200">Name - resourceGroupName</span></span>
     * <span data-ttu-id="2cd73-201">Type - tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2cd73-201">Type - String</span></span>
     * <span data-ttu-id="2cd73-202">Verplicht - Nee</span><span class="sxs-lookup"><span data-stu-id="2cd73-202">Mandatory - No</span></span>
     * <span data-ttu-id="2cd73-203">Standaardwaarde - aangepast</span><span class="sxs-lookup"><span data-stu-id="2cd73-203">Default value - Custom</span></span>
     * <span data-ttu-id="2cd73-204">Aangepaste standaardwaarde - \<naam van resourcegroep Hallo Hallo virtuele machines met ></span><span class="sxs-lookup"><span data-stu-id="2cd73-204">Custom default value - \<Name of hello resource group that contains hello virtual machines></span></span>
5. <span data-ttu-id="2cd73-205">Nadat u Hallo parameters toevoegen, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-205">Once you add hello parameters, click **OK**.</span></span>  <span data-ttu-id="2cd73-206">U kunt ze nu weergeven in Hallo **invoer en uitvoer blade**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-206">You can now view them in hello **Input and output blade**.</span></span> <span data-ttu-id="2cd73-207">Klik op **OK** opnieuw, en klik vervolgens op **opslaan** en **publiceren** uw runbook.</span><span class="sxs-lookup"><span data-stu-id="2cd73-207">Click **OK** again, and then click **Save** and **Publish** your runbook.</span></span>

## <a name="assign-values-tooinput-parameters-in-runbooks"></a><span data-ttu-id="2cd73-208">Waarden toewijzen tooinput parameters in runbooks</span><span class="sxs-lookup"><span data-stu-id="2cd73-208">Assign values tooinput parameters in runbooks</span></span>
<span data-ttu-id="2cd73-209">U kunt waarden tooinput parameters doorgeven in runbooks in Hallo volgen scenario's.</span><span class="sxs-lookup"><span data-stu-id="2cd73-209">You can pass values tooinput parameters in runbooks in hello following scenarios.</span></span>

### <a name="start-a-runbook-and-assign-parameters"></a><span data-ttu-id="2cd73-210">Een runbook Start en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-210">Start a runbook and assign parameters</span></span>
<span data-ttu-id="2cd73-211">Een runbook kan op veel verschillende manieren worden gestart: via hello Azure-portal, met een webhook, met PowerShell-cmdlets, hello REST-API of Hello SDK.</span><span class="sxs-lookup"><span data-stu-id="2cd73-211">A runbook can be started many ways: through hello Azure portal, with a webhook, with PowerShell cmdlets, with hello REST API, or with hello SDK.</span></span> <span data-ttu-id="2cd73-212">Hieronder besproken verschillende methoden voor een runbook starten en het toewijzen van parameters.</span><span class="sxs-lookup"><span data-stu-id="2cd73-212">Below we discuss different methods for starting a runbook and assigning parameters.</span></span>

#### <a name="start-a-published-runbook-by-using-hello-azure-portal-and-assign-parameters"></a><span data-ttu-id="2cd73-213">Een gepubliceerd runbook start met behulp van hello Azure-portal en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-213">Start a published runbook by using hello Azure portal and assign parameters</span></span>
<span data-ttu-id="2cd73-214">Wanneer u [hello runbook starten](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), Hallo **Runbook starten** blade wordt geopend en kunt u waarden voor Hallo-parameters die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2cd73-214">When you [start hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal), hello **Start Runbook** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Aan de slag met Hallo-portal](media/automation-runbook-input-parameters/automation-04-startrunbookusingportal.png)

<span data-ttu-id="2cd73-216">Hallo-label onder het invoervak hello ziet u Hallo kenmerken die zijn ingesteld voor parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="2cd73-216">In hello label beneath hello input box, you can see hello attributes that have been set for hello parameter.</span></span> <span data-ttu-id="2cd73-217">Kenmerken zijn verplicht of optioneel, type en de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="2cd73-217">Attributes include mandatory or optional, type, and  default value.</span></span> <span data-ttu-id="2cd73-218">Hallo help ballon volgende toohello parameternamen ziet u alle Hallo belangrijke informatie die u toomake beslissingen te nemen over parameter invoerwaarden nodig.</span><span class="sxs-lookup"><span data-stu-id="2cd73-218">In hello help balloon next toohello parameter name, you can see all hello key information you need toomake decisions about parameter input values.</span></span> <span data-ttu-id="2cd73-219">Deze informatie omvat of een parameter verplicht of optioneel is.</span><span class="sxs-lookup"><span data-stu-id="2cd73-219">This information includes whether a parameter is mandatory or optional.</span></span> <span data-ttu-id="2cd73-220">Dit omvat ook Hallo type en de standaardwaarde (indien aanwezig) en andere nuttige notities.</span><span class="sxs-lookup"><span data-stu-id="2cd73-220">It also includes hello type and default value (if any), and other helpful notes.</span></span>

![Ballon met Help](media/automation-runbook-input-parameters/automation-05-helpbaloon.png)

> [!NOTE]
> <span data-ttu-id="2cd73-222">Ondersteuning voor parameters van type String **leeg** tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="2cd73-222">String type parameters support **Empty** String values.</span></span>  <span data-ttu-id="2cd73-223">Invoeren **[EmptyString]** in Hallo invoerparameter vak geeft een lege tekenreeks toohello-parameter.</span><span class="sxs-lookup"><span data-stu-id="2cd73-223">Entering **[EmptyString]** in hello input parameter box will pass an empty string toohello parameter.</span></span> <span data-ttu-id="2cd73-224">Ook de parameters van het type tekenreeks niet ondersteunen **Null** waarden worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="2cd73-224">Also, String type parameters don’t support **Null** values being passed.</span></span> <span data-ttu-id="2cd73-225">Als u waarde toohello tekenreeksparameter gebruikt niet slaagt, wordt klikt u vervolgens PowerShell geïnterpreteerd als null.</span><span class="sxs-lookup"><span data-stu-id="2cd73-225">If you don’t pass any value toohello String parameter, then PowerShell will interpret it as null.</span></span>
> 
> 

#### <a name="start-a-published-runbook-by-using-powershell-cmdlets-and-assign-parameters"></a><span data-ttu-id="2cd73-226">Een gepubliceerd runbook start met behulp van PowerShell-cmdlets en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-226">Start a published runbook by using PowerShell cmdlets and assign parameters</span></span>
* <span data-ttu-id="2cd73-227">**Azure Resource Manager-cmdlets:** kunt u beginnen met een Automation-runbook is gemaakt in een resourcegroep met [Start AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cd73-227">**Azure Resource Manager cmdlets:** You can start an Automation runbook that was created in a resource group by using [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx).</span></span>
  
  <span data-ttu-id="2cd73-228">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="2cd73-228">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”;”resourceGroupeName”=”WSVMClassicSG”}
  
  Start-AzureRmAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” –ResourceGroupName $resourceGroupName -Parameters $params
  ```
* <span data-ttu-id="2cd73-229">**Azure Service Management-cmdlets:** kunt u beginnen met een automation-runbook dat is gemaakt in een standaardresourcegroep met behulp van [Start AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span><span class="sxs-lookup"><span data-stu-id="2cd73-229">**Azure Service Management cmdlets:** You can start an automation runbook that was created in a default resource group by using [Start-AzureAutomationRunbook](https://msdn.microsoft.com/library/dn690259.aspx).</span></span>
  
  <span data-ttu-id="2cd73-230">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="2cd73-230">**Example:**</span></span>
  
  ```
  $params = @{“VMName”=”WSVMClassic”; ”ServiceName”=”WSVMClassicSG”}
  
  Start-AzureAutomationRunbook -AutomationAccountName “TestAutomation” -Name “Get-AzureVMGraphical” -Parameters $params
  ```

> [!NOTE]
> <span data-ttu-id="2cd73-231">Wanneer u een runbook start met behulp van PowerShell-cmdlets, een standaardparameter **MicrosoftApplicationManagementStartedBy** wordt gemaakt met de waarde Hallo **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="2cd73-231">When you start a runbook by using PowerShell cmdlets, a default parameter, **MicrosoftApplicationManagementStartedBy** is created with hello value **PowerShell**.</span></span> <span data-ttu-id="2cd73-232">U kunt deze parameter weergeven in Hallo **taakgegevens** blade.</span><span class="sxs-lookup"><span data-stu-id="2cd73-232">You can view this parameter in hello **Job details** blade.</span></span>  
> 
> 

#### <a name="start-a-runbook-by-using-an-sdk-and-assign-parameters"></a><span data-ttu-id="2cd73-233">Een runbook start met behulp van een SDK en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-233">Start a runbook by using an SDK and assign parameters</span></span>
* <span data-ttu-id="2cd73-234">**Azure Resource Manager-methode:** kunt u een runbook start met behulp van Hallo SDK van een programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="2cd73-234">**Azure Resource Manager method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="2cd73-235">Hieronder ziet u een C#-codefragment voor het starten van een runbook in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="2cd73-235">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="2cd73-236">U vindt alle Hallo-code op onze [GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="2cd73-236">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ResourceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>  
  
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
* <span data-ttu-id="2cd73-237">**Azure Service Management-methode:** kunt u een runbook start met behulp van Hallo SDK van een programmeertaal.</span><span class="sxs-lookup"><span data-stu-id="2cd73-237">**Azure Service Management method:** You can start a runbook by using hello SDK of a programming language.</span></span> <span data-ttu-id="2cd73-238">Hieronder ziet u een C#-codefragment voor het starten van een runbook in uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="2cd73-238">Below is a C# code snippet for starting a runbook in your Automation account.</span></span> <span data-ttu-id="2cd73-239">U vindt alle Hallo-code op onze [GitHub-opslagplaats](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span><span class="sxs-lookup"><span data-stu-id="2cd73-239">You can view all hello code at our [GitHub repository](https://github.com/Azure/azure-sdk-for-net/blob/master/src/ServiceManagement/Automation/Automation.Tests/TestSupport/AutomationTestBase.cs).</span></span>
  
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
  
  <span data-ttu-id="2cd73-240">toostart deze methode maakt een woordenlijst toostore hello runbook-parameters, **VMName** en **resourceGroupName**, en de bijbehorende waarden.</span><span class="sxs-lookup"><span data-stu-id="2cd73-240">toostart this method, create a dictionary toostore hello runbook parameters, **VMName** and  **resourceGroupName**, and their values.</span></span> <span data-ttu-id="2cd73-241">Hallo runbook start.</span><span class="sxs-lookup"><span data-stu-id="2cd73-241">Then start hello runbook.</span></span> <span data-ttu-id="2cd73-242">Hieronder vindt u Hallo C# codefragment voor het aanroepen van Hallo-methode die hierboven gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2cd73-242">Below is hello C# code snippet for calling hello method that's defined above.</span></span>
  
  ```
  IDictionary<string, string> RunbookParameters = new Dictionary<string, string>();
  
  // Add parameters toohello dictionary.
  RunbookParameters.Add("VMName", "WSVMClassic");
  RunbookParameters.Add("resourceGroupName", "WSSC1");
  
  //Call hello StartRunbook method with parameters
  StartRunbook(“Get-AzureVMGraphical”, RunbookParameters);
  ```

#### <a name="start-a-runbook-by-using-hello-rest-api-and-assign-parameters"></a><span data-ttu-id="2cd73-243">Een runbook start met behulp van Hallo REST-API en parameters toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-243">Start a runbook by using hello REST API and assign parameters</span></span>
<span data-ttu-id="2cd73-244">Een runbooktaak worden gemaakt en gestart met hello Azure Automation REST-API met behulp van Hallo **plaatsen** methode met de volgende Hallo URI van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="2cd73-244">A runbook job can be created and started with hello Azure Automation REST API by using hello **PUT** method with hello following request URI.</span></span>

    https://management.core.windows.net/<subscription-id>/cloudServices/<cloud-service-name>/resources/automation/~/automationAccounts/<automation-account-name>/jobs/<job-id>?api-version=2014-12-08`

<span data-ttu-id="2cd73-245">Vervang in Hallo aanvraag-URI, Hallo volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="2cd73-245">In hello request URI, replace hello following parameters:</span></span>

* <span data-ttu-id="2cd73-246">**abonnement-id:** uw Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="2cd73-246">**subscription-id:** Your Azure subscription ID.</span></span>  
* <span data-ttu-id="2cd73-247">**cloud-service-naam:** Hallo-naam van Hallo cloud toowhich Hallo serviceaanvraag moet worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="2cd73-247">**cloud-service-name:** hello name of hello cloud service toowhich hello request should be sent.</span></span>  
* <span data-ttu-id="2cd73-248">**Automation-account-name:** Hallo-naam van uw automation-account die wordt gehost binnen Hallo opgegeven cloudservice.</span><span class="sxs-lookup"><span data-stu-id="2cd73-248">**automation-account-name:** hello name of your automation account that's hosted within hello specified cloud service.</span></span>  
* <span data-ttu-id="2cd73-249">**taak-id:** hello GUID voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="2cd73-249">**job-id:** hello GUID for hello job.</span></span> <span data-ttu-id="2cd73-250">GUID's in PowerShell kunnen worden gemaakt met behulp van Hallo **[GUID]::NewGuid(). ToString()** opdracht.</span><span class="sxs-lookup"><span data-stu-id="2cd73-250">GUIDs in PowerShell can be created by using hello **[GUID]::NewGuid().ToString()** command.</span></span>

<span data-ttu-id="2cd73-251">Gebruik in volgorde toopass parameters toohello runbooktaak, Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="2cd73-251">In order toopass parameters toohello runbook job, use hello request body.</span></span> <span data-ttu-id="2cd73-252">Het duurt Hallo twee eigenschappen in JSON-indeling te volgen:</span><span class="sxs-lookup"><span data-stu-id="2cd73-252">It takes hello following two properties provided in JSON format:</span></span>

* <span data-ttu-id="2cd73-253">**Runbooknaam:** vereist.</span><span class="sxs-lookup"><span data-stu-id="2cd73-253">**Runbook name:** Required.</span></span> <span data-ttu-id="2cd73-254">Hallo de naam van Hallo runbook voor Hallo taak toostart.</span><span class="sxs-lookup"><span data-stu-id="2cd73-254">hello name of hello runbook for hello job toostart.</span></span>  
* <span data-ttu-id="2cd73-255">**Runbook-parameters:** optioneel.</span><span class="sxs-lookup"><span data-stu-id="2cd73-255">**Runbook parameters:** Optional.</span></span> <span data-ttu-id="2cd73-256">Een dictionary van parameterlijst Hallo in (naam, waarde) waar de naam moet van het type tekenreeks en de waarde is een geldig JSON-waarde opmaken.</span><span class="sxs-lookup"><span data-stu-id="2cd73-256">A dictionary of hello parameter list in (name, value) format where name should be of String type and value can be any valid JSON value.</span></span>

<span data-ttu-id="2cd73-257">Als u wilt dat toostart hello **Get-AzureVMTextual** runbook dat eerder is gemaakt met **VMName** en **resourceGroupName** gebruiken als parameters Hallo volgende JSON-indeling voor Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="2cd73-257">If you want toostart hello **Get-AzureVMTextual** runbook that was created earlier with **VMName** and **resourceGroupName** as parameters, use hello following JSON format for hello request body.</span></span>

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

<span data-ttu-id="2cd73-258">Een HTTP-statuscode 201 wordt geretourneerd als het Hallo-taak is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2cd73-258">A HTTP status code 201 is returned if hello job is successfully created.</span></span> <span data-ttu-id="2cd73-259">Raadpleeg voor meer informatie over antwoordheaders en antwoordtekst Hallo toohello artikel over het te[een runbooktaak maken met behulp van Hallo REST-API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span><span class="sxs-lookup"><span data-stu-id="2cd73-259">For more information on response headers and hello response body, refer toohello article about how too[create a runbook job by using hello REST API.](https://msdn.microsoft.com/library/azure/mt163849.aspx)</span></span>

### <a name="test-a-runbook-and-assign-parameters"></a><span data-ttu-id="2cd73-260">Een runbook testen en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-260">Test a runbook and assign parameters</span></span>
<span data-ttu-id="2cd73-261">Wanneer u [test Hallo conceptversie van uw runbook](automation-testing-runbook.md) Hallo Hallo test-optie gebruikt, **testen** blade wordt geopend en kunt u waarden voor Hallo-parameters die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2cd73-261">When you [test hello draft version of your runbook](automation-testing-runbook.md) by using hello test option, hello **Test** blade opens and you can configure values for hello parameters that you just created.</span></span>

![Testen en parameters toewijzen](media/automation-runbook-input-parameters/automation-06-testandassignparameters.png)

### <a name="link-a-schedule-tooa-runbook-and-assign-parameters"></a><span data-ttu-id="2cd73-263">Een planning tooa runbook koppelen en parameters toewijzen</span><span class="sxs-lookup"><span data-stu-id="2cd73-263">Link a schedule tooa runbook and assign parameters</span></span>
<span data-ttu-id="2cd73-264">U kunt [een planning koppelen](automation-schedules.md) tooyour runbook zodanig dat Hallo runbook wordt gestart op een bepaald tijdstip.</span><span class="sxs-lookup"><span data-stu-id="2cd73-264">You can [link a schedule](automation-schedules.md) tooyour runbook so that hello runbook starts at a specific time.</span></span> <span data-ttu-id="2cd73-265">U toewijzen invoerparameters wanneer u Hallo planning maakt en Hallo runbook deze waarden worden gebruikt wanneer deze wordt gestart door Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="2cd73-265">You assign input parameters when you create hello schedule, and hello runbook will use these values when it is started by hello schedule.</span></span> <span data-ttu-id="2cd73-266">U kunt Hallo planning niet opslaan, totdat alle verplichte parameterwaarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2cd73-266">You can’t save hello schedule until all mandatory parameter values are provided.</span></span>

![Plannen en parameters toewijzen](media/automation-runbook-input-parameters/automation-07-scheduleandassignparameters.png)

### <a name="create-a-webhook-for-a-runbook-and-assign-parameters"></a><span data-ttu-id="2cd73-268">Een webhook voor een runbook maken en toewijzen van parameters</span><span class="sxs-lookup"><span data-stu-id="2cd73-268">Create a webhook for a runbook and assign parameters</span></span>
<span data-ttu-id="2cd73-269">Kunt u een [webhook](automation-webhooks.md) voor uw runbook en invoerparameters van runbook configureren.</span><span class="sxs-lookup"><span data-stu-id="2cd73-269">You can create a [webhook](automation-webhooks.md) for your runbook and configure runbook input parameters.</span></span> <span data-ttu-id="2cd73-270">U kunt Hallo webhook niet opslaan, totdat alle verplichte parameterwaarden zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2cd73-270">You can’t save hello webhook until all mandatory parameter values are provided.</span></span>

![Webhook maken en toewijzen van parameters](media/automation-runbook-input-parameters/automation-08-createwebhookandassignparameters.png)

<span data-ttu-id="2cd73-272">Als u een runbook met behulp van een webhook uitvoert, Hallo vooraf gedefinieerde invoerparameter  **[Webhookdata](automation-webhooks.md#details-of-a-webhook)**  wordt verzonden, samen met de Hallo invoerparameters die u hebt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="2cd73-272">When you execute a runbook by using a webhook, hello predefined input parameter **[Webhookdata](automation-webhooks.md#details-of-a-webhook)** is sent, along with hello input parameters that you defined.</span></span> <span data-ttu-id="2cd73-273">U kunt klikken op tooexpand hello **WebhookData** parameter voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2cd73-273">You can click tooexpand hello **WebhookData** parameter for more details.</span></span>

![WebhookData-parameter](media/automation-runbook-input-parameters/automation-09-webhook-data-parameters.png)

## <a name="next-steps"></a><span data-ttu-id="2cd73-275">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2cd73-275">Next steps</span></span>
* <span data-ttu-id="2cd73-276">Zie voor meer informatie over runbookinvoer en uitvoer [Azure Automation: runbook invoer, uitvoer en geneste runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span><span class="sxs-lookup"><span data-stu-id="2cd73-276">For more information on runbook input and output, see [Azure Automation: runbook input, output, and nested runbooks](https://azure.microsoft.com/blog/azure-automation-runbook-input-output-and-nested-runbooks/).</span></span>
* <span data-ttu-id="2cd73-277">Zie voor meer informatie over de verschillende manieren toostart een runbook [een runbook starten](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2cd73-277">For details about different ways toostart a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="2cd73-278">tooedit tekstueel runbook te verwijzen[bewerken tekstuele runbooks](automation-edit-textual-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="2cd73-278">tooedit a textual runbook, refer too[Editing textual runbooks](automation-edit-textual-runbook.md).</span></span>
* <span data-ttu-id="2cd73-279">een grafisch runbook tooedit te verwijzen[grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="2cd73-279">tooedit a graphical runbook, refer too[Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>

