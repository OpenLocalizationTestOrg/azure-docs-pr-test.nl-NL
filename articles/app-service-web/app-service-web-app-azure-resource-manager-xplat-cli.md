---
title: Azure Resource Manager gebaseerde platformoverschrijdende opdrachtregel-hulpprogramma's voor Azure Web-App | Microsoft Docs
description: Informatie over het gebruik van de nieuwe Azure Resource Manager gebaseerde platformoverschrijdende opdrachtregel hulpmiddelen voor het beheren van uw Azure-Web-Apps.
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
ms.openlocfilehash: 7a03e1417617453c43edcc3787da10d171359757
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-xplat-cli-for-azure-app-service"></a>Met behulp van Azure Resource Manager gebaseerde XPlat CLI voor Azure App Service
> [!div class="op_single_selector"]
> * [Azure-CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)

Met de release van Microsoft Azure platformoverschrijdende opdrachtregelprogramma's versie 0.10.5 zijn nieuwe opdrachten toegevoegd. Deze opdrachten krijgt de gebruiker de mogelijkheid om te gebruiken op basis van Azure Resource Manager PowerShell-opdrachten voor het beheren van App Service.

Zie voor meer informatie over het beheren van resourcegroepen, [de Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen](../azure-resource-manager/xplat-cli-azure-resource-manager.md). 

