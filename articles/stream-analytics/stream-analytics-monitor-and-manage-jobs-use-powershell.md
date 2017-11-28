---
title: aaaMonitor en beheren van Stream Analytics-taken met PowerShell | Microsoft Docs
description: Meer informatie over hoe de Azure PowerShell-cmdlets en toomonitor toouse en Stream Analytics-taken beheren.
keywords: Azure powershell, azure powershell-cmdlets, powershell-opdracht powershell-scripts
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 514f454e-d18c-4081-8304-ab48577e15e8
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 44abc82f1c44a5ebc1701badd6547b84dac239b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-stream-analytics-jobs-with-azure-powershell-cmdlets"></a><span data-ttu-id="eac1c-104">Bewaken en beheren van de Stream Analytics-taken met Azure PowerShell-cmdlets</span><span class="sxs-lookup"><span data-stu-id="eac1c-104">Monitor and manage Stream Analytics jobs with Azure PowerShell cmdlets</span></span>
<span data-ttu-id="eac1c-105">Meer informatie over hoe toomonitor Stream Analytics-resources met Azure PowerShell-cmdlets en powershell-scripts die basic Stream Analytics-taken uitvoeren en beheren.</span><span class="sxs-lookup"><span data-stu-id="eac1c-105">Learn how toomonitor and manage Stream Analytics resources with Azure PowerShell cmdlets and powershell scripting that execute basic Stream Analytics tasks.</span></span>

## <a name="prerequisites-for-running-azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="eac1c-106">Vereisten voor het uitvoeren van Azure PowerShell-cmdlets voor Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eac1c-106">Prerequisites for running Azure PowerShell cmdlets for Stream Analytics</span></span>
* <span data-ttu-id="eac1c-107">Maak een Azure-resourcegroep in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="eac1c-107">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="eac1c-108">Hallo Hieronder volgt een voorbeeld Azure PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="eac1c-108">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="eac1c-109">Zie voor informatie Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="eac1c-109">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

<span data-ttu-id="eac1c-110">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-110">Azure PowerShell 0.9.8:</span></span>  

         # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group if you have more than one subscription on your account.
        Select-AzureSubscription -SubscriptionName <subscription name>

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>

<span data-ttu-id="eac1c-111">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-111">Azure PowerShell 1.0:</span></span>  

         # Log in tooyour Azure account
        Login-AzureRmAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group.
        Get-AzureRmSubscription –SubscriptionName “your sub” | Select-AzureRmSubscription

        # If Stream Analytics has not been registered toohello subscription, remove remark symbol below (#) toorun hello Register-AzureProvider cmdlet tooregister hello provider namespace.
        #Register-AzureRmResourceProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureRMResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>



