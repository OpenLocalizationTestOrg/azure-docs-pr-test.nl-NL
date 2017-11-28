---
title: Een Azure Automation-account valideren | Microsoft Docs
description: In dit artikel wordt beschreven hoe u kunt controleren of uw Automation-account juist is geconfigureerd.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: magoedte
ms.openlocfilehash: 804e05f596e1d6d5f650e4c94a18eff6b7c3ba4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="afd95-103">De verificatie van een Azure Automation Uitvoeren als-account testen</span><span class="sxs-lookup"><span data-stu-id="afd95-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="afd95-104">Nadat een Automation-account is gemaakt, kunt u een eenvoudige test uitvoeren om te controleren of u zich met het zojuist gemaakte of bijgewerkte Automation Uitvoeren als-account kunt verifiëren in Azure Resource Manager of de klassieke Azure-implementatie.</span><span class="sxs-lookup"><span data-stu-id="afd95-104">After an Automation account is successfully created, you can perform a simple test to confirm you are able to successfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="afd95-105">Automation Uitvoeren als-verificatie</span><span class="sxs-lookup"><span data-stu-id="afd95-105">Automation Run As authentication</span></span>
<span data-ttu-id="afd95-106">Gebruik de voorbeeldcode hieronder om [een PowerShell-runbook te maken](automation-creating-importing-runbook.md) om verificatie met behulp van het Uitvoeren als-account te controleren. Gebruik deze voorbeeldcode ook in de aangepaste runbooks om Resource Manager-resources te beheren met behulp van het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="afd95-106">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Run As account and also in your custom runbooks to authenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get the connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in to Azure..."
        Add-AzureRmAccount `
           -ServicePrincipal `
           -TenantId $servicePrincipalConnection.TenantId `
           -ApplicationId $servicePrincipalConnection.ApplicationId `
           -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint 
    }
    catch {
       if (!$servicePrincipalConnection)
       {
          $ErrorMessage = "Connection $connectionName not found."
          throw $ErrorMessage
      } else{
          Write-Error -Message $_.Exception
          throw $_.Exception
      }
    }

    #Get all ARM resources from all resource groups
    $ResourceGroups = Get-AzureRmResourceGroup 

    foreach ($ResourceGroup in $ResourceGroups)
    {    
       Write-Output ("Showing resources in resource group " + $ResourceGroup.ResourceGroupName)
       $Resources = Find-AzureRmResource -ResourceGroupNameContains $ResourceGroup.ResourceGroupName | Select ResourceName, ResourceType
       ForEach ($Resource in $Resources)
       {
          Write-Output ($Resource.ResourceName + " of type " +  $Resource.ResourceType)
       }
       Write-Output ("")
    } 

