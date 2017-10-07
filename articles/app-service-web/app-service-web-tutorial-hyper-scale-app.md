---
title: aaaBuild hyperschaal-app in Azure | Microsoft Docs
description: Meer informatie over hoe toouse verschillende Azure-services toomaximize Hallo prestaties van een ASP.NET-app in Azure.
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Een hyperschaal web-app in Azure bouwen

Deze zelfstudie leert u hoe tooscale uit een ASP.NET-web-app in Azure toomaximize gebruiker vraagt.

Voordat u deze zelfstudie begint, zorg ervoor dat [hello Azure CLI is geïnstalleerd](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) op uw computer. U moet bovendien [Visual Studio](https://www.visualstudio.com/vs/) op uw lokale machine toorun Hallo-voorbeeldtoepassing.

## <a name="step-1---get-sample-application"></a>Stap 1 - Get-voorbeeldtoepassing
In deze stap moet u lokale ASP.NET-project Hallo instellen.

### <a name="clone-hello-application-repository"></a>Kloon Hallo toepassing opslagplaats

Open Hallo opdrachtregelprogramma terminal van uw keuze en `CD` tooa werkmap. De opdrachten uitvoeren Hallo volgende vervolgens tooclone Hallo-voorbeeldtoepassing. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Hallo-voorbeeldtoepassing uitvoeren in Visual Studio

Hallo-oplossing in Visual Studio openen.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Type `F5` toorun Hallo-toepassing.

In dit voorbeeld ASP.NET-webtoepassing afkomstig is van de standaardsjabloon Hallo en gebruiker sessies en maakt gebruik van Hallo uitvoercache zich blijft voordoen. Kijk eens naar `HighScaleApp\Controllers\HomeController.cs`. Hallo `Index()` methode voegt u een stukje gegevens toohello sessie.

```csharp
Session.Add("visited", "true"); 
```

En Hallo `About()` en `Contact()` methoden in de cache de uitvoer.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Stap 2: tooAzure implementeren
In deze stap maakt u een Azure-web-app maken en implementeren van uw tooit voorbeeld ASP.NET-toepassing.

### <a name="create-a-resource-group"></a>Een resourcegroep maken   
Gebruik [az groep maken](https://docs.microsoft.com/cli/azure/group#create) toocreate een [resourcegroep](../azure-resource-manager/resource-group-overview.md) in de regio West-Europa Hallo. Een resourcegroep is waar u alle plaatsen hello Azure-resources dat u wilt dat toomanage samen, zoals back-end Hallo web-app en alle SQL-Database.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee welke mogelijke waarden u kunt gebruiken voor `---location`, gebruik Hallo [az appservice lijst-locaties](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) opdracht.

### <a name="create-an-app-service-plan"></a>Een App Service-plan maken
Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate een "B1' [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Een App Service-abonnement is een schaaleenheid, met inbegrip van een willekeurig aantal apps dat u tooscale-up wilt of Hallo uit samen over dezelfde App Service-infrastructuur. Elk plan is ook toegewezen een [prijscategorie](https://azure.microsoft.com/en-us/pricing/details/app-service/). Hogere lagen bevatten betere hardware- en meer functies, zoals meer exemplaren van de scale-out.

Voor deze zelfstudie is B1 Hallo minimale laag waarmee scale-out toothree exemplaren. U kunt uw app altijd verplaatsen omhoog of omlaag Hallo prijscategorie later door te voeren [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Een webtoepassing maken
Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate een web-app met een unieke naam in `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Implementatiereferenties instellen
Gebruik [az appservice web implementatiegebruiker ingesteld](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset inzetten van uw account referenties voor App Service.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Configureer Git-implementatie
Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokale Git-implementatie.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

Met deze opdracht kunt u een uitvoer die op Hallo volgende lijkt:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Gebruik Hallo geretourneerd URL tooconfigure uw Git remote. Hallo volgende opdracht maakt gebruik van Hallo voorgaande voorbeeld van uitvoer.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Hallo-voorbeeldtoepassing implementeren
U bent nu klaar toodeploy uw voorbeeldtoepassing. Voer `git push` uit.

```powershell
git push azure master
```

Wanneer gevraagd om een wachtwoord, hello wachtwoord gebruiken dat u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>TooAzure web-app bladeren
Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee voor uw app live in Azure, met deze opdracht uitvoert.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Stap 3: verbinding maken met tooRedis
In deze stap maakt instellen u Azure Redis-Cache als een externe, geplaatste cache tooyour Azure-web-app. U kunt snel gebruikmaken van Redis toocache uw pagina-uitvoer. Bovendien wanneer u later uit uw web-apps schaalt, Redis helpt u behouden gebruikerssessies over meerdere exemplaren op betrouwbare wijze.

### <a name="create-an-azure-redis-cache"></a>Maak een Azure Redis Cache
Gebruik [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate in een Azure Redis-Cache en slaat u Hallo JSON-uitvoer. Gebruik een unieke naam in `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Hallo toepassing toouse Redis configureren
Hallo-verbindingsreeks voor uw cache-notatie.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

Hallo tweede regel geeft u een uitvoer die er als volgt uit:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

Maak in Visual Studio een web-configuratiebestand in de hoofdmap van uw project aangeroepen `redis.config` en plakken Hallo de volgende code in de App. In `value`, Hallo-verbindingsreeks uit Hallo uitvoer van PowerShell gebruiken.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Als u hello bekijkt `.gitignore` bestand in de Git-opslagplaats, ziet u dat dit bestand is uitgesloten van broncodebeheer. Op die manier uw vertrouwelijke gegevens veilig blijft. 

Open `Web.config`. Kennisgeving Hallo `<appSettings file="redis.config">` -element opgehaald Hallo-instelling die u hebt gemaakt in `redis.config`. 

Hallo opmerkingen vinden sectie `<sessionState>` en `<caching>`. Verwijder de opmerkingen in deze sectie.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Deze code lijkt voor Hallo Redis-verbindingsreeks die u hebt gedefinieerd in `RedisConnection`. 

Nu uw toepassing maakt gebruik van Redis toomanage sessies en opslaan in cache. Type `F5` toorun Hallo-toepassing. Indien gewenst, kunt u downloaden van een Redis-client toovisualize Hallo beheergegevens dat nu toohello cache is opgeslagen.

### <a name="configure-hello-connection-string-in-azure"></a>Hallo-verbindingsreeks configureren in Azure

Voor uw toepassing toowork in Azure, moet u tooconfigure Hallo dezelfde Redis-verbindingsreeks in uw Azure-web-app. Aangezien `redis.config` niet behouden in broncodebeheer, het is niet geïmplementeerd tooAzure tijdens het uitvoeren van Git-implementatie.

Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd Hallo connection string Hello dezelfde naam (`RedisConnection`).

AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection $connstring = '--$appName--resourcegroep myResourceGroup naam

Vergeet niet dat `$connstring` Hallo geformatteerd-verbindingsreeks bevat.

### <a name="redeploy-hello-application-tooazure"></a>Hallo toepassing tooAzure implementeren
Uw wijzigingen tooAzure voor Git-opdrachten toopush gebruiken

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Wanneer gevraagd om een wachtwoord, hello wachtwoord gebruiken dat u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Toohello Azure-web-app bladeren
Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee Hallo wijzigingen live in Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Stap 4: Scale toomultiple exemplaren
Hallo App Service-abonnement is Hallo schaaleenheid voor uw Azure-web-apps. tooscale uit uw web-app u schalen Hallo App Service-abonnement.

Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale uit Hallo App Service plan toothree exemplaren die Hallo maximaal toegestane aantal door Hallo B1 prijscategorie. Denk eraan dat B1 Hallo prijscategorie die u hebt gekozen toen u Hallo eerder App Service-abonnement hebt gemaakt. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Stap 5: Scale geografisch
Tijdens het geografisch schalen, kunt u uw app uitvoeren in meerdere regio's van hello Azure-cloud. Deze setup taakverdelingen van uw app verder op basis van Geografie en verlaagt de reactietijd van Hallo door het plaatsen van uw app dichter tooclient browsers.

In deze stap maakt u uw ASP.NET web app tooa tweede regio met schalen [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Aan het einde van de Hallo van Hallo stap hebt u een web-app uitgevoerd in West-Europa (al gemaakt) en een web-app uitgevoerd in Zuidoost-Azië (nog niet gemaakt). Beide apps kunnen worden geleverd vanuit Hallo dezelfde Traffic Manager-URL.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Hallo opschalen met Europa app tooStandard-laag
Integratie met Azure Traffic Manager vereist in App Service Hallo standaardcategorie prijzen. Gebruik [az appservice-abonnement update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale van uw App Service plan tooS1. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Een Traffic Manager-profiel maken 
Gebruik [az netwerk traffic manager-profiel maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate een Traffic Manager-profiel en toe te voegen tooyour resourcegroep. Gebruik een unieke DNS-naam in $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Hiermee wordt aangegeven dat dit profiel [gebruiker verkeer toohello dichtstbijzijnde endpoint van routes](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Hallo resource-ID van Hallo Europa app verkrijgen
Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hallo bron-ID van uw web-app.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Een Traffic Manager-eindpunt voor Hallo Europa app toevoegen
Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd een eindpunt tooyour Traffic Manager-profiel en gebruik Hallo bron-ID van uw web-app als doel Hallo.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Hallo Traffic Manager-eindpunt-URL ophalen
Uw Traffic Manager-profiel heeft nu een eindpunt dat punten tooyour bestaande web-app. Gebruik [az netwerk traffic manager-profiel weergeven](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget de URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Hallo-uitvoer in uw browser kopiëren. U ziet uw web-app opnieuw.

### <a name="create-an-azure-redis-cache-in-asia"></a>Maken van een Azure Redis-Cache in Azië
Nu u uw Azure-web-app toohello Zuidoost-Azië regio worden gerepliceerd. toostart, gebruik [az redis maken](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate een tweede Azure Redis-Cache in Zuidoost-Azië. Deze cache moet toobe die met uw app in Azië ditzelfde geplaatst.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`biedt Hallo Hallo Cachenaam Hallo cache West-Europa, Hello `-asia` achtervoegsel.

### <a name="create-an-app-service-plan-in-asia"></a>Maken van een App Service-plan in Azië
Gebruik [az appservice-abonnement maken](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate een tweede App Service-plan in Hallo Zuidoost-Azië regio, met behulp van Hallo dezelfde S1 trapsgewijs als Hallo West-Europa plan.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Een web-app maken in Azië
Gebruik [az appservice web maken](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate een tweede web-app.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`Geeft app Hallo-naam van app Hallo-West-Europa, Hallo Hello `-asia` achtervoegsel.

### <a name="configure-hello-connection-string-for-redis"></a>Hallo-verbindingsreeks configureren voor Redis
Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app Hallo verbindingsreeks voor Hallo cache Zuidoost-Azië.

AZ appservice webconfiguratie appsettings bijwerken--instellingen ' RedisConnection = $($redis.hostname): $($redis.sslPort), wachtwoord = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False '--naam $appName-Azië--resourcegroep myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>Configureer Git-implementatie voor Hallo Azië app.
Gebruik [-broncodebeheer in az appservice web-config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokale Git-implementatie voor Hallo tweede web-app.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

Met deze opdracht kunt u een uitvoer die op Hallo volgende lijkt:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Gebruik Hallo geretourneerd URL tooconfigure een tweede Git extern voor uw lokale opslagplaats. Hallo volgende opdracht maakt gebruik van Hallo voorgaande voorbeeld van uitvoer.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Uw voorbeeldtoepassing implementeren
Voer `git push` toodeploy uw voorbeeld toepassing toohello tweede Git remote. 

```bash
git push azure-asia master
```

Wanneer gevraagd om een wachtwoord, hello wachtwoord gebruiken dat u hebt opgegeven tijdens het uitvoeren van `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Toohello Azië app bladeren
Gebruik [az appservice surfen](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify die uw app live in Azure wordt uitgevoerd.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Hallo resource-ID van Hallo Azië app verkrijgen
Gebruik [az appservice web weergeven](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget Hallo bron-ID van uw web-app in Zuidoost-Azië.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Een Traffic Manager-eindpunt voor Hallo Azië app toevoegen
Gebruik [netwerkeindpunt voor het traffic manager az maken](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd een tweede eindpunt toohello Traffic Manager-profiel.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Regio id tooweb apps toevoegen
Gebruik [az appservice web config appsettings bijwerken](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd een regiospecifiek omgevingsvariabele.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Deze toepassingsinstelling wordt al gebruikt door de toepassingscode. Kijk eens naar `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Voltooid!

Probeer nu tooaccess Hallo-URL van uw Traffic Manager-profiel van browsers in verschillende geografische regio's. Clientbrowsers van Europa moeten weergeven 'ASP.NET West-Europa' en 'ASP.NET Zuidoost-Azië.' moet worden weergegeven in de browser van de client vanuit Azië

## <a name="more-resources"></a>Meer bronnen