> [!NOTE]
> <span data-ttu-id="eac1c-112">Stream Analytics-taken via een programma gemaakt beschikt niet over bewaking standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="eac1c-112">Stream Analytics jobs created programmatically do not have monitoring enabled by default.</span></span>  <span data-ttu-id="eac1c-113">U kunt handmatig inschakelen voor bewaking in hello Azure-Portal door te navigeren pagina van de Monitor van toohello taak en klikt u op de knop inschakelen Hallo of u kunt hiervoor programmatisch Hallo stappen volgt zich bevindt op [Azure Stream Analytics - stroom van de Monitor Analytics-taken via programmacode](stream-analytics-monitor-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="eac1c-113">You can manually enable monitoring in hello Azure Portal by navigating toohello job’s Monitor page and clicking hello Enable button or you can do this programmatically by following hello steps located at [Azure Stream Analytics - Monitor Stream Analytics Jobs Programatically](stream-analytics-monitor-jobs.md).</span></span>
> 
> 

## <a name="azure-powershell-cmdlets-for-stream-analytics"></a><span data-ttu-id="eac1c-114">Azure PowerShell-cmdlets voor Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eac1c-114">Azure PowerShell cmdlets for Stream Analytics</span></span>
<span data-ttu-id="eac1c-115">Hallo volgende Azure PowerShell-cmdlets worden gebruikte toomonitor en Azure Stream Analytics-taken beheren.</span><span class="sxs-lookup"><span data-stu-id="eac1c-115">hello following Azure PowerShell cmdlets can be used toomonitor and manage Azure Stream Analytics jobs.</span></span> <span data-ttu-id="eac1c-116">Houd er rekening mee dat Azure PowerShell verschillende versies heeft.</span><span class="sxs-lookup"><span data-stu-id="eac1c-116">Note that Azure PowerShell has different versions.</span></span> 
<span data-ttu-id="eac1c-117">**In de eerste opdracht vermelde Hallo voor Azure PowerShell 0.9.8 is Hallo voorbeelden is de tweede opdracht Hallo voor Azure PowerShell 1.0.**</span><span class="sxs-lookup"><span data-stu-id="eac1c-117">**In hello examples listed hello first command is for Azure PowerShell 0.9.8, hello second command is for Azure PowerShell 1.0.**</span></span> <span data-ttu-id="eac1c-118">Hello Azure PowerShell 1.0 opdrachten hebben altijd 'AzureRM' in Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="eac1c-118">hello Azure PowerShell 1.0 commands will always have "AzureRM" in hello command.</span></span>

### <a name="get-azurestreamanalyticsjob--get-azurermstreamanalyticsjob"></a><span data-ttu-id="eac1c-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="eac1c-119">Get-AzureStreamAnalyticsJob | Get-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="eac1c-120">Informatie over de taak over een specifieke taak in de resourcegroep opgehaald of een lijst met alle Stream Analytics-taken in hello Azure-abonnement of de opgegeven resourcegroep is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="eac1c-120">Lists all Stream Analytics jobs defined in hello Azure subscription or specified resource group, or gets job information about a specific job within a resource group.</span></span>

<span data-ttu-id="eac1c-121">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-121">**Example 1**</span></span>

<span data-ttu-id="eac1c-122">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-122">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob

<span data-ttu-id="eac1c-123">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-123">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob

<span data-ttu-id="eac1c-124">Deze PowerShell-opdracht retourneert informatie over alle Hallo Stream Analytics-taken in hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="eac1c-124">This PowerShell command returns information about all hello Stream Analytics jobs in hello Azure subscription.</span></span>

<span data-ttu-id="eac1c-125">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-125">**Example 2**</span></span>

<span data-ttu-id="eac1c-126">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-126">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="eac1c-127">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-127">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US 

<span data-ttu-id="eac1c-128">Deze PowerShell-opdracht retourneert informatie over alle Hallo Stream Analytics-taken in de resourcegroep Hallo StreamAnalytics, standaard, centraal, VS.</span><span class="sxs-lookup"><span data-stu-id="eac1c-128">This PowerShell command returns information about all hello Stream Analytics jobs in hello resource group StreamAnalytics-Default-Central-US.</span></span>

<span data-ttu-id="eac1c-129">**Voorbeeld 3**</span><span class="sxs-lookup"><span data-stu-id="eac1c-129">**Example 3**</span></span>

<span data-ttu-id="eac1c-130">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-130">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="eac1c-131">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-131">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob

<span data-ttu-id="eac1c-132">Deze PowerShell-opdracht retourneert informatie over Hallo Stream Analytics-taak StreamingJob in de resourcegroep Hallo StreamAnalytics, standaard, centraal, VS.</span><span class="sxs-lookup"><span data-stu-id="eac1c-132">This PowerShell command returns information about hello Stream Analytics job StreamingJob in hello resource group StreamAnalytics-Default-Central-US.</span></span>

### <a name="get-azurestreamanalyticsinput--get-azurermstreamanalyticsinput"></a><span data-ttu-id="eac1c-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="eac1c-133">Get-AzureStreamAnalyticsInput | Get-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="eac1c-134">Geeft een lijst van alle Hallo invoerwaarden die zijn gedefinieerd in een opgegeven Stream Analytics-taak of informatie ophalen over een specifieke invoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-134">Lists all of hello inputs that are defined in a specified Stream Analytics job, or gets information about a specific input.</span></span>

<span data-ttu-id="eac1c-135">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-135">**Example 1**</span></span>

<span data-ttu-id="eac1c-136">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-136">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="eac1c-137">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-137">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="eac1c-138">Deze PowerShell-opdracht retourneert informatie over alle Hallo invoer in Hallo taak StreamingJob gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="eac1c-138">This PowerShell command returns information about all hello inputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="eac1c-139">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-139">**Example 2**</span></span>

<span data-ttu-id="eac1c-140">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-140">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="eac1c-141">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-141">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name EntryStream

<span data-ttu-id="eac1c-142">Deze PowerShell-opdracht retourneert informatie over Hallo invoer met de naam gedefinieerd in taak Hallo StreamingJob EntryStream.</span><span class="sxs-lookup"><span data-stu-id="eac1c-142">This PowerShell command returns information about hello input named EntryStream defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsoutput--get-azurermstreamanalyticsoutput"></a><span data-ttu-id="eac1c-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="eac1c-143">Get-AzureStreamAnalyticsOutput | Get-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="eac1c-144">Informatie over een specifieke uitvoer opgehaald of een lijst met alle Hallo-uitvoer die zijn gedefinieerd in een opgegeven Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="eac1c-144">Lists all of hello outputs that are defined in a specified Stream Analytics job, or gets information about a specific output.</span></span>

<span data-ttu-id="eac1c-145">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-145">**Example 1**</span></span>

<span data-ttu-id="eac1c-146">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-146">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="eac1c-147">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-147">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob

<span data-ttu-id="eac1c-148">Deze PowerShell-opdracht retourneert informatie over het Hallo-uitvoer in Hallo taak StreamingJob gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="eac1c-148">This PowerShell command returns information about hello outputs defined in hello job StreamingJob.</span></span>

<span data-ttu-id="eac1c-149">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-149">**Example 2**</span></span>

<span data-ttu-id="eac1c-150">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-150">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="eac1c-151">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-151">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name Output

<span data-ttu-id="eac1c-152">Deze PowerShell-opdracht retourneert informatie over het Hallo-uitvoer met de naam gedefinieerd in taak Hallo StreamingJob uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-152">This PowerShell command returns information about hello output named Output defined in hello job StreamingJob.</span></span>

### <a name="get-azurestreamanalyticsquota--get-azurermstreamanalyticsquota"></a><span data-ttu-id="eac1c-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span><span class="sxs-lookup"><span data-stu-id="eac1c-153">Get-AzureStreamAnalyticsQuota | Get-AzureRMStreamAnalyticsQuota</span></span>
<span data-ttu-id="eac1c-154">Hiermee haalt u informatie over Hallo quotum van het streaming-eenheden in een opgegeven regio.</span><span class="sxs-lookup"><span data-stu-id="eac1c-154">Gets information about hello quota of streaming units in a specified region.</span></span>

<span data-ttu-id="eac1c-155">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-155">**Example 1**</span></span>

<span data-ttu-id="eac1c-156">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-156">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="eac1c-157">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-157">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsQuota –Location "Central US" 

<span data-ttu-id="eac1c-158">Deze PowerShell-opdracht retourneert informatie over het Hallo-quota en het gebruik van streaming-eenheden in de regio VS-midden Hallo.</span><span class="sxs-lookup"><span data-stu-id="eac1c-158">This PowerShell command returns information about hello quota and usage of streaming units in hello Central US region.</span></span>

### <a name="get-azurestreamanalyticstransformation--getazurermstreamanalyticstransformation"></a><span data-ttu-id="eac1c-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="eac1c-159">Get-AzureStreamAnalyticsTransformation | GetAzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="eac1c-160">Hiermee haalt u informatie over een specifieke transformatie gedefinieerd in een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="eac1c-160">Gets information about a specific transformation defined in a Stream Analytics job.</span></span>

<span data-ttu-id="eac1c-161">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-161">**Example 1**</span></span>

<span data-ttu-id="eac1c-162">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-162">Azure PowerShell 0.9.8:</span></span>  

    Get-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="eac1c-163">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-163">Azure PowerShell 1.0:</span></span>  

    Get-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –Name StreamingJob

<span data-ttu-id="eac1c-164">Deze PowerShell-opdracht retourneert informatie over Hallo transformatie StreamingJob in Hallo taak StreamingJob aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eac1c-164">This PowerShell command returns information about hello transformation called StreamingJob in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsinput--new-azurermstreamanalyticsinput"></a><span data-ttu-id="eac1c-165">Nieuwe AzureStreamAnalyticsInput | Nieuwe AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="eac1c-165">New-AzureStreamAnalyticsInput | New-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="eac1c-166">Maakt u een nieuwe invoer binnen een Stream Analytics-taak of updates van een bestaande opgegeven invoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-166">Creates a new input within a Stream Analytics job, or updates an existing specified input.</span></span>

<span data-ttu-id="eac1c-167">Hallo kan naam van Hallo invoer worden opgegeven in Hallo .json-bestand of op Hallo vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="eac1c-167">hello name of hello input can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="eac1c-168">Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.</span><span class="sxs-lookup"><span data-stu-id="eac1c-168">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="eac1c-169">Als u opgeeft dat al bestaat invoer en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande invoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-169">If you specify an input that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing input.</span></span>

<span data-ttu-id="eac1c-170">Als u opgeeft Hallo – Force-parameter en geef een bestaande naam invoeren, Hallo invoer worden vervangen zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-170">If you specify hello –Force parameter and specify an existing input name, hello input will be replaced without confirmation.</span></span>

<span data-ttu-id="eac1c-171">Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [maken invoer (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-input] sectie Hallo [Stream Analytics Management REST-API Referentiebibliotheek][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="eac1c-171">For detailed information on hello JSON file structure and contents, refer toohello [Create Input (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-input] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="eac1c-172">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-172">**Example 1**</span></span>

<span data-ttu-id="eac1c-173">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-173">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="eac1c-174">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-174">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" 

<span data-ttu-id="eac1c-175">Deze PowerShell-opdracht maakt een nieuwe invoer van Hallo bestand Input.json.</span><span class="sxs-lookup"><span data-stu-id="eac1c-175">This PowerShell command creates a new input from hello file Input.json.</span></span> <span data-ttu-id="eac1c-176">Als een bestaande invoer met Hallo naam die is opgegeven in de invoer definitiebestand Hallo al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.</span><span class="sxs-lookup"><span data-stu-id="eac1c-176">If an existing input with hello name specified in hello input definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="eac1c-177">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-177">**Example 2**</span></span>

<span data-ttu-id="eac1c-178">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-178">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="eac1c-179">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-179">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream

<span data-ttu-id="eac1c-180">Deze PowerShell-opdracht maakt een nieuwe invoer in Hallo taak EntryStream aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eac1c-180">This PowerShell command creates a new input in hello job called EntryStream.</span></span> <span data-ttu-id="eac1c-181">Als een bestaande invoer met deze naam al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.</span><span class="sxs-lookup"><span data-stu-id="eac1c-181">If an existing input with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="eac1c-182">**Voorbeeld 3**</span><span class="sxs-lookup"><span data-stu-id="eac1c-182">**Example 3**</span></span>

<span data-ttu-id="eac1c-183">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-183">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="eac1c-184">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-184">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US -JobName StreamingJob –File "C:\Input.json" –Name EntryStream -Force

<span data-ttu-id="eac1c-185">Deze PowerShell-opdracht vervangt Hallo definitie van Hallo bestaande invoerbron EntryStream aangeroepen met Hallo definitie uit het Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="eac1c-185">This PowerShell command replaces hello definition of hello existing input source called EntryStream with hello definition from hello file.</span></span>

### <a name="new-azurestreamanalyticsjob--new-azurermstreamanalyticsjob"></a><span data-ttu-id="eac1c-186">Nieuwe AzureStreamAnalyticsJob | Nieuwe AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="eac1c-186">New-AzureStreamAnalyticsJob | New-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="eac1c-187">Maakt een nieuwe Stream Analytics-taak in Microsoft Azure of updates Hallo definitie van een bestaande opgegeven taak.</span><span class="sxs-lookup"><span data-stu-id="eac1c-187">Creates a new Stream Analytics job in Microsoft Azure, or updates hello definition of an existing specified job.</span></span>

<span data-ttu-id="eac1c-188">Hallo-naam van Hallo taak kan worden opgegeven in Hallo .json-bestand of op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="eac1c-188">hello name of hello job can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="eac1c-189">Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.</span><span class="sxs-lookup"><span data-stu-id="eac1c-189">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="eac1c-190">Als u een taaknaam opgeeft die al bestaat en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande taak.</span><span class="sxs-lookup"><span data-stu-id="eac1c-190">If you specify a job name that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing job.</span></span>

<span data-ttu-id="eac1c-191">Als u opgeeft Hallo – Force-parameter en geef de taaknaam van een bestaande, wordt de taakdefinitie Hallo vervangen zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-191">If you specify hello –Force parameter and specify an existing job name, hello job definition will be replaced without confirmation.</span></span>

<span data-ttu-id="eac1c-192">Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [Stream Analytics-taak maken] [ msdn-rest-api-create-stream-analytics-job] sectie Hallo [Stream Analytics Management REST API-verwijzing Bibliotheek][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="eac1c-192">For detailed information on hello JSON file structure and contents, refer toohello [Create Stream Analytics Job][msdn-rest-api-create-stream-analytics-job] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="eac1c-193">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-193">**Example 1**</span></span>

<span data-ttu-id="eac1c-194">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-194">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="eac1c-195">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-195">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" 

<span data-ttu-id="eac1c-196">Deze PowerShell-opdracht maakt een nieuwe taak van Hallo definitie in JobDefinition.json.</span><span class="sxs-lookup"><span data-stu-id="eac1c-196">This PowerShell command creates a new job from hello definition in JobDefinition.json.</span></span> <span data-ttu-id="eac1c-197">Als een bestaande taak met opgegeven in het bestand taak Hallo Hallo-naam al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.</span><span class="sxs-lookup"><span data-stu-id="eac1c-197">If an existing job with hello name specified in hello job definition file is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="eac1c-198">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-198">**Example 2**</span></span>

<span data-ttu-id="eac1c-199">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-199">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="eac1c-200">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-200">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\JobDefinition.json" –Name StreamingJob -Force

<span data-ttu-id="eac1c-201">Deze PowerShell-opdracht vervangt de taakdefinitie Hallo voor StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="eac1c-201">This PowerShell command replaces hello job definition for StreamingJob.</span></span>

### <a name="new-azurestreamanalyticsoutput--new-azurermstreamanalyticsoutput"></a><span data-ttu-id="eac1c-202">Nieuwe AzureStreamAnalyticsOutput | Nieuwe AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="eac1c-202">New-AzureStreamAnalyticsOutput | New-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="eac1c-203">Maakt een nieuwe uitvoer binnen een Stream Analytics-taak of een bestaande uitvoer-updates.</span><span class="sxs-lookup"><span data-stu-id="eac1c-203">Creates a new output within a Stream Analytics job, or updates an existing output.</span></span>  

<span data-ttu-id="eac1c-204">Hallo-naam van Hallo uitvoer kan worden opgegeven op Hallo vanaf de opdrachtregel of Hallo .json-bestand.</span><span class="sxs-lookup"><span data-stu-id="eac1c-204">hello name of hello output can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="eac1c-205">Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.</span><span class="sxs-lookup"><span data-stu-id="eac1c-205">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="eac1c-206">Als u opgeeft een uitvoer die al bestaat en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-206">If you specify an output that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing output.</span></span>

<span data-ttu-id="eac1c-207">Als u opgeeft Hallo – Force-parameter en geef de naam van een bestaande uitvoer, Hallo uitvoer worden vervangen zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-207">If you specify hello –Force parameter and specify an existing output name, hello output will be replaced without confirmation.</span></span>

<span data-ttu-id="eac1c-208">Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [uitvoer maken (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-output] sectie Hallo [Stream Analytics Management REST-API Referentiebibliotheek][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="eac1c-208">For detailed information on hello JSON file structure and contents, refer toohello [Create Output (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-output] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="eac1c-209">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-209">**Example 1**</span></span>

<span data-ttu-id="eac1c-210">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-210">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="eac1c-211">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-211">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output

<span data-ttu-id="eac1c-212">Deze PowerShell-opdracht maakt u een nieuwe uitvoer 'uitvoer' hello taak StreamingJob aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eac1c-212">This PowerShell command creates a new output called "output" in hello job StreamingJob.</span></span> <span data-ttu-id="eac1c-213">Als een bestaande uitvoer met deze naam al is gedefinieerd, wordt u gevraagd Hallo cmdlet of tooreplace deze.</span><span class="sxs-lookup"><span data-stu-id="eac1c-213">If an existing output with this name is already defined, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="eac1c-214">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-214">**Example 2**</span></span>

<span data-ttu-id="eac1c-215">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-215">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="eac1c-216">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-216">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Output.json" –JobName StreamingJob –Name output -Force

<span data-ttu-id="eac1c-217">Deze PowerShell-opdracht vervangt Hallo definitie voor 'uitvoer' hello taak StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="eac1c-217">This PowerShell command replaces hello definition for "output" in hello job StreamingJob.</span></span>

### <a name="new-azurestreamanalyticstransformation--new-azurermstreamanalyticstransformation"></a><span data-ttu-id="eac1c-218">Nieuwe AzureStreamAnalyticsTransformation | Nieuwe AzureRMStreamAnalyticsTransformation</span><span class="sxs-lookup"><span data-stu-id="eac1c-218">New-AzureStreamAnalyticsTransformation | New-AzureRMStreamAnalyticsTransformation</span></span>
<span data-ttu-id="eac1c-219">Maakt u een nieuwe transformatie binnen een Stream Analytics-taak of Hallo bestaande transformatie-updates.</span><span class="sxs-lookup"><span data-stu-id="eac1c-219">Creates a new transformation within a Stream Analytics job, or updates hello existing transformation.</span></span>

<span data-ttu-id="eac1c-220">Hallo-naam van Hallo transformatie kan worden opgegeven in Hallo .json-bestand of op Hallo vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="eac1c-220">hello name of hello transformation can be specified in hello .json file or on hello command line.</span></span> <span data-ttu-id="eac1c-221">Als beide worden opgegeven, moet Hallo-naam op de opdrachtregel Hallo hetzelfde als Hallo in Hallo-bestand worden Hallo.</span><span class="sxs-lookup"><span data-stu-id="eac1c-221">If both are specified, hello name on hello command line must be hello same as hello one in hello file.</span></span>

<span data-ttu-id="eac1c-222">Als u opgeeft dat al bestaat de transformatie en geef geen hello – Force-parameter Hallo cmdlet wordt u gevraagd of tooreplace Hallo bestaande transformatie.</span><span class="sxs-lookup"><span data-stu-id="eac1c-222">If you specify a transformation that already exists and do not specify hello –Force parameter, hello cmdlet will ask whether or not tooreplace hello existing transformation.</span></span>

<span data-ttu-id="eac1c-223">Als u opgeeft Hallo – Force-parameter en geef de naam van een bestaande transformatie, Hallo transformatie worden vervangen zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-223">If you specify hello –Force parameter and specify an existing transformation name, hello transformation will be replaced without confirmation.</span></span>

<span data-ttu-id="eac1c-224">Raadpleeg voor gedetailleerde informatie over Hallo JSON-bestandsstructuur en inhoud toohello [transformatie maken (Azure Stream Analytics)] [ msdn-rest-api-create-stream-analytics-transformation] sectie Hallo [Stream Analytics Management REST-API-referentiebibliotheek][stream.analytics.rest.api.reference].</span><span class="sxs-lookup"><span data-stu-id="eac1c-224">For detailed information on hello JSON file structure and contents, refer toohello [Create Transformation (Azure Stream Analytics)][msdn-rest-api-create-stream-analytics-transformation] section of hello [Stream Analytics Management REST API Reference Library][stream.analytics.rest.api.reference].</span></span>

<span data-ttu-id="eac1c-225">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-225">**Example 1**</span></span>

<span data-ttu-id="eac1c-226">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-226">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="eac1c-227">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-227">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform

<span data-ttu-id="eac1c-228">Deze PowerShell-opdracht maakt een nieuwe transformatie StreamingJobTransform in Hallo taak StreamingJob aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="eac1c-228">This PowerShell command creates a new transformation called StreamingJobTransform in hello job StreamingJob.</span></span> <span data-ttu-id="eac1c-229">Als is al een bestaande transformatie gedefinieerd met deze naam, wordt u gevraagd Hallo cmdlet of tooreplace deze.</span><span class="sxs-lookup"><span data-stu-id="eac1c-229">If an existing transformation is already defined with this name, hello cmdlet will ask whether or not tooreplace it.</span></span>

<span data-ttu-id="eac1c-230">**Voorbeeld 2**</span><span class="sxs-lookup"><span data-stu-id="eac1c-230">**Example 2**</span></span>

<span data-ttu-id="eac1c-231">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-231">Azure PowerShell 0.9.8:</span></span>  

    New-AzureStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

<span data-ttu-id="eac1c-232">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-232">Azure PowerShell 1.0:</span></span>  

    New-AzureRMStreamAnalyticsTransformation -ResourceGroupName StreamAnalytics-Default-Central-US –File "C:\Transformation.json" –JobName StreamingJob –Name StreamingJobTransform -Force

 <span data-ttu-id="eac1c-233">Deze PowerShell-opdracht vervangt Hallo definitie van StreamingJobTransform in Hallo taak StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="eac1c-233">This PowerShell command replaces hello definition of StreamingJobTransform in hello job StreamingJob.</span></span>

### <a name="remove-azurestreamanalyticsinput--remove-azurermstreamanalyticsinput"></a><span data-ttu-id="eac1c-234">Verwijder AzureStreamAnalyticsInput | Verwijder AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="eac1c-234">Remove-AzureStreamAnalyticsInput | Remove-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="eac1c-235">Een specifieke invoer wordt asynchroon worden verwijderd uit een Stream Analytics-taak in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eac1c-235">Asynchronously deletes a specific input from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="eac1c-236">Als u opgeeft hello – Force parameter Hallo invoer worden verwijderd zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-236">If you specify hello –Force parameter, hello input will be deleted without confirmation.</span></span>

<span data-ttu-id="eac1c-237">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-237">**Example 1**</span></span>

<span data-ttu-id="eac1c-238">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-238">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="eac1c-239">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-239">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EventStream

<span data-ttu-id="eac1c-240">Deze PowerShell-opdracht verwijdert Hallo invoer EventStream in Hallo taak StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="eac1c-240">This PowerShell command removes hello input EventStream in hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsjob--remove-azurermstreamanalyticsjob"></a><span data-ttu-id="eac1c-241">Verwijder AzureStreamAnalyticsJob | Verwijder AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="eac1c-241">Remove-AzureStreamAnalyticsJob | Remove-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="eac1c-242">Asynchroon Hiermee verwijdert u een specifieke Stream Analytics-taak in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eac1c-242">Asynchronously deletes a specific Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="eac1c-243">Als u opgeeft hello – Force-parameter Hallo taak zal worden verwijderd zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-243">If you specify hello –Force parameter, hello job will be deleted without confirmation.</span></span>

<span data-ttu-id="eac1c-244">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-244">**Example 1**</span></span>

<span data-ttu-id="eac1c-245">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-245">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="eac1c-246">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-246">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="eac1c-247">Deze PowerShell-opdracht verwijdert Hallo taak StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="eac1c-247">This PowerShell command removes hello job StreamingJob.</span></span>  

### <a name="remove-azurestreamanalyticsoutput--remove-azurermstreamanalyticsoutput"></a><span data-ttu-id="eac1c-248">Verwijder AzureStreamAnalyticsOutput | Verwijder AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="eac1c-248">Remove-AzureStreamAnalyticsOutput | Remove-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="eac1c-249">Een specifieke uitvoer wordt asynchroon worden verwijderd uit een Stream Analytics-taak in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eac1c-249">Asynchronously deletes a specific output from a Stream Analytics job in Microsoft Azure.</span></span>  
<span data-ttu-id="eac1c-250">Als u opgeeft hello – Force parameter Hallo uitvoer worden verwijderd zonder bevestiging.</span><span class="sxs-lookup"><span data-stu-id="eac1c-250">If you specify hello –Force parameter, hello output will be deleted without confirmation.</span></span>

<span data-ttu-id="eac1c-251">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-251">**Example 1**</span></span>

<span data-ttu-id="eac1c-252">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-252">Azure PowerShell 0.9.8:</span></span>  

    Remove-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="eac1c-253">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-253">Azure PowerShell 1.0:</span></span>  

    Remove-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="eac1c-254">Deze PowerShell-opdracht verwijdert Hallo uitvoer in Hallo taak StreamingJob uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-254">This PowerShell command removes hello output Output in hello job StreamingJob.</span></span>  

### <a name="start-azurestreamanalyticsjob--start-azurermstreamanalyticsjob"></a><span data-ttu-id="eac1c-255">Start AzureStreamAnalyticsJob | Start AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="eac1c-255">Start-AzureStreamAnalyticsJob | Start-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="eac1c-256">Asynchroon implementeert en een Stream Analytics-taak start in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="eac1c-256">Asynchronously deploys and starts a Stream Analytics job in Microsoft Azure.</span></span>

<span data-ttu-id="eac1c-257">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-257">**Example 1**</span></span>

<span data-ttu-id="eac1c-258">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-258">Azure PowerShell 0.9.8:</span></span>  

    Start-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="eac1c-259">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-259">Azure PowerShell 1.0:</span></span>  

    Start-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US -Name StreamingJob -OutputStartMode CustomTime -OutputStartTime 2012-12-12T12:12:12Z

<span data-ttu-id="eac1c-260">Deze PowerShell-opdracht wordt gestart Hallo taak StreamingJob met een begintijd aangepaste uitvoer ingesteld tooDecember 12, 2012 12:12:12 UTC.</span><span class="sxs-lookup"><span data-stu-id="eac1c-260">This PowerShell command starts hello job StreamingJob with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC.</span></span>

### <a name="stop-azurestreamanalyticsjob--stop-azurermstreamanalyticsjob"></a><span data-ttu-id="eac1c-261">Stop AzureStreamAnalyticsJob | Stop AzureRMStreamAnalyticsJob</span><span class="sxs-lookup"><span data-stu-id="eac1c-261">Stop-AzureStreamAnalyticsJob | Stop-AzureRMStreamAnalyticsJob</span></span>
<span data-ttu-id="eac1c-262">Asynchroon stopt een Stream Analytics-taak wordt uitgevoerd in Microsoft Azure en ongedaan wijst bronnen toe die zijn die zijn gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eac1c-262">Asynchronously stops a Stream Analytics job from running in Microsoft Azure and de-allocates resources that were that were being used.</span></span> <span data-ttu-id="eac1c-263">Hallo blijven taakdefinitie en metagegevens beschikbaar in uw abonnement via hello Azure-portal en API's zodanig dat hello taak kan worden bewerkt en opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="eac1c-263">hello job definition and metadata will remain available within your subscription through both hello Azure portal and management APIs, such that hello job can be edited and restarted.</span></span> <span data-ttu-id="eac1c-264">U wordt niet in rekening gebracht voor een taak gestopt Hallo status heeft.</span><span class="sxs-lookup"><span data-stu-id="eac1c-264">You will not be charged for a job in hello stopped state.</span></span>

<span data-ttu-id="eac1c-265">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-265">**Example 1**</span></span>

<span data-ttu-id="eac1c-266">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-266">Azure PowerShell 0.9.8:</span></span>  

    Stop-AzureStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="eac1c-267">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-267">Azure PowerShell 1.0:</span></span>  

    Stop-AzureRMStreamAnalyticsJob -ResourceGroupName StreamAnalytics-Default-Central-US –Name StreamingJob 

<span data-ttu-id="eac1c-268">Deze PowerShell-opdracht stopt Hallo taak StreamingJob.</span><span class="sxs-lookup"><span data-stu-id="eac1c-268">This PowerShell command stops hello job StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsinput--test-azurermstreamanalyticsinput"></a><span data-ttu-id="eac1c-269">Test AzureStreamAnalyticsInput | Test AzureRMStreamAnalyticsInput</span><span class="sxs-lookup"><span data-stu-id="eac1c-269">Test-AzureStreamAnalyticsInput | Test-AzureRMStreamAnalyticsInput</span></span>
<span data-ttu-id="eac1c-270">Tests Hallo mogelijkheid van Stream Analytics tooconnect tooa opgegeven invoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-270">Tests hello ability of Stream Analytics tooconnect tooa specified input.</span></span>

<span data-ttu-id="eac1c-271">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-271">**Example 1**</span></span>

<span data-ttu-id="eac1c-272">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-272">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="eac1c-273">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-273">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsInput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name EntryStream

<span data-ttu-id="eac1c-274">Deze verbindingsstatus van PowerShell-opdracht tests Hallo Hallo EntryStream in StreamingJob invoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-274">This PowerShell command tests hello connection status of hello input EntryStream in StreamingJob.</span></span>  

### <a name="test-azurestreamanalyticsoutput--test-azurermstreamanalyticsoutput"></a><span data-ttu-id="eac1c-275">Test AzureStreamAnalyticsOutput | Test AzureRMStreamAnalyticsOutput</span><span class="sxs-lookup"><span data-stu-id="eac1c-275">Test-AzureStreamAnalyticsOutput | Test-AzureRMStreamAnalyticsOutput</span></span>
<span data-ttu-id="eac1c-276">Tests Hallo mogelijkheid van Stream Analytics tooconnect tooa opgegeven uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-276">Tests hello ability of Stream Analytics tooconnect tooa specified output.</span></span>

<span data-ttu-id="eac1c-277">**Voorbeeld 1**</span><span class="sxs-lookup"><span data-stu-id="eac1c-277">**Example 1**</span></span>

<span data-ttu-id="eac1c-278">Azure PowerShell 0.9.8:</span><span class="sxs-lookup"><span data-stu-id="eac1c-278">Azure PowerShell 0.9.8:</span></span>  

    Test-AzureStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="eac1c-279">Azure PowerShell 1.0:</span><span class="sxs-lookup"><span data-stu-id="eac1c-279">Azure PowerShell 1.0:</span></span>  

    Test-AzureRMStreamAnalyticsOutput -ResourceGroupName StreamAnalytics-Default-Central-US –JobName StreamingJob –Name Output

<span data-ttu-id="eac1c-280">Deze verbindingsstatus van PowerShell-opdracht tests Hallo Hallo uitvoer in StreamingJob uitvoer.</span><span class="sxs-lookup"><span data-stu-id="eac1c-280">This PowerShell command tests hello connection status of hello output Output in StreamingJob.</span></span>  

## <a name="get-support"></a><span data-ttu-id="eac1c-281">Ondersteuning krijgen</span><span class="sxs-lookup"><span data-stu-id="eac1c-281">Get support</span></span>
<span data-ttu-id="eac1c-282">Voor verdere hulp kunt u proberen onze [Azure Stream Analytics-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="eac1c-282">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="eac1c-283">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eac1c-283">Next steps</span></span>
* [<span data-ttu-id="eac1c-284">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eac1c-284">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="eac1c-285">Aan de slag met Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="eac1c-285">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="eac1c-286">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="eac1c-286">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="eac1c-287">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="eac1c-287">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="eac1c-288">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="eac1c-288">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[msdn-switch-azuremode]: http://msdn.microsoft.com/library/dn722470.aspx
[powershell-install]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
[msdn-rest-api-create-stream-analytics-job]: https://msdn.microsoft.com/library/dn834994.aspx
[msdn-rest-api-create-stream-analytics-input]: https://msdn.microsoft.com/library/dn835010.aspx
[msdn-rest-api-create-stream-analytics-output]: https://msdn.microsoft.com/library/dn835015.aspx
[msdn-rest-api-create-stream-analytics-transformation]: https://msdn.microsoft.com/library/dn835007.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