<span data-ttu-id="afd95-107">De cmdlet die wordt gebruikt voor verificatie in het runbook - **Add-AzureRmAccount**, gebruikt de parameterset *ServicePrincipalCertificate*.</span><span class="sxs-lookup"><span data-stu-id="afd95-107">Notice the cmdlet used for authenticating in the runbook - **Add-AzureRmAccount**, uses the *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="afd95-108">In plaats van referenties wordt voor verificatie het certificaat van de service-principal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="afd95-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="afd95-109">Wanneer u [het runbook uitvoert](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) om het Uitvoeren als-account te valideren, wordt een [runbooktaak](automation-runbook-execution.md) gemaakt, de blade Taak weergegeven en de taakstatus weergegeven in de tegel **Taaksamenvatting**.</span><span class="sxs-lookup"><span data-stu-id="afd95-109">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="afd95-110">In eerste instantie is de taakstatus *In de wachtrij geplaatst*. Hiermee wordt aangegeven dat er wordt gewacht tot in de cloud een runbook-werkrol beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="afd95-110">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="afd95-111">De taakstatus verandert daarna in *Starten* wanneer een werkrol de taak claimt en daarna in *Wordt uitgevoerd* wanneer het runbook daadwerkelijk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="afd95-111">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="afd95-112">Wanneer de runbooktaak is voltooid, is de status **Voltooid**.</span><span class="sxs-lookup"><span data-stu-id="afd95-112">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="afd95-113">Klik op de tegel **Uitvoer** als u de gedetailleerde resultaten van het runbook wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="afd95-113">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="afd95-114">Op de blade **Uitvoer** ziet u dat de verificatie is geslaagd. Er wordt ook een lijst met alle resources in alle resourcegroepen weergegeven.</span><span class="sxs-lookup"><span data-stu-id="afd95-114">On the **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="afd95-115">Vergeet niet om het codeblok dat begint met de opmerking `#Get all ARM resources from all resource groups`, te verwijderen wanneer u de code voor de runbooks hergebruikt.</span><span class="sxs-lookup"><span data-stu-id="afd95-115">Just remember to remove the block of code starting with the comment `#Get all ARM resources from all resource groups` when you reuse the code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="afd95-116">Klassieke Uitvoeren als-verificatie</span><span class="sxs-lookup"><span data-stu-id="afd95-116">Classic Run As authentication</span></span>
<span data-ttu-id="afd95-117">Gebruik de voorbeeldcode hieronder om [een PowerShell-runbook te maken](automation-creating-importing-runbook.md) om verificatie met behulp van het klassieke Uitvoeren als-account te controleren. Gebruik deze voorbeeldcode ook in de aangepaste runbooks om resources in het klassieke implementatiemodel te verifiëren en te beheren.</span><span class="sxs-lookup"><span data-stu-id="afd95-117">Use the sample code below to [create a PowerShell runbook](automation-creating-importing-runbook.md) to verify authentication using the Classic Run As account and also in your custom runbooks to authenticate and manage resources in the classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get the connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate to Azure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in the Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting the certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in the Automation account."
    }

    Write-Verbose "Authenticating to Azure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in the subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="afd95-118">Wanneer u [het runbook uitvoert](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) om het Uitvoeren als-account te valideren, wordt een [runbooktaak](automation-runbook-execution.md) gemaakt, de blade Taak weergegeven en de taakstatus weergegeven in de tegel **Taaksamenvatting**.</span><span class="sxs-lookup"><span data-stu-id="afd95-118">When you [run the runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) to validate your Run As account, a [runbook job](automation-runbook-execution.md) is created, the Job blade is displayed, and the job status displayed in the **Job Summary** tile.</span></span> <span data-ttu-id="afd95-119">In eerste instantie is de taakstatus *In de wachtrij geplaatst*. Hiermee wordt aangegeven dat er wordt gewacht tot in de cloud een runbook-werkrol beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="afd95-119">The job status will start as *Queued* indicating that it is waiting for a runbook worker in the cloud to become available.</span></span> <span data-ttu-id="afd95-120">De taakstatus verandert daarna in *Starten* wanneer een werkrol de taak claimt en daarna in *Wordt uitgevoerd* wanneer het runbook daadwerkelijk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="afd95-120">It will then move to *Starting* when a worker claims the job, and then *Running* when the runbook actually starts running.</span></span>  <span data-ttu-id="afd95-121">Wanneer de runbooktaak is voltooid, is de status **Voltooid**.</span><span class="sxs-lookup"><span data-stu-id="afd95-121">When the runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="afd95-122">Klik op de tegel **Uitvoer** als u de gedetailleerde resultaten van het runbook wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="afd95-122">To see the detailed results of the runbook, click on the **Output** tile.</span></span>  <span data-ttu-id="afd95-123">Op de blade **Uitvoer** ziet u dat de verificatie is geslaagd. Er wordt ook een lijst met alle virtuele Azure-machines die zijn geïmplementeerd in het abonnement, weergegeven op VM-naam.</span><span class="sxs-lookup"><span data-stu-id="afd95-123">On the **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="afd95-124">Vergeet niet om de cmdlet **Get-AzureVM** te verwijderen wanneer u de code voor de runbooks hergebruikt.</span><span class="sxs-lookup"><span data-stu-id="afd95-124">Just remember to remove the cmdlet **Get-AzureVM** when you reuse the code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afd95-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="afd95-125">Next steps</span></span>
* <span data-ttu-id="afd95-126">Zie [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md) om aan de slag te gaan met PowerShell-runbooks.</span><span class="sxs-lookup"><span data-stu-id="afd95-126">To get started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="afd95-127">Zie voor meer informatie over grafisch ontwerpen [Grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="afd95-127">To learn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