> [!NOTE] 
> Bovendien uitproberen [Azure CLI 2.0](https://github.com/Azure/azure-cli), een volgende generatie CLI in Python is geschreven voor de resource management-implementatiemodel.
>
>

## <a name="managing-app-service-plans"></a>Het beheren van App Service-plannen
### <a name="create-an-app-service-plan"></a>Een App Service-abonnement maken
Gebruik voor het maken van een app service-plan de **azure appserviceplan maken** opdracht.

Hieronder volgen beschrijvingen van de verschillende parameters:

* **--resourcegroep**: resourcegroep met de nieuwe app service-abonnement.
* **--naam**: naam van het app service-abonnement.
* **--locatie**: app service-plan locatie.
* **--sku**: de gewenste prijscategorie sku (de opties zijn: F1 (gratis). D1 (gedeeld). B1 (Basic klein) B2 (Basic gemiddeld), en B3 (Basic grote). S1 (standaard klein) S2 (standaard gemiddeld), en S3 (standaard grote). P1 (klein Premium), P2 (Premium gemiddeld), en P3 (grote Premium).)
* **--exemplaren**: het aantal werknemers in de app service plan (de standaardwaarde is 1).

Voorbeeld van deze cmdlet gebruikt:

    azure appserviceplan create --name ContosoAppServicePlan --location "South Central US" --resource-group ContosoAzureResourceGroup --sku P1 --instances 10

#### <a name="create-a-linux-app-service-plan"></a>Een Linux-App Service-abonnement maken

Met behulp van dezelfde **azure appserviceplan maken** opdracht met de extra parameter **--islinux waar**. Noteer de beperkingen en regio's die worden beschreven in [Inleiding tot op Linux-App Service](app-service-linux-intro.md)

### <a name="list-existing-app-service-plans"></a>Lijst met bestaande App Service-plannen
U kunt de bestaande app-serviceabonnementen gebruiken **azure appserviceplan lijst** opdracht.

U kunt alle app-serviceabonnementen onder een bepaalde resourcegroep gebruiken:

    azure appserviceplan list --resource-group ContosoAzureResourceGroup

Als u een specifieke app service-abonnement, gebruikt **azure appserviceplan weergeven** opdracht:

    azure appserviceplan show --name ContosoAppServicePlan --resource-group southeastasia

### <a name="configure-an-existing-app-service-plan"></a>Een bestaand App Service-Plan configureren
U kunt de instellingen voor een bestaand app service-abonnement wijzigen met de **azure appserviceplan config** opdracht. U kunt de sku, en het aantal werknemers wijzigen 

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1 --instances 9

#### <a name="scaling-an-app-service-plan"></a>Schalen van een App Service-abonnement
Als u wilt schalen met een bestaand App Service Plan, gebruiken:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --instances 9

#### <a name="changing-the-sku-of-an-app-service-plan"></a>De SKU van een App Service-abonnement wijzigen
De sku van een bestaand App Service Plan met kunt u wijzigen:

    azure appserviceplan config --name ContosoAppServicePlan --resource-group ContosoAzureResourceGroup --sku S1


### <a name="delete-an-existing-app-service-plan"></a>Verwijder een bestaande App Service-Plan
Als u wilt verwijderen van een bestaand app service-abonnement, moeten alle toegewezen apps worden verplaatst of verwijderd. Klik met de **azure webapp verwijderen** opdracht kunt u het app service-abonnement verwijderen.

    azure appserviceplan delete --name ContosoAppServicePlan --resource-group southeastasia

## <a name="managing-app-service-apps"></a>App Service-apps beheren
### <a name="create-a-web-app"></a>Een webtoepassing maken
Voor het maken van een web-app gebruikt de **azure webapp maken** opdracht.

Hieronder volgen beschrijvingen van de verschillende parameters:

* **--naam**: naam in voor de web-app.
* **--plan**: naam van de service-plan dat is gebruikt voor het hosten van de web-app.
* **--resourcegroep**: resourcegroep die als host fungeert voor het App service-abonnement.
* **--locatie**: de locatie van web-app.

Voorbeeld van deze cmdlet gebruikt:

    azure webapp create --name ContosoWebApp --resource-group ContosoAzureResourceGroup --plan ContosoAppServicePlan --location "South Central US"

### <a name="delete-an-existing-app"></a>Verwijderen van een bestaande app
Als u wilt verwijderen van een bestaande app, kunt u de **azure webapp verwijderen** opdracht. U moet de naam van de app en de naam van de resourcegroep opgeven.

    azure webapp delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="list-existing-apps"></a>Lijst van bestaande apps
U kunt de bestaande apps gebruiken de **azure webapp lijst** opdracht.

U kunt alle apps in een specifieke resourcegroep gebruiken:

    azure webapp list --resource-group ContosoAzureResourceGroup

Als u een specifieke app, gebruikt de **azure webapp weergeven** opdracht.

    azure webapp show --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="configure-an-existing-app"></a>Een bestaande app configureren
U kunt de instellingen en configuraties voor een bestaande app wijzigen met de **azure webapp configuratieset** opdracht.

(1) voorbeeld: Wijzig de php-versie van een app 

    azure webapp config set --name ContosoWebApp --resource-group ContosoAzureResourceGroup --phpversion 5.6

(2) voorbeeld: toevoegen of wijzigen van app-instellingen

    webapp config appsettings set --name ContosoWebApp --resource-group ContosoAzureResourceGroup appsetting1=appsetting1value,appsetting2=appsetting2value

Weten wat andere configuratie kan worden gewijzigd, gebruikt u de **azure webapp-config -h ingesteld** opdracht.

### <a name="change-the-state-of-an-existing-app"></a>De status van een bestaande app wijzigen
#### <a name="restart-an-app"></a>Een app opnieuw starten
Als u wilt een app opnieuw is opgestart, moet u de groep en de bron van de app opgeven.

    azure webapp restart --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="stop-an-app"></a>Een app stoppen
Als u wilt stoppen van een app, moet u de groep en de bron van de app opgeven.

    azure webapp stop --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="start-an-app"></a>Een app te starten
Als u wilt een app, moet u de groep en de bron van de app opgeven.

    azure webapp start --name ContosoWebApp --resource-group ContosoAzureResourceGroup

### <a name="manage-publishing-profiles-of-an-app"></a>Publicatie van een app-profielen beheren
Elke app heeft een publicatieprofiel die kan worden gebruikt voor het publiceren van uw code.

#### <a name="get-publishing-profile"></a>Krijg profiel
Als u het publicatieprofiel voor een app, gebruikt u:

    azure webapp publishingprofile --name ContosoWebApp --resource-group ContosoAzureResourceGroup

Met deze opdracht geeft publishing profiel gebruikersnaam en wachtwoord voor de opdrachtregel.

### <a name="manage-app-hostnames"></a>App-hostnamen beheren
Voor het beheren van hostnaambindings voor uw app gebruikt de **azure webapp config hostnamen** opdracht  

#### <a name="list-hostname-bindings"></a>Hostnaambindings lijst
Als u de huidige hostnaambindings voor een app, gebruikt u:

    azure webapp config hostnames list --name ContosoWebApp --resource-group ContosoAzureResourceGroup

#### <a name="add-hostname-bindings"></a>Hostnaambindings toevoegen
Hostnaambindings toevoegen aan een app, als u wilt gebruiken:

    azure webapp config hostnames add --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

#### <a name="delete-hostname-bindings"></a>Hostnaambindings verwijderen
Als u wilt verwijderen hostnaambindings, gebruiken:

    azure webapp config hostnames delete --name ContosoWebApp --resource-group ContosoAzureResourceGroup --hostname www.contoso.com

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over de ondersteuning van Azure Resource Manager CLI, [de Azure CLI gebruiken voor het beheren van Azure-resources en resourcegroepen.](../azure-resource-manager/xplat-cli-azure-resource-manager.md)
* Zie voor meer informatie over het beheren van App Service met behulp van PowerShell, [Using Azure Resource Manager-Based PowerShell voor Azure-Web-Apps beheren.](app-service-web-app-azure-resource-manager-powershell.md)
* Zie voor meer informatie over Azure App Service op Linux, [Inleiding tot op Linux-App Service](app-service-linux-intro.md)
