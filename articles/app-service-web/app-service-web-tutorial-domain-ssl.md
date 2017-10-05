---
title: Aangepast domein- en SSL toevoegen aan een Azure-web-app | Microsoft Docs
description: Informatie over het voorbereiden van uw Azure-web-app gaan productie door uw huisstijl toe te voegen. De aangepaste domeinnaam (vanity domein) worden toegewezen aan uw web-app en beveilig deze met een aangepaste SSL-certificaat.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a>Aangepast domein- en SSL toevoegen aan een Azure-web-app

Deze zelfstudie laat zien hoe u snel toewijzen van een aangepaste domeinnaam naar uw Azure-web-app en beveilig deze met een aangepaste SSL-certificaat. 

## <a name="before-you-begin"></a>Voordat u begint

Voordat u dit voorbeeld uitvoert, installeert u de [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokaal.

Ook moet u beheerderstoegang tot de pagina DNS-configuratie voor de provider van het desbetreffende domein. Bijvoorbeeld, om toe te voegen `www.contoso.com`, moet u mogelijk voor het configureren van DNS-vermeldingen voor `contoso.com`.

Tot slot moet u een geldige. PFX-bestand _en_ het wachtwoord voor het SSL-certificaat dat u wilt uploaden en binden. Dit SSL-certificaat moet worden geconfigureerd voor de aangepaste domeinnaam die u wilt beveiligen. In het bovenstaande voorbeeld uw SSL-certificaat moet beveiligen `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Stap 1: een Azure-web-app maken

### <a name="log-in-to-azure"></a>Meld u aan bij Azure.

We gaan nu de Azure CLI 2.0 in een terminalvenster gebruiken om de resources te maken die nodig zijn voor het hosten van onze Node.js-app in Azure.  Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Een resourcegroep maken   
Maak een resourcegroep met de opdracht [az group create](/cli/azure/group#create). Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals web-apps, databases en opslagaccounts, worden geïmplementeerd en beheerd. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

Gebruik de Azure CLI-opdracht `az appservice list-locations` om te zien welke waarden u kunt gebruiken voor `---location`.

## <a name="create-an-app-service-plan"></a>Een App Service-plan maken

Maak een App Service-plan met de opdracht [az appservice plan create](/cli/azure/appservice/plan#create). 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Het volgende voorbeeld wordt een App Service-abonnement met de naam `myAppServicePlan` met behulp van de **Basic** prijscategorie.

AZ appservice-abonnement maken--naam myAppServicePlan--resourcegroep myResourceGroup--sku B1

Wanneer de App Service-abonnement is gemaakt, de Azure CLI geeft informatie weer zoals in het volgende voorbeeld. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Een webtoepassing maken

Nu er een App Service-plan is gemaakt, maakt u binnen dit `myAppServicePlan` App Service-plan een web-app. De web-app kunt u bent een hosting ruimte om uw code te implementeren als een URL die u kunt de gedistribueerde toepassing weergeven. Gebruik de opdracht [az appservice web create](/cli/azure/appservice/web#create) om de web-app te maken. 

Vervang de naam van uw eigen unieke app waarin u ziet in de onderstaande opdracht de `<app_name>` tijdelijke aanduiding. Deze unieke naam zal worden gebruikt als het deel van naam van het standaarddomein voor de web-app zodat de naam moet uniek zijn in alle apps in Azure. Later kunt u een aangepaste DNS-vermelding toewijzen aan de web-app voordat u deze beschikbaar maakt voor uw gebruikers. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Wanneer de web-app is gemaakt, toont de Azure CLI soortgelijke informatie als in het volgende voorbeeld. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

Van de JSON-uitvoer `defaultHostName` standaarddomeinnaam van uw web-app bevat. Ga in uw browser naar dit adres.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Stap 2: configureer DNS-toewijzing

In deze stap maakt u een toewijzing toevoegen van een aangepast domein voor uw web-app standaarddomeinnaam, `<app_name>.azurewebsites.net`. Normaal gesproken uitvoeren u deze stap in de website van de domeinprovider van uw. Elke domeinregistrar website is enigszins verschillen, dus u moet de documentatie van uw provider. Hier zijn echter enkele algemene richtlijnen. 

### <a name="navigate-to-to-dns-management-page"></a>Ga naar naar DNS-pagina

Eerst aanmelden bij uw domeinregistrar website.  

Zoek de pagina voor het beheren van DNS-records. Zoek naar koppelingen of gebieden van de site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**. Vaak kunt u de koppeling vinden door de gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.

Wanneer u deze pagina hebt gevonden, zoekt u een koppeling waarmee u DNS-records toevoegt of bewerkt. Dit wordt mogelijk een **zonebestand** of **DNS-Records** koppeling of een **geavanceerde configuratie** koppeling.

### <a name="create-a-cname-record"></a>Een CNAME-record maken

Voeg een CNAME-record die de gewenste subdomeinnaam wordt toegewezen aan uw web-app standaarddomeinnaam (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de unieke naam van uw app).

Voor de `www.contoso.com` wanneer u een CNAME dat is toegewezen bijvoorbeeld maakt de `www` hostname naar `<app_name>.azurewebsites.net`.

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a>Stap 3: het aangepast domein configureren op uw web-app

Wanneer u klaar bent met het configureren van de toewijzing van de hostnaam in de website van de domeinprovider van uw, kunt u kunt het aangepast domein configureren op uw web-app. Gebruik de [az appservice web config hostnaam toevoegen](/cli/azure/appservice/web/config/hostname#add) opdracht voor het toevoegen van deze configuratie. 

In de onderstaande opdracht vervangen `<app_name>` met unieke app-naam en < your_custom_domain > met de aangepaste volledig gekwalificeerde domeinnaam (bijvoorbeeld `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

Het aangepaste domein is nu volledig toegewezen aan uw web-app. Ga in uw browser naar de aangepaste domeinnaam. Bijvoorbeeld:

```
http://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a>Stap 4: een aangepaste SSL-certificaat binden aan uw web-app

U hebt nu een Azure-web-app met de domeinnaam die u wilt dat in de adresbalk van de browser. Echter, als u naar navigeren de `https://<your_custom_domain>` nu het ophalen van een certificaatfout. 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Deze fout treedt op omdat uw web-app een SSL-certificaat-binding die overeenkomt met de naam van uw aangepaste domein nog geen. Echter, u niet krijgt een fout als u de navigatiefunctie `https://<app_name>.azurewebsites.net`. Dit komt doordat uw app, evenals alle apps van Azure App Service, is beveiligd met SSL-certificaat voor de `*.azurewebsites.net` jokertekendomein standaard. 

U moet toegang krijgen tot uw web-app op uw aangepaste domeinnaam, de SSL-certificaat voor uw aangepaste domein binden aan de web-app. Dit doet u in deze stap. 

### <a name="upload-the-ssl-certificate"></a>Het SSL-certificaat uploaden

Het SSL-certificaat voor uw aangepaste domein uploaden naar uw web-app met behulp van de [az appservice web config ssl uploaden](/cli/azure/appservice/web/config/ssl#upload) opdracht.

In de onderstaande opdracht vervangen `<app_name>` met de naam van uw unieke app `<path_to_ptx_file>` met het pad naar uw. PFX-bestand en `<password>` met het wachtwoord voor uw certificaat. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Wanneer het certificaat is geüpload, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

Van de JSON-uitvoer `thumbprint` ziet u de vingerafdruk van het geüploade certificaat. Kopieer de waarde voor de volgende stap.

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a>Het geüploade SSL-certificaat binden aan de web-app

Uw web-app heeft nu de aangepaste domeinnaam die u wilt en heeft ook een SSL-certificaat dat aangepaste domein beveiligt. De enige nog te doen is de geüploade certificaat binden aan de web-app. U dit doen met behulp van de [az appservice web config ssl-binding](/cli/azure/appservice/web/config/ssl#bind) opdracht.

In de onderstaande opdracht vervangen `<app_name>` met de naam van uw unieke app en `<thumbprint-from-previous-output>` met de certificaatvingerafdruk die u via de vorige opdracht. 

AZ appservice web config ssl bind--naam < app_naam >--resourcegroep myResourceGroup--certificaatvingerafdruk < vingerafdruk-van-vorige-output >--ssl-type SNI

Wanneer het certificaat is gekoppeld aan uw web-app, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:

{'Meldingenbeheer': 'Normale', 'clientAffinityEnabled': true, 'clientCertEnabled': false 'cloningInfo': null, 'containerSize': 0, "dailyMemoryTimeQuota": 0, "defaultHostName': ' < app_naam >. azurewebsites.net ', 'enabled': true, 'enabledHostNames': ['www.contoso.com' ' < app_naam >. azurewebsites.net ', ' < app_naam >. scm.azurewebsites.net '], 'gatewaySiteName': null, 'hostNameSslStates': [{'hostType': 'Standaard', 'name': ' < app_naam >. azurewebsites.net ', 'sslState': 'Disabled', 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'opslagplaats", "name": ' < app_naam >. scm.azurewebsites.net ', 'sslState': "Uitgeschakeld" 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'Standaard', 'name': 'www.contoso.com', 'sslState': 'SniEnabled' 'vingerafdruk': '9FD1D2D06E2293673E2A8D1CA484A092BD016D00', 'toUpdate': null, 'virtualIp': null}], 'hostnamen': ['www.contoso.com' ' < app_naam >. azurewebsites.net '], 'hostNamesDisabled': false 'hostingEnvironmentProfile': null 'id': ' /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < app_naam > ', 'isDefaultContainer': null, 'type': 'WebApp', 'lastModifiedTimeUtc': ' 2017-03-29T14:36:18.803333 ', 'locatie': 'West-Europa', 'maxNumberOfWorkers': null, 'microService': 'false', 'name': "< app_naam >" 'outboundIpAddresses': '13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1', 'premiumAppDeployed': null, 'repositorySiteName': '< app_naam >', 'gereserveerd': false 'resourceGroup': 'myResourceGroup', 'scmSiteAlsoStopped': false 'serverFarmId': ' / abonnementen/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft t.Web/serverfarms/myAppServicePlan ', 'siteConfig': null, 'slotSwapStatus': null, 'status': 'Actief', 'suspendedTill': null, 'labels': null, 'targetSwapSlot': null, 'trafficManagerHostNames': null, 'type': 'Microsoft.Web/sites', 'usageState': 'Standaard'}

Ga in uw browser naar HTTPS-eindpunt van uw aangepaste domeinnaam. Bijvoorbeeld:

```
https://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Meer bronnen

[Kopen en een aangepaste domeinnaam configureren in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kopen en configureren van een SSL-certificaat voor uw Azure App Service](web-sites-purchase-ssl-web-site.md)
