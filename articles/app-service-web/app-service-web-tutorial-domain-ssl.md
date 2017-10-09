---
title: aangepast domein aaaAdd en SSL tooan Azure web-app | Microsoft Docs
description: Meer informatie over hoe tooprepare uw Azure web-app toogo productie door uw huisstijl toe te voegen. Overzicht van Hallo aangepaste domain name (vanity domein) tooyour web-app en beveilig deze met een aangepaste SSL-certificaat.
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
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Aangepast domein- en SSL tooan Azure-web-app toevoegen

Deze zelfstudie leert u hoe tooquickly toewijzen van een aangepast domein naam tooyour Azure-web-app en beveilig deze met een aangepaste SSL-certificaat. 

## <a name="before-you-begin"></a>Voordat u begint

Voordat u dit voorbeeld uitvoert, installeert u Hallo [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokaal.

U moet ook pagina beheerderstoegang toohello DNS-configuratie voor de provider van het desbetreffende domein. Bijvoorbeeld: tooadd `www.contoso.com`, moet u toobe kunnen tooconfigure DNS-vermeldingen voor `contoso.com`.

Tot slot moet u een geldige. PFX-bestand _en_ het wachtwoord voor Hallo gewenste tooupload SSL-certificaat en bindt. Dit SSL-certificaat moet geconfigureerde toosecure Hallo aangepaste domeinnaam gewenste. In Hallo hierboven voorbeeld uw SSL-certificaat moet beveiligen `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Stap 1: een Azure-web-app maken

### <a name="log-in-tooazure"></a>Meld u bij tooAzure

We zijn nu gaat toouse hello Azure CLI 2.0 in een terminalvenster toocreate Hallo bronnen nodig toohost onze Node.js-app in Azure.  Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Een resourcegroep maken   
Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create). Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals web-apps, databases en opslagaccounts, worden geïmplementeerd en beheerd. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee welke mogelijke waarden u kunt gebruiken voor `---location`, gebruik Hallo `az appservice list-locations` Azure CLI-opdracht.

## <a name="create-an-app-service-plan"></a>Een App Service-plan maken

Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Hallo volgende voorbeeld maakt u een App Service-abonnement met de naam `myAppServicePlan` met Hallo **Basic** prijscategorie.

AZ appservice-abonnement maken--naam myAppServicePlan--resourcegroep myResourceGroup--sku B1

Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. 

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

Nu dat een App Service-abonnement is gemaakt, maakt u een web-app binnen Hallo `myAppServicePlan` App Service-abonnement. Hallo web-app biedt u een hosting ruimte toodeploy bent uw code, evenals een URL biedt u tooview Hallo toepassing geïmplementeerd. Gebruik Hallo [az appservice web maken](/cli/azure/appservice/web#create) opdracht toocreate Hallo web-app. 

Vervang de naam van uw eigen unieke app waar u Hallo zien in Hallo opdracht hieronder `<app_name>` tijdelijke aanduiding. Deze unieke naam zal worden gebruikt als onderdeel van de Hallo van Hallo standaarddomeinnaam voor Hallo-web-app zodat Hallo naam toobe uniek zijn in alle apps in Azure moet. U kunt aangepaste DNS-vermelding toohello web-app later toewijzen voordat u deze tooyour gebruikers weergeven. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Wanneer Hallo web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. 

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

Van Hallo JSON-uitvoer `defaultHostName` standaarddomeinnaam van uw web-app bevat. Navigeer in uw browser toothis adres.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Stap 2: configureer DNS-toewijzing

In deze stap maakt u een toewijzing toevoegen van een aangepast domein tooyour van web-app standaarddomeinnaam, `<app_name>.azurewebsites.net`. Normaal gesproken uitvoeren u deze stap in de website van de domeinprovider van uw. Elke domeinregistrar website is enigszins verschillen, dus u moet de documentatie van uw provider. Hier zijn echter enkele algemene richtlijnen. 

### <a name="navigate-tootoodns-management-page"></a>Navigeer tootooDNS management-pagina

Meld u eerst in tooyour domeinregistrar website.  

Vervolgens Hallo pagina vinden voor het beheren van DNS-records. Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**. U kunt vaak Hallo koppeling vinden door gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.

Wanneer u deze pagina hebt gevonden, zoekt u een koppeling waarmee u DNS-records toevoegt of bewerkt. Dit wordt mogelijk een **zonebestand** of **DNS-Records** koppeling of een **geavanceerde configuratie** koppeling.

### <a name="create-a-cname-record"></a>Een CNAME-record maken

Voeg een CNAME-record dat is toegewezen standaarddomeinnaam Hallo gewenste subdomein naam tooyour van web-app (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de unieke naam van uw app).

Voor Hallo `www.contoso.com` bijvoorbeeld als u een CNAME dat is toegewezen Hallo maken `www` hostnaam te`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Stap 3: Hallo aangepast domein configureren op uw web-app

Wanneer u klaar bent met het Hallo hostnaam toewijzing configureren in de website van de domeinprovider van uw, bent u klaar tooconfigure Hallo aangepast domein op uw web-app. Gebruik Hallo [az appservice web config hostnaam toevoegen](/cli/azure/appservice/web/config/hostname#add) opdracht tooadd deze configuratie. 

In onderstaande Hallo opdracht, Vervang `<app_name>` met unieke app-naam en < your_custom_domain > met Hallo aangepaste FQDN-naam (bijvoorbeeld `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

Hallo aangepaste domein is nu volledig toegewezen tooyour web-app. Navigeer in uw browser toohello aangepaste domeinnaam. Bijvoorbeeld:

```
http://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Stap 4: een aangepaste SSL-certificaat tooyour web-app binden

U hebt nu een Azure-web-app met Hallo-domeinnaam die u wilt dat in de adresbalk van de browser Hallo. Echter, als u de navigatiefunctie toohello `https://<your_custom_domain>` nu het ophalen van een certificaatfout. 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Deze fout treedt op omdat uw web-app een SSL-certificaat-binding die overeenkomt met de naam van uw aangepaste domein nog geen. Echter, u niet krijgt een fout als u te navigeren`https://<app_name>.azurewebsites.net`. Dit is omdat uw app, evenals alle apps van Azure App Service, is beveiligd met SSL-certificaat voor Hallo Hallo `*.azurewebsites.net` jokertekendomein standaard. 

In het sorteren van de tooaccess uw web-app op uw aangepaste domeinnaam, moet u toobind Hallo SSL-certificaat voor uw aangepaste domein toohello web-app. Dit doet u in deze stap. 

### <a name="upload-hello-ssl-certificate"></a>Hallo SSL-certificaat uploaden

Hallo SSL-certificaat voor uw aangepaste domein tooyour web-app uploaden via Hallo [az appservice web config ssl uploaden](/cli/azure/appservice/web/config/ssl#upload) opdracht.

In onderstaande Hallo opdracht, Vervang `<app_name>` met de naam van uw unieke app `<path_to_ptx_file>` met Hallo pad tooyour. PFX-bestand en `<password>` met het wachtwoord voor uw certificaat. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Wanneer het Hallo-certificaat is geüpload, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

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

Van Hallo JSON-uitvoer `thumbprint` ziet u de vingerafdruk van het geüploade certificaat. Kopieer de waarde voor de volgende stap Hallo.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>BIND Hallo toohello web-app van SSL-certificaat geüpload

Uw web-app heeft nu de aangepaste domeinnaam Hallo gewenste en heeft ook een SSL-certificaat dat aangepaste domein beveiligt. Hallo is alleen ding links toodo toobind Hallo geüploade certificaat toohello web-app. U dit doen met behulp van Hallo [az appservice web config ssl-binding](/cli/azure/appservice/web/config/ssl#bind) opdracht.

In onderstaande Hallo opdracht, Vervang `<app_name>` met de naam van uw unieke app en `<thumbprint-from-previous-output>` met Hallo certificaatvingerafdruk die u via de vorige opdracht Hallo. 

AZ appservice web config ssl bind--naam < app_naam >--resourcegroep myResourceGroup--certificaatvingerafdruk < vingerafdruk-van-vorige-output >--ssl-type SNI

Wanneer het Hallo-certificaat wordt gebonden tooyour web-app, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

{'Meldingenbeheer': 'Normale', 'clientAffinityEnabled': true, 'clientCertEnabled': false 'cloningInfo': null, 'containerSize': 0, "dailyMemoryTimeQuota": 0, "defaultHostName': ' < app_naam >. azurewebsites.net ', 'enabled': true, 'enabledHostNames': ['www.contoso.com' ' < app_naam >. azurewebsites.net ', ' < app_naam >. scm.azurewebsites.net '], 'gatewaySiteName': null, 'hostNameSslStates': [{'hostType': 'Standaard', 'name': ' < app_naam >. azurewebsites.net ', 'sslState': 'Disabled', 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'opslagplaats", "name": ' < app_naam >. scm.azurewebsites.net ', 'sslState': "Uitgeschakeld" 'vingerafdruk': null, 'toUpdate': null, 'virtualIp': null}, {'hostType': 'Standaard', 'name': 'www.contoso.com', 'sslState': 'SniEnabled' 'vingerafdruk': '9FD1D2D06E2293673E2A8D1CA484A092BD016D00', 'toUpdate': null, 'virtualIp': null}], 'hostnamen': ['www.contoso.com' ' < app_naam >. azurewebsites.net '], 'hostNamesDisabled': false 'hostingEnvironmentProfile': null 'id': ' /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < app_naam > ', 'isDefaultContainer': null, 'type': 'WebApp', 'lastModifiedTimeUtc': ' 2017-03-29T14:36:18.803333 ', 'locatie': 'West-Europa', 'maxNumberOfWorkers': null, 'microService': 'false', 'name': "< app_naam >" 'outboundIpAddresses': '13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1', 'premiumAppDeployed': null, 'repositorySiteName': '< app_naam >', 'gereserveerd': false 'resourceGroup': 'myResourceGroup', 'scmSiteAlsoStopped': false 'serverFarmId': ' / abonnementen/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft t.Web/serverfarms/myAppServicePlan ', 'siteConfig': null, 'slotSwapStatus': null, 'status': 'Actief', 'suspendedTill': null, 'labels': null, 'targetSwapSlot': null, 'trafficManagerHostNames': null, 'type': 'Microsoft.Web/sites', 'usageState': 'Standaard'}

Navigeer in uw browser tooHTTPS eindpunt van uw aangepaste domeinnaam. Bijvoorbeeld:

```
https://www.contoso.com 
``` 

![app-service-web-service-gemaakt](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Meer bronnen

[Kopen en een aangepaste domeinnaam configureren in Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kopen en configureren van een SSL-certificaat voor uw Azure App Service](web-sites-purchase-ssl-web-site.md)
