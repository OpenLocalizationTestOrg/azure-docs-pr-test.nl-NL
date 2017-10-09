---
title: configuratie van aaaValidate Azure Automation-account | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooconfirm Hallo configuratie van uw Automation-account juist is geconfigureerd.
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
ms.openlocfilehash: 3a990dcc6661cf67c4b62592ce03d55a3791053a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-automation-run-as-account-authentication"></a><span data-ttu-id="4745f-103">De verificatie van een Azure Automation Uitvoeren als-account testen</span><span class="sxs-lookup"><span data-stu-id="4745f-103">Test Azure Automation Run As account authentication</span></span>
<span data-ttu-id="4745f-104">Nadat een Automation-account is gemaakt, kunt u een eenvoudige test tooconfirm kunt uitvoeren toosuccessfully zich verifiëren bij Azure Resource Manager of Azure-klassieke implementatie met behulp van uw nieuwe of bijgewerkte Automation Run As-account.</span><span class="sxs-lookup"><span data-stu-id="4745f-104">After an Automation account is successfully created, you can perform a simple test tooconfirm you are able toosuccessfully authenticate in Azure Resource Manager or Azure classic deployment using your newly created or updated Automation Run As account.</span></span>    

## <a name="automation-run-as-authentication"></a><span data-ttu-id="4745f-105">Automation Uitvoeren als-verificatie</span><span class="sxs-lookup"><span data-stu-id="4745f-105">Automation Run As authentication</span></span>
<span data-ttu-id="4745f-106">Hallo voorbeeldcode hieronder ook gebruiken[maken van een PowerShell-runbook](automation-creating-importing-runbook.md) tooverify-verificatie met behulp van Hallo uitvoeren als-account en uw aangepaste runbooks tooauthenticate en Resource Manager-resources beheren met uw Automation-account.</span><span class="sxs-lookup"><span data-stu-id="4745f-106">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Run As account and also in your custom runbooks tooauthenticate and manage Resource Manager resources with your Automation account.</span></span>   

    $connectionName = "AzureRunAsConnection"
    try
    {
        # Get hello connection "AzureRunAsConnection "
        $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

        "Logging in tooAzure..."
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

<span data-ttu-id="4745f-107">Let op Hallo van cmdlet gebruikt voor de verificatie in Hallo runbook - **Add-AzureRmAccount**, gebruikt Hallo *ServicePrincipalCertificate* parameterset.</span><span class="sxs-lookup"><span data-stu-id="4745f-107">Notice hello cmdlet used for authenticating in hello runbook - **Add-AzureRmAccount**, uses hello *ServicePrincipalCertificate* parameter set.</span></span>  <span data-ttu-id="4745f-108">In plaats van referenties wordt voor verificatie het certificaat van de service-principal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4745f-108">It authenticates by using service principal certificate, not credentials.</span></span>  

<span data-ttu-id="4745f-109">Wanneer u [hello runbook uitvoeren](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate uw Run As-account een [runbooktaak](automation-runbook-execution.md) is gemaakt, Hallo taakblade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht**tegel.</span><span class="sxs-lookup"><span data-stu-id="4745f-109">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="4745f-110">Hallo taakstatus wordt gestart als *in de wachtrij geplaatst* die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4745f-110">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="4745f-111">Verandert daarna te*starten* wanneer een werknemer claims Hallo taak, en vervolgens *met* wanneer Hallo runbook daadwerkelijk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4745f-111">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="4745f-112">Wanneer de runbooktaak Hallo is voltooid, zien we de status van **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="4745f-112">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="4745f-113">toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.</span><span class="sxs-lookup"><span data-stu-id="4745f-113">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="4745f-114">Op Hallo **uitvoer** blade ziet u het is geverifieerd en retourneert een lijst van alle resources in alle resourcegroepen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4745f-114">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all resources in all resource groups in your subscription.</span></span>  

<span data-ttu-id="4745f-115">Let erop dat tooremove Hallo codeblok beginnen met Hallo Opmerking `#Get all ARM resources from all resource groups` wanneer u code opnieuw gebruiken Hallo voor uw runbooks.</span><span class="sxs-lookup"><span data-stu-id="4745f-115">Just remember tooremove hello block of code starting with hello comment `#Get all ARM resources from all resource groups` when you reuse hello code for your runbooks.</span></span>

## <a name="classic-run-as-authentication"></a><span data-ttu-id="4745f-116">Klassieke Uitvoeren als-verificatie</span><span class="sxs-lookup"><span data-stu-id="4745f-116">Classic Run As authentication</span></span>
<span data-ttu-id="4745f-117">Hallo voorbeeldcode hieronder ook gebruiken[een PowerShell-runbook maken](automation-creating-importing-runbook.md) tooverify verificatie met behulp van klassieke Hallo uitvoeren als-account en uw aangepaste runbooks tooauthenticate en resources in het klassieke implementatiemodel Hallo beheren.</span><span class="sxs-lookup"><span data-stu-id="4745f-117">Use hello sample code below too[create a PowerShell runbook](automation-creating-importing-runbook.md) tooverify authentication using hello Classic Run As account and also in your custom runbooks tooauthenticate and manage resources in hello classic deployment model.</span></span>  

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID
    
    #Get all VMs in hello subscription and return list with name of each
    Get-AzureVM | ft Name

<span data-ttu-id="4745f-118">Wanneer u [hello runbook uitvoeren](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate uw Run As-account een [runbooktaak](automation-runbook-execution.md) is gemaakt, Hallo taakblade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht**tegel.</span><span class="sxs-lookup"><span data-stu-id="4745f-118">When you [run hello runbook](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate your Run As account, a [runbook job](automation-runbook-execution.md) is created, hello Job blade is displayed, and hello job status displayed in hello **Job Summary** tile.</span></span> <span data-ttu-id="4745f-119">Hallo taakstatus wordt gestart als *in de wachtrij geplaatst* die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="4745f-119">hello job status will start as *Queued* indicating that it is waiting for a runbook worker in hello cloud toobecome available.</span></span> <span data-ttu-id="4745f-120">Verandert daarna te*starten* wanneer een werknemer claims Hallo taak, en vervolgens *met* wanneer Hallo runbook daadwerkelijk wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4745f-120">It will then move too*Starting* when a worker claims hello job, and then *Running* when hello runbook actually starts running.</span></span>  <span data-ttu-id="4745f-121">Wanneer de runbooktaak Hallo is voltooid, zien we de status van **voltooid**.</span><span class="sxs-lookup"><span data-stu-id="4745f-121">When hello runbook job completes, we should see a status of **Completed**.</span></span>

<span data-ttu-id="4745f-122">toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.</span><span class="sxs-lookup"><span data-stu-id="4745f-122">toosee hello detailed results of hello runbook, click on hello **Output** tile.</span></span>  <span data-ttu-id="4745f-123">Op Hallo **uitvoer** blade ziet u het is geverifieerd en retourneert een lijst van alle virtuele machines van Azure door VMName die zijn geïmplementeerd in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="4745f-123">On hello **Output** blade, you should see it has successfully authenticated and returns a list of all Azure VMs by VMName that are deployed in your subscription.</span></span>  

<span data-ttu-id="4745f-124">Let erop dat tooremove Hallo cmdlet **Get-AzureVM** wanneer u code opnieuw gebruiken Hallo voor uw runbooks.</span><span class="sxs-lookup"><span data-stu-id="4745f-124">Just remember tooremove hello cmdlet **Get-AzureVM** when you reuse hello code for your runbooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4745f-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4745f-125">Next steps</span></span>
* <span data-ttu-id="4745f-126">Zie tooget gestart met PowerShell-runbooks [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4745f-126">tooget started with PowerShell runbooks, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>
* <span data-ttu-id="4745f-127">Zie toolearn meer informatie over grafisch ontwerpen [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).</span><span class="sxs-lookup"><span data-stu-id="4745f-127">toolearn more about Graphical Authoring, see [Graphical authoring in Azure Automation](automation-graphical-authoring-intro.md).</span></span>
