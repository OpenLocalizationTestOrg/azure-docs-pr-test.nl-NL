---
title: Azure Resource Manager gebaseerde PowerShell-opdrachten voor Azure-Web-App | Microsoft Docs
description: Informatie over het gebruiken van de nieuwe Azure Resource Manager gebaseerde PowerShell-opdrachten voor het beheren van uw Azure-Web-Apps.
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
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a>Azure-Web-Apps beheren met behulp van Azure Resource Manager gebaseerde PowerShell
> [!div class="op_single_selector"]
> * [Azure-CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Met Microsoft Azure PowerShell versie 1.0.0 zijn nieuwe opdrachten toegevoegd, die de gebruiker wilt geven op basis van Azure Resource Manager PowerShell-opdrachten gebruiken voor het beheren van Web-Apps.

Zie voor meer informatie over het beheren van resourcegroepen, [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md). 

Zie voor meer informatie over de volledige lijst met parameters en opties voor de PowerShell-cmdlets, de [volledige Cmdlet-verwijzing op basis van een Web App Azure Resource Manager PowerShell-Cmdlets](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Het beheren van App Service-plannen
### <a name="create-an-app-service-plan"></a>Een App Service-abonnement maken
Gebruik voor het maken van een app service-plan de **nieuw AzureRmAppServicePlan** cmdlet.

Hieronder volgen beschrijvingen van de verschillende parameters:

* **Naam**: naam van het app service-abonnement.
* **Locatie**: service-plan locatie.
* **ResourceGroupName**: resourcegroep met de nieuwe app service-abonnement.
* **Laag**: de gewenste prijscategorie (standaardwaarde is gratis, andere opties zijn gedeeld, Basic, Standard en Premium)
* **WorkerSize**: de grootte van de werknemers (de standaardwaarde is klein als de parameter lagen is opgegeven als Basic, Standard of Premium. Andere opties zijn Medium en Large.)
* **NumberofWorkers**: het aantal werknemers in de app service plan (de standaardwaarde is 1). 

Voorbeeld van deze cmdlet gebruikt:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Een App Service-abonnement maken in App Service-omgeving
Gebruik dezelfde opdracht voor het maken van een app service-abonnement in een app service-omgeving, **nieuw AzureRmAppServicePlan** opdracht met extra parameters van de as-omgeving naam en de naam van de as-omgeving resourcegroep opgeven.

Voorbeeld van deze cmdlet gebruikt:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

Controleer voor meer informatie over app service-omgeving, [Inleiding tot de App Service-omgeving](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Lijst met bestaande App Service-plannen
U kunt de bestaande app-serviceabonnementen gebruiken **Get-AzureRmAppServicePlan** cmdlet.

U kunt alle app-serviceabonnementen onder uw abonnement gebruiken: 

    Get-AzureRmAppServicePlan

U kunt alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

Als u een specifieke app service-abonnement, gebruikt u:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Een bestaand App Service-Plan configureren
U kunt de instellingen voor een bestaand app service-abonnement wijzigen met de **Set AzureRmAppServicePlan** cmdlet. U kunt de laag, worker grootte en het aantal werknemers wijzigen 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Schalen van een App Service-abonnement
Als u wilt schalen met een bestaand App Service Plan, gebruiken:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a>De grootte van de werknemer van een App Service-abonnement wijzigen
Als de grootte van de werknemers in een bestaand App Service Plan wijzigen, gebruikt u:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a>De laag van een App Service-abonnement wijzigen
Als u wilt wijzigen van de laag van een bestaand App Service Plan, gebruiken:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Verwijder een bestaande App Service-Plan
Als u wilt verwijderen van een bestaand app service-abonnement, moeten alle toegewezen web-apps worden verplaatst of verwijderd. Klik met de **verwijderen AzureRmAppServicePlan** cmdlet kunt u het app service-abonnement verwijderen.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>App Service-Web-Apps beheren
### <a name="create-a-web-app"></a>Een web-app maken
Voor het maken van een web-app gebruikt de **nieuw AzureRmWebApp** cmdlet.

Hieronder volgen beschrijvingen van de verschillende parameters:

* **Naam**: naam in voor de web-app.
* **AppServicePlan**: naam van de service-plan dat is gebruikt voor het hosten van de web-app.
* **ResourceGroupName**: resourcegroep die als host fungeert voor het App service-abonnement.
* **Locatie**: de locatie van web-app.

Voorbeeld van deze cmdlet gebruikt:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Een Web-App maken in App Service-omgeving
Een WebApp maken in een App Service omgeving (as-omgeving). Gebruik van dezelfde **nieuw AzureRmWebApp** opdracht met extra parameters om op te geven met de naam van de as-omgeving en de resourcegroep een naam die de as-omgeving behoort.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

Controleer voor meer informatie over app service-omgeving, [Inleiding tot de App Service-omgeving](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Een bestaande Web-App verwijderen
Verwijderen van een bestaande web-app kunt u de **verwijderen AzureRmWebApp** cmdlet, moet u de naam van de web-app en de naam van de resourcegroep opgeven.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Lijst met bestaande Web-Apps
U kunt de bestaande web-apps gebruiken de **Get-AzureRmWebApp** cmdlet.

U kunt alle web-apps in uw abonnement gebruiken:

    Get-AzureRmWebApp

U kunt alle web-apps onder een bepaalde resourcegroep gebruiken:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

Als u een specifieke web-app, gebruikt u:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Een bestaande Web-App configureren
U kunt de instellingen en configuraties voor een bestaande web-app wijzigen met de **Set AzureRmWebApp** cmdlet. Controleer voor een volledige lijst met parameters, de [Cmdlet verwijzende koppeling](https://msdn.microsoft.com/library/mt652487.aspx)

Voorbeeld (1): Gebruik deze cmdlet verbindingsreeksen wijzigen

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

(2) voorbeeld: toevoegen of wijzigen van app-instellingen

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


(3) voorbeeld: Stel de web-app in 64-bits modus uit te voeren

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a>Wijzig de status van een bestaande Web-App
#### <a name="restart-a-web-app"></a>Een web-app starten
Om opnieuw te starten in een web-app, moet u de groep en de bron van de web-app opgeven.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Een web-app stoppen
Als u wilt stoppen met een web-app, moet u de groep en de bron van de web-app opgeven.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Een web-app starten
U kunt de groep en de bron van de web-app moet opgeven voor het starten van een web-app.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Web-App Publishing profielen beheren
Elke web-app heeft een publicatieprofiel die kan worden gebruikt voor het publiceren van uw apps en verschillende bewerkingen kunnen worden uitgevoerd op het publiceren van profielen.

#### <a name="get-publishing-profile"></a>Krijg profiel
Als u het publicatieprofiel voor een web-app, gebruikt u:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Met deze opdracht geeft het publicatieprofiel aan de opdrachtregel als goed uitvoergegevens het publicatieprofiel in een tekstbestand.

#### <a name="reset-publishing-profile"></a>Opnieuw instellen van profiel publiceren
Om in te stellen op zowel het publishing wachtwoord voor FTP en web implementeren voor een web-app gebruikt:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Web-App certificaten beheren
Zie voor meer informatie over het beheren van certificaten voor web-app, [SSL-certificaten binding met behulp van PowerShell](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over Azure Resource Manager PowerShell-ondersteuning, [Azure PowerShell gebruiken met Azure Resource Manager.](../powershell-azure-resource-manager.md)
* Zie voor meer informatie over App Service-omgevingen, [Inleiding tot de App Service-omgeving.](app-service-app-service-environment-intro.md)
* Zie voor meer informatie over het beheren van App Service SSL-certificaten met behulp van PowerShell, [SSL-certificaten binding met behulp van PowerShell.](app-service-web-app-powershell-ssl-binding.md)
* Zie voor meer informatie over de volledige lijst met Azure Resource Manager gebaseerde PowerShell-cmdlets voor Azure-Web-Apps, [naslaginformatie over Azure-cmdlets van Web Apps in Azure Resource Manager PowerShell-Cmdlets.](https://msdn.microsoft.com/library/mt619237.aspx)
* * Zie voor meer informatie over het beheren van App Service met CLI, [Using Azure Resource Manager-Based XPlat CLI voor Azure-Web-App.](app-service-web-app-azure-resource-manager-xplat-cli.md)

