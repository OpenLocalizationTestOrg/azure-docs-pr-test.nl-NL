---
title: aaaAzure op basis van een Resource Manager PowerShell-opdrachten voor Azure-Web-App | Microsoft Docs
description: Meer informatie over hoe toouse Hallo nieuwe Azure Resource Manager gebaseerde PowerShell-opdrachten toomanage uw Azure-Web-Apps.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Met behulp van PowerShell Azure Resource Manager-Based tooManage Azure Web Apps
> [!div class="op_single_selector"]
> * [Azure-CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Met Microsoft Azure PowerShell versie 1.0.0 zijn nieuwe opdrachten toegevoegd, die geven Hallo gebruiker Hallo mogelijkheid toouse op basis van Azure Resource Manager PowerShell-opdrachten toomanage Web-Apps.

toolearn over het beheren van resourcegroepen, Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md). 

toolearn over Hallo volledige lijst met parameters en opties voor Hallo PowerShell-cmdlets, Zie Hallo [volledige Cmdlet-verwijzing op basis van een Web App Azure Resource Manager PowerShell-Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Het beheren van App Service-plannen
### <a name="create-an-app-service-plan"></a>Een App Service-abonnement maken
een app service-plan toocreate gebruiken Hallo **nieuw AzureRmAppServicePlan** cmdlet.

Hieronder volgen beschrijvingen van de verschillende parameters Hallo:

* **Naam**: naam van het Hallo-app service-abonnement.
* **Locatie**: service-plan locatie.
* **ResourceGroupName**: bronnengroep met Hallo nieuwe app service-abonnement.
* **Laag**: Hallo gewenste prijscategorie (standaardwaarde is gratis, andere opties zijn gedeeld, Basic, Standard en Premium)
* **WorkerSize**: Hallo grootte van de werknemers (de standaardwaarde is klein als Hallo laag parameter is opgegeven als Basic, Standard of Premium. Andere opties zijn Medium en Large.)
* **NumberofWorkers**: aantal werknemers Hallo in Hallo-app service-abonnement (de standaardwaarde is 1). 

Voorbeeld toouse deze cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Een App Service-abonnement maken in App Service-omgeving
toocreate van een app service plan bent in een app service-omgeving, gebruik Hallo dezelfde opdracht **nieuw AzureRmAppServicePlan** opdracht met de naam van de extra parameters toospecify Hallo van as-omgeving en de naam van de as-omgeving resourcegroep.

Voorbeeld toouse deze cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

meer informatie over app service-omgeving, selectievakje toolearn [inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Lijst met bestaande App Service-plannen
Gebruik toolist Hallo bestaande app-serviceabonnementen **Get-AzureRmAppServicePlan** cmdlet.

toolist gebruiken voor alle app-serviceabonnementen onder uw abonnement: 

    Get-AzureRmAppServicePlan

toolist alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget een specifieke app service-abonnement gebruiken:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Een bestaand App Service-Plan configureren
toochange Hallo-instellingen voor een bestaand app service-abonnement gebruiken Hallo **Set AzureRmAppServicePlan** cmdlet. U kunt Hallo laag, de grootte van de werknemer en Hallo aantal werknemers wijzigen 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Schalen van een App Service-abonnement
een bestaand App Service-Plan, tooscale gebruiken:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Hallo worker grootte wijzigen van een App Service-Plan
toochange hello grootte van de werknemers in een bestaand App Service-Plan, gebruiken:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Hallo laag van een App Service-abonnement wijzigen
toochange hello laag van een bestaande App Service-Plan, gebruiken:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Verwijder een bestaande App Service-Plan
een bestaand app service-abonnement toodelete, worden alle web-apps nodig toobe verplaatst of verwijderd eerst toegewezen. Met behulp van Hallo **verwijderen AzureRmAppServicePlan** cmdlet kunt u Hallo-app service-abonnement verwijderen.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>App Service-Web-Apps beheren
### <a name="create-a-web-app"></a>Een web-app maken
een web-app toocreate gebruiken Hallo **nieuw AzureRmWebApp** cmdlet.

Hieronder volgen beschrijvingen van de verschillende parameters Hallo:

* **Naam**: naam in voor Hallo web-app.
* **AppServicePlan**: Geef een naam voor service-abonnement Hallo toohost Hallo web-app gebruikt.
* **ResourceGroupName**: resourcegroep die als host fungeert voor Hallo-App service-abonnement.
* **Locatie**: Hallo web-app-locatie.

Voorbeeld toouse deze cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Een Web-App maken in App Service-omgeving
toocreate een web-app in een App Service omgeving (as-omgeving). Gebruik dezelfde Hallo **nieuw AzureRmWebApp** opdracht met extra parameters toospecify Hallo as-omgeving naam en Hallo Resourcegroepnaam behorend Hallo as-omgeving.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

meer informatie over app service-omgeving, selectievakje toolearn [inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Een bestaande Web-App verwijderen
een bestaande web-app kunt u Hallo toodelete **verwijderen AzureRmWebApp** cmdlet, moet u toospecify Hallo naam van Hallo web-app en de naam van resourcegroep Hallo.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Lijst met bestaande Web-Apps
toolist hello bestaande WebApps gebruiken Hallo **Get-AzureRmWebApp** cmdlet.

toolist gebruiken voor alle web-apps in uw abonnement:

    Get-AzureRmWebApp

toolist alle web-apps onder een bepaalde resourcegroep gebruiken:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget een specifieke web-app gebruiken:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Een bestaande Web-App configureren
toochange hello instellingen en configuraties voor een bestaande web-app gebruiken Hallo **Set AzureRmWebApp** cmdlet. Controleer voor een volledige lijst met parameters Hallo [Cmdlet verwijzende koppeling](https://msdn.microsoft.com/library/mt652487.aspx)

Voorbeeld (1): Gebruik deze cmdlet toochange-verbindingsreeksen

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

(2) voorbeeld: toevoegen of wijzigen van app-instellingen

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


(3) voorbeeld: Hallo web app toorun in 64-bits modus instellen

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Hallo-status van een bestaande Web-App wijzigen
#### <a name="restart-a-web-app"></a>Een web-app starten
toorestart een web-app, moet u de naam en resource groep Hallo van Hallo web-app opgeven.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Een web-app stoppen
toostop een web-app, moet u de naam en resource groep Hallo van Hallo web-app opgeven.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Een web-app starten
toostart een web-app, moet u de naam en resource groep Hallo van Hallo web-app opgeven.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Web-App Publishing profielen beheren
Elke web-app heeft een publicatieprofiel die gebruikt toopublish worden kan uw apps en verschillende bewerkingen kunnen worden uitgevoerd op het publiceren van profielen.

#### <a name="get-publishing-profile"></a>Krijg profiel
tooget hello profiel voor een web-app, gebruik publiceren:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Met deze opdracht geeft Hallo profiel toohello opdrachtregel ook publiceren uitvoer Hallo profiel tooa tekstbestand publiceren.

#### <a name="reset-publishing-profile"></a>Opnieuw instellen van profiel publiceren
tooreset beide publishing wachtwoord Hallo voor FTP en web implementeren voor een web-app gebruikt:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Web-App certificaten beheren
toolearn over hoe toomanage web-app-certificaten, Zie [SSL-certificaten binding met behulp van PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Volgende stappen
* toolearn over Azure Resource Manager PowerShell-ondersteuning, Zie [Azure PowerShell gebruiken met Azure Resource Manager.](../powershell-azure-resource-manager.md)
* toolearn over App Service-omgevingen, Zie [inleiding tooApp Service-omgeving.](app-service-app-service-environment-intro.md)
* toolearn over het beheren van App Service SSL-certificaten met behulp van PowerShell, Zie [SSL-certificaten binding met behulp van PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* toolearn over Hallo volledige lijst met Azure Resource Manager gebaseerde PowerShell-cmdlets voor Azure Web Apps, Zie [naslaginformatie over Azure-cmdlets van Web Apps in Azure Resource Manager PowerShell-Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)
* * toolearn over het beheren van App Service met CLI, Zie [Using Azure Resource Manager-Based XPlat CLI voor Azure-Web-App.](app-service-web-app-azure-resource-manager-xplat-cli.md)

