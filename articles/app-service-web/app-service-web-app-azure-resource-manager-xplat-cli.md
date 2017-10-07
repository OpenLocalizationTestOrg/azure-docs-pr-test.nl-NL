---
title: aaaAzure Resource Manager gebaseerde platformoverschrijdende opdrachtregel-hulpprogramma's voor Azure-Web-App | Microsoft Docs
description: Meer informatie over hoe toouse Hallo nieuwe hulpprogramma's voor Azure Resource Manager gebaseerde platformoverschrijdende opdrachtregel toomanage uw Azure-Web-Apps.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: d415b195-4262-416f-b59f-7e1aef200054
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 5f5e03edcb01154aef3bd220cd27358f69656ef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Met behulp van Azure Resource Manager gebaseerde XPlat CLI voor Azure App Service
> [!div class="op_single_selector"]
> * [Azure-CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Hallo-versie van Microsoft Azure platformoverschrijdende opdrachtregelprogramma's versie 0.10.5, zijn nieuwe opdrachten toegevoegd. Deze opdrachten geven Hallo gebruiker Hallo mogelijkheid toouse op basis van Azure Resource Manager PowerShell-opdrachten toomanage App Service.

toolearn over het beheren van resourcegroepen, Zie [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Bovendien uitproberen [Azure CLI 2.0](https://github.com/Azure/azure-cli), een volgende generatie CLI in Python is geschreven voor Hallo resource management-implementatiemodel.
>
>

## <a name="managing-app-service-plans"></a>Het beheren van App Service-plannen
### <a name="create-an-app-service-plan"></a>Een App Service-abonnement maken
een app service-plan toocreate gebruiken Hallo **azure appserviceplan maken** opdracht.

Hieronder volgen beschrijvingen van de verschillende parameters Hallo:

* **--resourcegroep**: bronnengroep met Hallo nieuwe app service-abonnement.
* **--naam**: naam van het Hallo-app service-abonnement.
* **--locatie**: app service-plan locatie.
* **--sku**: Hallo gewenste prijscategorie sku (Hallo opties zijn: F1 (gratis). D1 (gedeeld). B1 (Basic klein) B2 (Basic gemiddeld), en B3 (Basic grote). S1 (standaard klein) S2 (standaard gemiddeld), en S3 (standaard grote). P1 (klein Premium), P2 (Premium gemiddeld), en P3 (grote Premium).)
* **--exemplaren**: aantal werknemers Hallo in Hallo-app service-abonnement (de standaardwaarde is 1).

Voorbeeld toouse deze cmdlet:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Een Linux-App Service-abonnement maken

Met behulp van dezelfde Hallo **azure appserviceplan maken** opdracht Hello extra parameter **--islinux waar**. Houd er rekening mee Hallo beperkingen en regio's die worden beschreven in [inleiding tooApp-Service op Linux](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Lijst met bestaande App Service-plannen
Gebruik toolist Hallo bestaande app-serviceabonnementen **azure appserviceplan lijst** opdracht.

toolist alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

gebruik van een specifieke app service-abonnement tooget **azure appserviceplan weergeven** opdracht:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Een bestaand App Service-Plan configureren
toochange Hallo-instellingen voor een bestaand app service-abonnement gebruiken Hallo **azure appserviceplan config** opdracht. U kunt Hallo sku en het aantal werknemers Hallo wijzigen 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Schalen van een App Service-abonnement
een bestaand App Service-Plan, tooscale gebruiken:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-hello-sku-of-an-app-service-plan"></a>Hallo SKU van een App Service-abonnement wijzigen
toochange hello sku van een bestaande App Service-Plan, gebruiken:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Verwijder een bestaande App Service-Plan
toodelete een bestaand app service-abonnement, worden alle apps moeten toobe verplaatst of verwijderd eerst toegewezen. Met behulp van Hallo **azure webapp verwijderen** opdracht kunt u Hallo-app service-abonnement verwijderen.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>App Service-apps beheren
### <a name="create-a-web-app"></a>Een webtoepassing maken
een web-app toocreate gebruiken Hallo **azure webapp maken** opdracht.

Hieronder volgen beschrijvingen van de verschillende parameters Hallo:

* **--naam**: naam in voor Hallo web-app.
* **--plan**: Geef een naam voor service-abonnement Hallo toohost Hallo web-app gebruikt.
* **--resourcegroep**: resourcegroep die als host fungeert voor Hallo-App service-abonnement.
* **--locatie**: Hallo web-app-locatie.

Voorbeeld toouse deze cmdlet:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Verwijderen van een bestaande app
een bestaande app toodelete, kunt u Hallo **azure webapp verwijderen** opdracht. Moet u toospecify Hallo-naam van Hallo-app en de naam van resourcegroep Hallo.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Lijst van bestaande apps
toolist hello bestaande apps, gebruikt u Hallo **azure webapp lijst** opdracht.

toolist gebruiken voor alle apps in een specifieke resourcegroep:

    azure webapp list --resource-group ContosoAzureResourceGroup

een specifieke app tooget gebruiken Hallo **azure webapp weergeven** opdracht.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Een bestaande app configureren
toochange hello instellingen en configuraties voor een bestaande app gebruiken Hallo **azure webapp configuratieset** opdracht.

(1) voorbeeld: Wijzig de Hallo php-versie van een app 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

(2) voorbeeld: toevoegen of wijzigen van app-instellingen

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

welke andere configuratie kan worden gewijzigd, tooknow gebruik Hallo **azure webapp-config -h ingesteld** opdracht.

### <a name="change-hello-state-of-an-existing-app"></a>Hallo-status van een bestaande app wijzigen
#### <a name="restart-an-app"></a>Een app opnieuw starten
toorestart een app, moet u Hallo en de bron groep Hallo app opgeven.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Een app stoppen
toostop een app, moet u Hallo en de bron groep Hallo app opgeven.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Een app te starten
toostart een app, moet u Hallo en de bron groep Hallo app opgeven.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Publicatie van een app-profielen beheren
Elke app heeft een publicatieprofiel die gebruikt toopublish worden kan uw code.

#### <a name="get-publishing-profile"></a>Krijg profiel
tooget hello profiel voor een app, gebruik publiceren:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Met deze opdracht geeft Hallo publiceren profiel gebruikersnaam en wachtwoord toohello vanaf de opdrachtregel.

### <a name="manage-app-hostnames"></a>App-hostnamen beheren
hostnaambindings toomanage voor uw app gebruiken Hallo **azure webapp config hostnamen** opdracht  

#### <a name="list-hostname-bindings"></a>Hostnaambindings lijst
tooget hello huidige hostnaam bindingen voor een app gebruiken:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Hostnaambindings toevoegen
tooadd hostnaam bindingen tooan app, gebruiken:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Hostnaambindings verwijderen
hostnaambindings toodelete, gebruiken:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn over de ondersteuning van Azure Resource Manager CLI [hello Azure CLI toomanage Azure gebruiken resources en resourcegroepen.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* toolearn over het beheren van App Service met behulp van PowerShell, Zie [Using Azure Resource Manager-Based PowerShell tooManage Azure Web Apps.](app-service-web-app-azure-resource-manager-powershell.md)
* toolearn over Azure App Service op Linux, Zie [inleiding tooApp-Service op Linux](app-service-linux-intro.md)
