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
# <a name="test-azure-automation-run-as-account-authentication"></a>De verificatie van een Azure Automation Uitvoeren als-account testen
Nadat een Automation-account is gemaakt, kunt u een eenvoudige test tooconfirm kunt uitvoeren toosuccessfully zich verifiëren bij Azure Resource Manager of Azure-klassieke implementatie met behulp van uw nieuwe of bijgewerkte Automation Run As-account.    

## <a name="automation-run-as-authentication"></a>Automation Uitvoeren als-verificatie
Hallo voorbeeldcode hieronder ook gebruiken[maken van een PowerShell-runbook](automation-creating-importing-runbook.md) tooverify-verificatie met behulp van Hallo uitvoeren als-account en uw aangepaste runbooks tooauthenticate en Resource Manager-resources beheren met uw Automation-account.   

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

Let op Hallo van cmdlet gebruikt voor de verificatie in Hallo runbook - **Add-AzureRmAccount**, gebruikt Hallo *ServicePrincipalCertificate* parameterset.  In plaats van referenties wordt voor verificatie het certificaat van de service-principal gebruikt.  

Wanneer u [hello runbook uitvoeren](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate uw Run As-account een [runbooktaak](automation-runbook-execution.md) is gemaakt, Hallo taakblade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht**tegel. Hallo taakstatus wordt gestart als *in de wachtrij geplaatst* die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar. Verandert daarna te*starten* wanneer een werknemer claims Hallo taak, en vervolgens *met* wanneer Hallo runbook daadwerkelijk wordt uitgevoerd.  Wanneer de runbooktaak Hallo is voltooid, zien we de status van **voltooid**.

toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.  Op Hallo **uitvoer** blade ziet u het is geverifieerd en retourneert een lijst van alle resources in alle resourcegroepen in uw abonnement.  

Let erop dat tooremove Hallo codeblok beginnen met Hallo Opmerking `#Get all ARM resources from all resource groups` wanneer u code opnieuw gebruiken Hallo voor uw runbooks.

## <a name="classic-run-as-authentication"></a>Klassieke Uitvoeren als-verificatie
Hallo voorbeeldcode hieronder ook gebruiken[een PowerShell-runbook maken](automation-creating-importing-runbook.md) tooverify verificatie met behulp van klassieke Hallo uitvoeren als-account en uw aangepaste runbooks tooauthenticate en resources in het klassieke implementatiemodel Hallo beheren.  

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

Wanneer u [hello runbook uitvoeren](automation-starting-a-runbook.md#starting-a-runbook-with-the-azure-portal) toovalidate uw Run As-account een [runbooktaak](automation-runbook-execution.md) is gemaakt, Hallo taakblade wordt weergegeven en Hallo taakstatus wordt weergegeven in Hallo **taakoverzicht**tegel. Hallo taakstatus wordt gestart als *in de wachtrij geplaatst* die aangeeft dat er wordt gewacht tot een runbook worker in Hallo cloud toobecome beschikbaar. Verandert daarna te*starten* wanneer een werknemer claims Hallo taak, en vervolgens *met* wanneer Hallo runbook daadwerkelijk wordt uitgevoerd.  Wanneer de runbooktaak Hallo is voltooid, zien we de status van **voltooid**.

toosee Hallo gedetailleerde resultaten van Hallo runbook, klikt u op Hallo **uitvoer** tegel.  Op Hallo **uitvoer** blade ziet u het is geverifieerd en retourneert een lijst van alle virtuele machines van Azure door VMName die zijn geïmplementeerd in uw abonnement.  

Let erop dat tooremove Hallo cmdlet **Get-AzureVM** wanneer u code opnieuw gebruiken Hallo voor uw runbooks.

## <a name="next-steps"></a>Volgende stappen
* Zie tooget gestart met PowerShell-runbooks [Mijn eerste PowerShell-runbook](automation-first-runbook-textual-powershell.md).
* Zie toolearn meer informatie over grafisch ontwerpen [grafisch ontwerpen in Azure Automation](automation-graphical-authoring-intro.md).
